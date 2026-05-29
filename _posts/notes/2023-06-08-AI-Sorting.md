---
layout: post
title: AI just found a new sorting algorithm (or did it?)
---

Yesterday, DeepMind [announced](https://www.nature.com/articles/s41586-023-06004-9) that their AI 
(more specifically DRL) managed to find alternative sorting
algorithms which outperform current state-of-the-art.

As it turns out, there was no actual new sorting algorithm invented. But it's still
an interesting finding. Basically what they did was, they focused on so-called "small sorting algorithms"
(usually 2-4 items), both of fixed (also known as [sorting networks](https://en.wikipedia.org/wiki/Sorting_network)) and variable length.

Each algorithm was represented as an assembly program, and the AI played a self-reinforcing single player game of
"shuffle the assembly instructions around until a more performant algorithm is found" (e.g. one
that uses fewer commands). We went from inventing a new sorting algorithm, to finding
architecture-specific assembly code micro-optimisations. Still interesting stuff though!

Here are some examples of the improvements AI found.

First, we're looking at `VarSort4` - algorithm for sorting variable length arrays up to four elements big.
Old high-level algorithm looked like this (in pseudocode):
```
if (s.length == 4) sort4(s)
else if (s.length == 3) sort3(s)
else if (s.length == 2) sort2(s)
return s
```

AI-improved algorithm looks like this:
```
if (s.length == 2) sort2(s)
else {
  sort3(s)
  if (s.length == 4) insert_sorted(s[3], s)
}
return s
```

where `insert_sorted` is a simple single-step insertion sort for putting the fourth element
into its right location within an already sorted three-element array (done in the previous line).

Here's another example:

<img src="../images/sorting_algo.png" class="img-responsive">

Without going into too much detail, it figured out that it can perform a simpler `min(A, B)` 
instead of `min(A, B, C)` because at that point `B <= C` is guaranteed. Feel free to verify it.

So it's not the sorting algorithm itself that was improved. It's the 
underlying implementation of it. Actually, this AI model knows nothing about sorting. It might
as well have been given an assembly implementation of a sudoku solver. As long as the reward
function is defined correctly, it can shuffle the instructions around until it finds
a shorter version that achieves the same solution.

DeepMind is awesome,
but sometimes they tend to overhype their findings. 
We managed to squeeze some extra juice out of current LLVM C++ small sort implementations,
but we're still far away from asking the AI to come up with a meaningful improvement to
some sorting algorithm itself (not its implementation).
Let alone to come up with a completely novel sorting algorithm that outperforms existing ones.

Doesn't mean it won't happen some day though!