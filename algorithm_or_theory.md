# 关于分支定界(branch and bound)
## BnB是什么

Branch and bound (BB, B&B, or BnB) is an algorithm design paradigm for discrete and combinatorial optimization problems, as well as mathematical optimization. A branch-and-bound algorithm consists of a systematic enumeration of candidate solutions by means of state space search: the set of candidate solutions is thought of as forming a rooted tree with the full set at the root. 

The algorithm explores branches of this tree, which represent subsets of the solution set. Before enumerating the candidate solutions of a branch, the branch is checked against upper and lower estimated bounds on the optimal solution, and is discarded if it cannot produce a better solution than the best one found so far by the algorithm.

The algorithm depends on efficient estimation of the lower and upper bounds of regions/branches of the search space. If no bounds are available, the algorithm degenerates to an exhaustive search.

分支定界算法始终围绕着一颗搜索树进行的，我们将原问题看作搜索树的根节点，从这里出发，分支的含义就是将大的问题分割成小的问题。

大问题可以看成是搜索树的父节点，那么从大问题分割出来的小问题就是父节点的子节点了。

分支的过程就是不断给树增加子节点的过程。而定界就是在分支的过程中检查子问题的上下界，如果子问题不能产生一比当前最优解还要优的解，那么砍掉这一支。直到所有子问题都不能产生一个更优的解时，算法结束。

## 
