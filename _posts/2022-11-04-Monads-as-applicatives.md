---
layout: post
title: Monads as applicative functors
---

Applicative functor (or just "applicative" in short) is a more general abstraction than a monad. 
In other words, monad is an applicative with extra functionality, and therefore a more specialised and stronger abstraction.

Applicative can be expressed in the following three ways:

```
unit + apply
unit + map2
unit + map + product   
```

By using an applicative functor instead of the non-applicative one, we can map by using multi-parameter curried functions 
(either by applying curried parameters one by one with apply, or by lifting everything into a product and mapping that).

Monad can be expressed in the following three ways:

```
unit + map + flatten
unit + flatmap
unit + compose
```

Since monad is an extension of the applicative functor, it must be possible to implement any applicative operations using any monadic operations.
We can demonstrate that by implementing applicative's `apply + product` using monad's `map + flatten` (we won't be needing `unit`).

Let's say we have the following definition of a monad in Scala (we agreed to omit `unit`):

```
trait Monad[F[_]] {
  def map[A, B](fa: F[A], f: A => B): F[B] = ???
  def flatten[A](fa: F[F[A]]): F[A] = ???
}
```

Applicative's methods can then be implemented as:

```
trait Monad2[F[_]] extends Monad[F] {

  def apply[A, B](fa: F[A], fab: F[A => B]): F[B] = 
    flatten(map(fab, (f: A => B) => map(fa, f)))

  def product[A, B](fa: F[A], fb: F[B]): F[(A, B)] = 
    flatten(map(fa, (a: A) => map(fb, (b: B) => (a,b))))
}
```

Here's an example of using `apply` with a curried function, using `List` for simplicity.

```
def apply[A, B](list: List[A], f: List[A => B]): List[B] = f.flatMap(f => list.map(f))

val curriedF = (a: Int) => (b: Int) => (c: Int) => a + b + c

val result1 = apply(List(1), List(curriedF))  
val result2 = apply(List(2), result1)  
apply(List(3), result2) // List(6)
```

The usage is the same as in applicative case. However, there's a significant difference - if `apply` is implemented using `flatmap`, 
we are taking advantage of monad's power to chain things into series. Applicative functor's `apply` and `product` lack this ability.

Let's show this difference in practice. Since we were working with `apply` in the previous example, let's take `product` now. 
We can provide two different implementations: one using monadic functions, and another one in standard applicative fashion (we can use standard Scala's `zip`):

```
// Future stuff
import scala.concurrent.{Await, Future}  
import scala.concurrent.duration._  
import scala.concurrent.ExecutionContext.Implicits.global

// Monad  
def serialProduct[A, B](f1: => Future[A], f2: => Future[B]): Future[(A, B)] = 
  f1.flatMap(a => f2.map(b => (a, b)))

// Applicative  
def parallelProduct[A, B](f1: => Future[A], f2: => Future[B]): Future[(A, B)] = 
  f1 zip f2
```

Note that both are taking their parameters by-name instead of by-value in order to prevent futures from executing as soon as they are passed.

Let's create the futures:
```
def first = Future { println("first"); Thread.sleep(2000); 1 }
def second = Future { println("second"); Thread.sleep(2000); 2 }
```
Using serial product, we get:
```
val result1 = serialProduct(first, second).map { case (a, b) => a + b }
Await.result(result1, 10 seconds)
// prints "first", then two seconds later "second"
```
Using parallel product, we get:
```
val result2 = parallelProduct(first, second).map { case (a, b) => a + b }
Await.result(result2, 10 seconds)
// performs in parallel; order of printing is indeterministic
```

Monad as a data structure could have methods `apply` and `product` exposed in its API, but it usually doesn't.
If you need those operations on some type `T`, your code should restrict `T` to the `Applicative` type class, following the "rule of least power".
However, it is common to end up working with monads in conjunction with applicatives, in which case it can be tedious to juggle between the two.
In that case, some libraries also provide the "bridge" type class (in Cats it's intuitively called [Parallel](https://typelevel.org/cats/typeclasses/parallel.html)) 
which abstracts over `Monad` type class by providing it with parallel applicative functionality.