# Theoretical Sorting

A Computer Science researcher claims to have come up with a sorting algorithm
that can sort arbitrary elements in $O(n)$ time based on comparisons of two
elements at a time. This would be asymptotically faster than any known general
sorting algorithm. The algorithm itself is proprietary and will be sold by a
company.

How would you verify this claim? You may assume that you have access to a
black-box implementation of the sorting algorithm, i.e. you cannot examine the
source code, but you can use it to sort any list you like. Explain in detail
your method for investigating whether X is correct, including any expected
results you would get.

Also give a theoretical argument for why X could or could not be correct, based
on the complexity of the general sorting problem we covered in class.

Add your answers to this markdown file.

---

Answer:

I guess to start I would test this function on very large arrays to see if the runtime indeed follows linear growth. As is understood in Computer Science, however, this should not happen for a comparison-based sorting algorithm.

I would also need to devise some sort of experiment to determine that the algorithm is indeed making comparisons of elements to other elements to order the array. As far as how to do this (I'm not sure if JavaScript has the capability for this), but I would probably use C++ or something and make a class for array elements and overload the comparison operators, so that a counter is incremented whenever they are used. If the counter changed at all, then there are obviously comparisons being made.

As far as the second part of this question, I am going to analyze the decision tree model like we did in class. In this model, each parent node represents a decision (comparison operation). For any array, there are $n!$ possible orderings or permutations that can be a result of some certain combination of individual comparison results. This is the number of leaves in the tree.

A key property of binary trees like this is that the height of the tree is $h \ge \log_2(l)$, where l is the number of leaves in the tree. Therefore, the decision tree must have a minimum height of $\log_2(n!)$. This is the shortest possible path to any permutation of the array, and in the best case scenario, that is the sorted one. This is approximated using Stirling's approximation, and is approximately equal to $n\log(n)$.

Therefore, it is impossible that the mystery sorting function actually has a linear runtime complexity if it is comparison-based.

I tried using a graph to model comparisons between elements, where each node was an element, and each of them had a two-way edge representing a comparison between the two edges. Since each two-way edge only needs to be looked at once (the order in which elements are compared doesn't matter), and I want to count all possible pairs of nodes, that means there are a total of $\binom{n}{2} = \frac{n!}{2!(n-2)!} = \frac{n(n-1)(n-2)!}{2(n-2)!} = \frac{n(n-1)}{2}$ connections (comparisons) between nodes (elements in the array). Unfortunately, this doesn't at all resemble the value $log_2(n!)$.

I think the disparity between these values and models is that the decision tree is able to distinguish between unique permutations of the input array and the combination of comparison results that had to occur to result in that permutation, whereas the graph is not. The graph shows the maximum number of comparisons between elements, but that doesn't say much with regards to sorting.

---

**I certify that I have listed all sources used to complete this exercise, including the use
of any Large Language Models. All of the work is my own, except where stated
otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is
suspected, charges may be filed against me without prior notice.**
