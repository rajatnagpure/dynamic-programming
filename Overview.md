# Dynamic Programming Questions

Below are the different types of Dynamic Programming questions. For each type, we have provided explanations on how to solve them using both top-down (memoization) and bottom-up (tabulation) approaches.

1. **0-1 Knapsack** ... 6 
2. **Unbounded Knapsack** ... 5
3. **Fibonacci** ... 7
4. **LCS (Longest Common Subsequence)** ... 15
5. **LIS (Longest Increasing Subsequence)** ... 10
6. **Kadane's Algorithm** ... 6
7. **Matrix Chain Multiplication** ... 7
8. **DP on Trees** ... 4
9. **DP on Grid** ... 14
10. **Stock** ... 6
11. **Others** ... 5

--------------

1. **0-1 Knapsack**
The 0-1 Knapsack problem involves selecting items with given weights and values to maximize the total value without exceeding a given weight capacity. Each item can be included or excluded.

    - **Logic**: The problem can be broken down into smaller subproblems where we decide whether to include or exclude each item. If we include an item, we add its value to our total and decrease the capacity by its weight. If we exclude it, we simply move to the next item. This is done recursively, and overlapping subproblems are solved using dynamic programming.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int knapsack(int[] weights, int[] values, int n, int W)`
        - **Base Case**: `if (n == 0 || W == 0) return 0;`
        - **Recursion Call**:
          ```python
          if (weights[n-1] <= W) 
              return max(values[n-1] + knapsack(weights, values, n-1, W-weights[n-1]), knapsack(weights, values, n-1, W));
          else
              return knapsack(weights, values, n-1, W);
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n+1][W+1]`
        - **Base Case**: Initialize `dp[i][0] = 0` and `dp[0][j] = 0` for all `i` and `j`.
        - **Iteration Call**:
          ```python
          for i in range(1, n+1):
              for j in range(1, W+1):
                  if weights[i-1] <= j:
                      dp[i][j] = max(values[i-1] + dp[i-1][j-weights[i-1]], dp[i-1][j]);
                  else:
                      dp[i][j] = dp[i-1][j];
          ```

2. **Unbounded Knapsack**
The Unbounded Knapsack problem is similar to the 0-1 Knapsack problem but allows an unlimited number of instances of each item.

    - **Logic**: This problem can be thought of as a variation of the 0-1 Knapsack problem where each item can be chosen multiple times. The solution involves determining the maximum value by either including an item (multiple times) or excluding it.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int unboundedKnapsack(int[] weights, int[] values, int n, int W)`
        - **Base Case**: `if (n == 0 || W == 0) return 0;`
        - **Recursion Call**:
          ```python
          if (weights[n-1] <= W)
              return max(values[n-1] + unboundedKnapsack(weights, values, n, W-weights[n-1]), unboundedKnapsack(weights, values, n-1, W));
          else
              return unboundedKnapsack(weights, values, n-1, W);
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[W+1]`
        - **Base Case**: Initialize `dp[0] = 0` for all `j`.
        - **Iteration Call**:
          ```python
          for i in range(n):
              for j in range(weights[i], W+1):
                  dp[j] = max(dp[j], dp[j-weights[i]] + values[i]);
          ```

