# GGSIPU – UNIT III ASSIGNMENT - SHREYA SAINI

## SECTION A – Short Theory [15 Marks]

**1) DP essentials**
- **Optimal substructure:** optimal solution to problem contains optimal solutions to subproblems.  
- **Overlapping subproblems:** subproblems recur many times (can be cached).  
- **DP table / memoization:** store subproblem results for reuse.  

**2) DP vs Divide & Conquer** 
- **Subproblem overlap:** DP exploits overlap by reusing results; D&C usually has disjoint subproblems (e.g., quicksort).  
- **Reuse / caching:** DP uses memoization/tabulation; D&C recomputes unless explicitly memoized.  
- **Examples:** DP — Fibonacci with memo; D&C — mergesort/quicksort.

**3) Principle of optimality** 
- **Definition:** If an optimal solution to a problem contains substructures, those substructures must themselves be optimal.  
- **Example:** Shortest path in a weighted graph (e.g., Dijkstra) satisfies this.

**4) Memoization** vs **Tabulation**
- **Memoization:** top-down recursion + cache results on first compute.  
- **Tabulation:** bottom-up fill of a table iteratively; no recursion.

**5) Branch and Bound idea** 
- Branch and Bound systematically explores search tree nodes, using **bounds** to prune subtrees that cannot contain better solutions.  
- A tight upper/lower bound reduces explored nodes and speeds search.

---

## SECTION B – Algorithms & Recurrences [15 Marks]

**6) Matrix Chain Multiplication** (A₁:5×4, A₂:4×6, A₃:6×2, A₄:2×7)

a) **Recurrence & base** 

Let p = [5,4,6,2,7] where Ai is p[i-1] x p[i].
m[i,i] = 0 for all i.
For i < j:
m[i,j] = min_{i ≤ k < j} { m[i,k] + m[k+1,j] + p[i-1]*p[k]*p[j] }.

b) Minimum Scalar Multiplications :
158

**7) Longest Common Subsequence (X="ABCDGH", Y="AEDFHR")**

a) Recurrence & Base

LCS(i,0) = 0 for all i; LCS(0,j)=0 for all j.
If X[i]==Y[j]: LCS(i,j) = 1 + LCS(i-1,j-1)
Else: LCS(i,j) = max( LCS(i-1,j), LCS(i,j-1) )


b) LCS length :
3

**8) Optimal Binary Search Tree (keys: 10,20,30; p: 0.4,0.3,0.3; assume q=0)**

a) w[i,j] and e[i,j] formulations with base

Let p[1..n] be key probabilities, q[0..n] be dummy key probs (here q = 0).
Base:
for i = 1..n+1:
  e[i,i-1] = q[i-1]
  w[i,i-1] = q[i-1]
For i ≤ j:
  w[i,j] = w[i,j-1] + p[j] + q[j]
  e[i,j] = min_{r = i..j} { e[i,r-1] + e[r+1,j] + w[i,j] }


b) Minimum expected search cost :
1.7

**9) 0/1 Knapsack – Branch & Bound (W=5; w={2,3,4,5}, p={3,4,5,6})**

a) Fractional upper bound formula 

Sort remaining items by profit/weight (p_i/w_i) descending. Let remaining capacity = R. Upper bound = current_value + sum of full profits of items that fit + fraction of next item to exactly fill R. Formally:

UB = v + ∑_{items k fully fitting into R} p_k + p_j * (R - ∑ weights of fully taken)/w_j


(where j is the first item partially taken).

b) Level-0 and Level-1 nodes (v,w,ub)

Compute ratios p/w: item1=1.5, item2≈1.333, item3=1.25, item4=1.2. (Greedy order: 1,2,3,4)

Level-0 (root): include nothing yet → (v=0, w=0, ub=7) (capacity 5 filled fractionally: item1 (2,3) + item2 (3,4) → ub = 3+4 = 7).

Level-1 include item1: (v=3, w=2, ub=7) (after including item1, capacity 3 → item2 fits; ub stays 7).

Level-1 exclude item1: (v=0, w=0, ub=7) (same fractional fill as root).

(These nodes show v = accumulated profit, w = accumulated weight, ub = fractional upper bound.)

**10) TSP – Dynamic Programming (Held–Karp)**

a) Recurrence and final answer expression

Let cities be {1..n}, start at 1. For subset S ⊆ {2..n} and j ∈ S:
C[S, j] = min_{i ∈ S, i ≠ j} { C[S \ {j}, i] + d[i][j] }.

Final answer: min_{j ∈ {2..n}} { C[{2..n}, j] + d[j][1] }.


b) Initialize base entries C[{k},k] for k=2..4

C[{2},2] = d[1,2]
C[{3},3] = d[1,3]
C[{4},4] = d[1,4]