3. **Fibonacci**
The Fibonacci sequence is a series of numbers where each number is the sum of the two preceding ones.

    - **Logic**: The problem can be solved by recursively adding the two preceding numbers to get the current number. Since the same subproblems are solved multiple times, dynamic programming helps in storing the results of these subproblems to avoid redundant calculations.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int fib(int n)`
        - **Base Case**: `if (n <= 1) return n;`
        - **Recursion Call**:
          ```python
          return fib(n-1) + fib(n-2);
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n+1]`
        - **Base Case**: Initialize `dp[0] = 0` and `dp[1] = 1`.
        - **Iteration Call**:
          ```python
          for i in range(2, n+1):
              dp[i] = dp[i-1] + dp[i-2];
          ```

4. **LCS (Longest Common Subsequence)**
The Longest Common Subsequence problem involves finding the longest subsequence that is common to two sequences.

    - **Logic**: The problem can be broken down into smaller subproblems by comparing the last characters of the two sequences. If the characters match, we include it in our solution and move to the next characters. If they don't match, we try excluding each character in turn and take the longer subsequence. Dynamic programming helps store the results of these subproblems to avoid redundant calculations.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int lcs(String s1, String s2, int m, int n)`
        - **Base Case**: `if (m == 0 || n == 0) return 0;`
        - **Recursion Call**:
          ```python
          if (s1.charAt(m-1) == s2.charAt(n-1))
              return 1 + lcs(s1, s2, m-1, n-1);
          else
              return max(lcs(s1, s2, m-1, n), lcs(s1, s2, m, n-1));
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[m+1][n+1]`
        - **Base Case**: Initialize `dp[i][0] = 0` and `dp[0][j] = 0` for all `i` and `j`.
        - **Iteration Call**:
          ```python
          for i in range(1, m+1):
              for j in range(1, n+1):
                  if (s1.charAt(i-1) == s2.charAt(j-1))
                      dp[i][j] = 1 + dp[i-1][j-1];
                  else
                      dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
          ```

5. **LIS (Longest Increasing Subsequence)**
The Longest Increasing Subsequence problem involves finding the longest subsequence that is strictly increasing.

    - **Logic**: This problem can be solved by finding all possible increasing subsequences and choosing the longest one. Dynamic programming helps by storing the results of subproblems, where the subproblem is to find the longest increasing subsequence ending at each index.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int lis(int[] arr, int n, int prev)`
        - **Base Case**: `if (n == 0) return 0;`
        - **Recursion Call**:
          ```python
          if (arr[n-1] > prev)
              return max(1 + lis(arr, n-1, arr[n-1]), lis(arr, n-1, prev));
          else
              return lis(arr, n-1, prev);
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n]`
        - **Base Case**: Initialize `dp[i] = 1` for all `i`.
        - **Iteration Call**:
          ```python
          for i in range(1, n):
              for j in range(0, i):
                  if (arr[i] > arr[j])
                      dp[i] = max(dp[i], dp[j] + 1);
          ```

6. **Kadane's Algorithm**
Kadane's Algorithm is used to find the maximum sum subarray in a given array of integers.

    - **Logic**: The algorithm works by iterating through the array and keeping track of the maximum sum subarray ending at each position. If the current element is greater than the sum of the current element and the maximum sum subarray ending at the previous position, we start a new subarray at the current element.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int kadane(int[] arr, int n)`
        - **Base Case**: `if (n ==
        - **Base Case**: `if (n == 1) return arr[0];`
        - **Recursion Call**:
          ```python
          return max(arr[n-1], arr[n-1] + kadane(arr, n-1));
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n]`
        - **Base Case**: Initialize `dp[0] = arr[0]`.
        - **Iteration Call**:
          ```python
          for i in range(1, n):
              dp[i] = max(arr[i], dp[i-1] + arr[i]);
          ```

7. **Matrix Chain Multiplication**
The Matrix Chain Multiplication problem involves finding the most efficient way to multiply a given sequence of matrices.

    - **Logic**: The problem can be broken down into smaller subproblems by considering different places to split the product. The cost of multiplying matrices depends on where the split is made. Dynamic programming helps in storing the minimum number of multiplications needed to multiply the matrices.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int matrixChain(int[] p, int i, int j)`
        - **Base Case**: `if (i == j) return 0;`
        - **Recursion Call**:
          ```python
          int minCount = Integer.MAX_VALUE;
          for (int k = i; k < j; k++) {
              int count = matrixChain(p, i, k) + matrixChain(p, k+1, j) + p[i-1]*p[k]*p[j];
              minCount = Math.min(minCount, count);
          }
          return minCount;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n][n]`
        - **Base Case**: Initialize `dp[i][i] = 0` for all `i`.
        - **Iteration Call**:
          ```python
          for (int l = 2; l < n; l++) {
              for (int i = 1; i < n - l + 1; i++) {
                  int j = i + l - 1;
                  dp[i][j] = Integer.MAX_VALUE;
                  for (int k = i; k < j; k++) {
                      dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k+1][j] + p[i-1]*p[k]*p[j]);
                  }
              }
          }
          ```

8. **DP on Trees**
Dynamic Programming on Trees involves solving problems related to tree data structures using DP techniques.

    - **Logic**: Problems on trees often require traversing the tree and solving subproblems for each subtree. By storing the results of subproblems, we avoid redundant calculations and can solve the problem efficiently.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int treeDP(TreeNode node)`
        - **Base Case**: `if (node == null) return 0;`
        - **Recursion Call**:
          ```python
          int result = 0;
          for (TreeNode child : node.children) {
              result = Math.max(result, treeDP(child));
          }
          return result;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[nodeCount]`
        - **Base Case**: Initialize `dp[node]` for all leaf nodes.
        - **Iteration Call**:
          ```python
          for (each node from bottom to top) {
              for (each child of node) {
                  dp[node] = Math.max(dp[node], dp[child]);
              }
          }
          ```

9. **DP on Grid**
Dynamic Programming on Grids involves solving problems on grid structures, such as finding the minimum path sum.

    - **Logic**: Problems on grids often require finding paths or areas with certain properties. By breaking the problem into smaller subproblems for each cell and storing the results, we can solve the overall problem efficiently.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int gridDP(int[][] grid, int m, int n)`
        - **Base Case**: `if (m == 0 && n == 0) return grid[0][0];`
        - **Recursion Call**:
          ```python
          if (m == 0) 
              return grid[0][n] + gridDP(grid, 0, n-1);
          if (n == 0) 
              return grid[m][0] + gridDP(grid, m-1, 0);
          return grid[m][n] + Math.min(gridDP(grid, m-1, n), gridDP(grid, m, n-1));
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[m+1][n+1]`
        - **Base Case**: Initialize `dp[0][0] = grid[0][0]`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i <= m; i++) {
              dp[i][0] = dp[i-1][0] + grid[i][0];
          }
          for (int j = 1; j <= n; j++) {
              dp[0][j] = dp[0][j-1] + grid[0][j];
          }
          for (int i = 1; i <= m; i++) {
              for (int j = 1; j <= n; j++) {
                  dp[i][j] = grid[i][j] + Math.min(dp[i-1][j], dp[i][j-1]);
          }
          ```

10. **Stock**
Dynamic Programming on Stock problems involves solving problems related to stock trading to maximize profit under given constraints.

    - **Logic**: Stock trading problems can be broken down into smaller subproblems by considering the decision to buy, sell, or hold at each day. By storing the results of these decisions, we can solve the problem efficiently.

    - **Top-Down (Memoization)**
        - **Function Signature**: `int maxProfit(int[] prices, int n)`
        - **Base Case**: `if (n <= 1) return 0;`
        - **Recursion Call**:
          ```python
          if (prices[n-1] > prices[n-2])
              return max(prices[n-1] - prices[n-2] + maxProfit(prices, n-2), maxProfit(prices, n-1));
          else
              return maxProfit(prices, n-1);
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n]`
        - **Base Case**: Initialize `dp[i] = 0` for all `i`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i < n; i++) {
              for (int j = 0; j < i; j++) {
                  if (prices[i] > prices[j])
                      dp[i] = Math.max(dp[i], prices[i] - prices[j] + dp[j]);
              }
          }
          ```

11. **Others**
This section includes various other dynamic programming problems.

    - **Top-Down (Memoization)**
        - **Function Signature**: Varies depending on the problem.
        - **Base Case**: Define the base case according to the problem.
        - **Recursion Call**: Recursively solve the subproblems while storing the results.
    - **Bottom-Up (Tabulation)**
        - **Dimensions
        - **Dimensions**: Varies depending on the problem.
        - **Base Case**: Initialize the base cases according to the problem.
        - **Iteration Call**: Iterate through the possible states and transitions to solve the subproblems and build up to the final solution.

This README provides a structured approach to solving various dynamic programming problems using both top-down (memoization) and bottom-up (tabulation) methods. For each problem type, it explains the function signature, base case, recursion calls for memoization, and the dimensions, base case, and iteration calls for tabulation.
