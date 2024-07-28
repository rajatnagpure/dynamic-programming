
### Example Problems
- **Climbing Stairs**: Given `n` stairs, each time you can climb 1 or 2 steps. In how many distinct ways can you climb to the top?
    - **Logic**: The problem can be solved by considering the number of ways to reach the current step from the previous one or two steps. Use dynamic programming to store the results of these subproblems.
    - **Top-Down (Memoization)**
        - **Function Signature**: `int climbStairs(int n)`
        - **Base Case**: `if (n <= 1) return 1;`
        - **Recursion Call**:
          ```python
          return climbStairs(n-1) + climbStairs(n-2);
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n+1]`
        - **Base Case**: Initialize `dp[0] = 1` and `dp[1] = 1`.
        - **Iteration Call**:
          ```python
          for (int i = 2; i <= n; i++) {
              dp[i] = dp[i-1] + dp[i-2];
          ```

- **House Robber**: Given an array of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
    - **Logic**: The problem can be solved by deciding whether to rob the current house or skip it. If you rob it, you can't rob the previous house.
    - **Top-Down (Memoization)**
        - **Function Signature**: `int rob(int[] nums, int n)`
        - **Base Case**: `if (n < 0) return 0;`
        - **Recursion Call**:
          ```python
          return max(nums[n] + rob(nums, n-2), rob(nums, n-1));
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n]`
        - **Base Case**: Initialize `dp[0] = nums[0]`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i < n; i++) {
              dp[i] = max(nums[i] + (i > 1 ? dp[i-2] : 0), dp[i-1]);
          ```

- **Coin Change**: Given a set of coin denominations and an amount, find the minimum number of coins needed to make the amount.
    - **Logic**: The problem can be solved by considering the minimum coins needed for each amount up to the target amount. Dynamic programming helps in storing the results of these subproblems.
    - **Top-Down (Memoization)**
        - **Function Signature**: `int coinChange(int[] coins, int amount)`
        - **Base Case**: `if (amount == 0) return 0;`
        - **Recursion Call**:
          ```python
          int res = Integer.MAX_VALUE;
          for (int coin : coins) {
              if (amount >= coin) {
                  int sub_res = coinChange(coins, amount - coin);
                  if (sub_res != Integer.MAX_VALUE) {
                      res = Math.min(res, sub_res + 1);
                  }
              }
          }
          return res;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[amount + 1]`
        - **Base Case**: Initialize `dp[0] = 0`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i <= amount; i++) {
              dp[i] = Integer.MAX_VALUE;
              for (int coin : coins) {
                  if (i >= coin && dp[i - coin] != Integer.MAX_VALUE) {
                      dp[i] = Math.min(dp[i], dp[i - coin] + 1);
          ```

- **Edit Distance**: Given two strings, find the minimum number of operations required to convert one string into the other.
    - **Logic**: The problem can be solved by considering the cost of inserting, deleting, or replacing characters. Dynamic programming helps in storing the results of these subproblems.
    - **Top-Down (Memoization)**
        - **Function Signature**: `int editDistance(String s1, String s2, int m, int n)`
        - **Base Case**: `if (m == 0) return n; if (n == 0) return m;`
        - **Recursion Call**:
          ```python
          if (s1.charAt(m-1) == s2.charAt(n-1))
              return editDistance(s1, s2, m-1, n-1);
          else
              return 1 + Math.min(editDistance(s1, s2, m, n-1), // Insert
                                  Math.min(editDistance(s1, s2, m-1, n), // Remove
                                           editDistance(s1, s2, m-1, n-1))); // Replace
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[m+1][n+1]`
        - **Base Case**: Initialize `dp[i][0] = i` and `dp[0][j] = j` for all `i` and `j`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i <= m; i++) {
              for (int j = 1; j <= n; j++) {
                  if (s1.charAt(i-1) == s2.charAt(j-1))
                      dp[i][j] = dp[i-1][j-1];
                  else
                      dp[i][j] = 1 + Math.min(dp[i][j-1], // Insert
                                              Math.min(dp[i-1][j], // Remove
                                                       dp[i-1][j-1])); // Replace
          ```


- **Combination Sum IV**: Given an array of distinct integers `nums` and a target integer `target`, return the number of possible combinations that add up to `target`.
    - **Logic**: The problem can be solved by considering all possible ways to reach the target using the given numbers. Dynamic programming helps in storing the results of subproblems to avoid recomputation.
    - **Top-Down (Memoization)**
        - **Function Signature**: `int combinationSum4(int[] nums, int target)`
        - **Base Case**: `if (target == 0) return 1;`
        - **Recursion Call**:
          ```python
          int res = 0;
          for (int num : nums) {
              if (target >= num) {
                  res += combinationSum4(nums, target - num);
              }
          }
          return res;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[target + 1]`
        - **Base Case**: Initialize `dp[0] = 1`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i <= target; i++) {
              for (int num : nums) {
                  if (i >= num) {
                      dp[i] += dp[i - num];
                  }
              }
          ```

- **Word Break**: Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.
    - **Logic**: The problem can be solved by checking if the current prefix of the string can be formed using words from the dictionary. Use dynamic programming to store the results of these subproblems.
    - **Top-Down (Memoization)**
        - **Function Signature**: `boolean wordBreak(String s, List<String> wordDict)`
        - **Base Case**: `if (s.isEmpty()) return true;`
        - **Recursion Call**:
          ```python
          for (String word : wordDict) {
              if (s.startsWith(word)) {
                  if (wordBreak(s.substring(word.length()), wordDict)) {
                      return true;
                  }
              }
          }
          return false;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[s.length() + 1]`
        - **Base Case**: Initialize `dp[0] = true`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i <= s.length(); i++) {
              for (String word : wordDict) {
                  if (i >= word.length() && s.substring(i - word.length(), i).equals(word)) {
                      dp[i] = dp[i] || dp[i - word.length()];
                  }
              }
          ```

- **Word Break II**: Given a string `s` and a dictionary of strings `wordDict`, return all possible sentences where `s` can be segmented into a space-separated sequence of one or more dictionary words.
    - **Logic**: The problem can be solved by checking if the current prefix of the string can be formed using words from the dictionary. Use dynamic programming to store the results of these subproblems and construct the sentences.
    - **Top-Down (Memoization)**
        - **Function Signature**: `List<String> wordBreak(String s, List<String> wordDict)`
        - **Base Case**: `if (s.isEmpty()) return Arrays.asList("");`
        - **Recursion Call**:
          ```python
          List<String> result = new ArrayList<>();
          for (String word : wordDict) {
              if (s.startsWith(word)) {
                  List<String> sublist = wordBreak(s.substring(word.length()), wordDict);
                  for (String sub : sublist) {
                      result.add(word + (sub.isEmpty() ? "" : " ") + sub);
                  }
              }
          }
          return result;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[s.length() + 1]`
        - **Base Case**: Initialize `dp[0] = Arrays.asList("");`
        - **Iteration Call**:
          ```python
          for (int i = 1; i <= s.length(); i++) {
              List<String> list = new ArrayList<>();
              for (String word : wordDict) {
                  if (i >= word.length() && s.substring(i - word.length(), i).equals(word)) {
                      for (String sub : dp[i - word.length()]) {
                          list.add(sub + (sub.isEmpty() ? "" : " ") + word);
                      }
                  }
              }
              dp[i] = list;
          ```

- **Unique Binary Search Trees**: Given an integer `n`, return the number of structurally unique BSTs (binary search trees) that store values 1 ... n.
    - **Logic**: The problem can be solved by considering each number as the root and calculating the number of unique BSTs formed by the left and right subtrees.
    - **Top-Down (Memoization)**
        - **Function Signature**: `int numTrees(int n)`
        - **Base Case**: `if (n <= 1) return 1;`
        - **Recursion Call**:
          ```python
          int sum = 0;
          for (int i = 1; i <= n; i++) {
              sum += numTrees(i - 1) * numTrees(n - i);
          }
          return sum;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n + 1]`
        - **Base Case**: Initialize `dp[0] = 1` and `dp[1] = 1`.
        - **Iteration Call**:
          ```python
          for (int i = 2; i <= n; i++) {
              for (int j = 1; j <= i; j++) {
                  dp[i] += dp[j - 1] * dp[i - j];
              }
          ```

- **Ugly Number II**: Given an integer `n`, return the nth ugly number. Ugly numbers are positive numbers whose prime factors only include 2, 3, and 5.
    - **Logic**: The problem can be solved by generating ugly numbers in sequence using dynamic programming to store the results of these subproblems.
    - **Top-Down (Memoization)**
        - **Function Signature**: `int nthUglyNumber(int n)`
        - **Base Case**: Initialize `uglyNumbers[0] = 1`.
        - **Recursion Call**:
          ```python
          int nextUgly = min(2 * uglyNumbers[index2], 3 * uglyNumbers[index3], 5 * uglyNumbers[index5]);
          if (nextUgly == 2 * uglyNumbers[index2]) index2++;
          if (nextUgly == 3 * uglyNumbers[index3]) index3++;
          if (nextUgly == 5 * uglyNumbers[index5]) index5++;
          uglyNumbers[i] = nextUgly;
          ```
    - **Bottom-Up (Tabulation)**
        - **Dimensions**: `dp[n]`
        - **Base Case**: Initialize `dp[0] = 1`.
        - **Iteration Call**:
          ```python
          for (int i = 1; i < n; i++) {
              int nextUgly = Math.min(2 * dp[index2], Math.min(3 * dp[index3], 5 * dp[index5]));
              dp[i] = nextUgly;
              if (nextUgly == 2 * dp[index2]) index2++;
              if (nextUgly == 3 * dp[index3]) index3++;
              if (nextUgly == 5 * dp[index5]) index5++;
          ```

### Example Problems

#### Rod Cutting - Unbounded Knapsack
The Rod Cutting problem is a classic example of the unbounded knapsack problem, where the goal is to maximize the profit by cutting a rod of length `n` into smaller pieces of given lengths and associated prices.
- **Logic**: We can cut the rod into any number of pieces of given lengths. For each length, we decide whether to cut it or not, and we try to maximize the profit.
- **Top-Down (Memoization)**
  - **Function Signature**: `int rodCutting(int[] lengths, int[] prices, int n)`
  - **Base Case**: `if (n == 0) return 0;`
  - **Recursion Call**:
    ```python
    int maxVal = 0;
    for (int i = 0; i < lengths.length; i++) {
        if (lengths[i] <= n) {
            maxVal = Math.max(maxVal, prices[i] + rodCutting(lengths, prices, n - lengths[i]));
        }
    }
    return maxVal;
    ```
- **Bottom-Up (Tabulation)**
  - **Dimensions**: `dp[n+1]`
  - **Base Case**: Initialize `dp[0] = 0`.
  - **Iteration Call**:
    ```python
    for (int i = 1; i <= n; i++) {
        for (int j = 0; j < lengths.length; j++) {
            if (lengths[j] <= i) {
                dp[i] = Math.max(dp[i], dp[i - lengths[j]] + prices[j]);
            }
        }
    }
    ```

#### Decode Ways - DP on Strings (Similar to LCS)
The Decode Ways problem involves decoding a string of digits into letters, where each digit or pair of digits corresponds to a letter.
- **Logic**: Each digit can be decoded individually, and some pairs of digits can also be decoded together. Use dynamic programming to store the number of ways to decode substrings.
- **Top-Down (Memoization)**
  - **Function Signature**: `int numDecodings(String s)`
  - **Base Case**: `if (s.isEmpty()) return 1; if (s.charAt(0) == '0') return 0;`
  - **Recursion Call**:
    ```python
    if (s.length() == 1) return 1;
    int count = numDecodings(s.substring(1));
    if (Integer.parseInt(s.substring(0, 2)) <= 26) {
        count += numDecodings(s.substring(2));
    }
    return count;
    ```
- **Bottom-Up (Tabulation)**
  - **Dimensions**: `dp[s.length() + 1]`
  - **Base Case**: Initialize `dp[0] = 1` and `dp[1] = s.charAt(0) == '0' ? 0 : 1`.
  - **Iteration Call**:
    ```python
    for (int i = 2; i <= s.length(); i++) {
        if (s.charAt(i - 1) != '0') {
            dp[i] += dp[i - 1];
        }
        int twoDigit = Integer.parseInt(s.substring(i - 2, i));
        if (twoDigit >= 10 && twoDigit <= 26) {
            dp[i] += dp[i - 2];
        }
    }
    ```

#### Unique Paths - DP on Grid
The Unique Paths problem involves finding the number of unique paths from the top-left corner to the bottom-right corner of a grid.
- **Logic**: At each cell, the number of ways to get there is the sum of the number of ways to get to the cell directly above and the cell directly to the left.
- **Top-Down (Memoization)**
  - **Function Signature**: `int uniquePaths(int m, int n)`
  - **Base Case**: `if (m == 1 || n == 1) return 1;`
  - **Recursion Call**:
    ```python
    return uniquePaths(m - 1, n) + uniquePaths(m, n - 1);
    ```
- **Bottom-Up (Tabulation)**
  - **Dimensions**: `dp[m][n]`
  - **Base Case**: Initialize `dp[i][0] = 1` and `dp[0][j] = 1` for all `i` and `j`.
  - **Iteration Call**:
    ```python
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }
    ```

#### Minimum Egg Drops - DP on 2D Grid (Egg Drop Problem)
The Egg Drop problem involves determining the minimum number of trials needed to find the critical floor from which an egg can be dropped without breaking.
- **Logic**: Use a dynamic programming table to store the results of subproblems. For each floor and egg, consider the worst-case scenario of the egg breaking or not breaking.
- **Top-Down (Memoization)**
  - **Function Signature**: `int eggDrop(int k, int n)`
  - **Base Case**: `if (n == 0 || n == 1) return n; if (k == 1) return n;`
  - **Recursion Call**:
    ```python
    int minTrials = Integer.MAX_VALUE;
    for (int i = 1; i <= n; i++) {
        int res = 1 + Math.max(eggDrop(k - 1, i - 1), eggDrop(k, n - i));
        minTrials = Math.min(minTrials, res);
    }
    return minTrials;
    ```
- **Bottom-Up (Tabulation)**
  - **Dimensions**: `dp[k+1][n+1]`
  - **Base Case**: Initialize `dp[i][0] = 0` and `dp[i][1] = 1` for all `i`.
  - **Iteration Call**:
    ```python
    for (int i = 1; i <= k; i++) {
        for (int j = 2; j <= n; j++) {
            dp[i][j] = Integer.MAX_VALUE;
            for (int x = 1; x <= j; x++) {
                int res = 1 + Math.max(dp[i - 1][x - 1], dp[i][j - x]);
                dp[i][j] = Math.min(dp[i][j], res);
            }
        }
    }
    ```

#### Word Break II - Unbounded Knapsack (Similar to Word Break I)
The Word Break II problem involves finding all possible sentences where a string `s` can be segmented into a space-separated sequence of one or more dictionary words.
- **Logic**: Similar to Word Break I, but we need to store all possible sentences rather than just a boolean result.
- **Top-Down (Memoization)**
  - **Function Signature**: `List<String> wordBreakII(String s, List<String> wordDict)`
  - **Base Case**: `if (s.isEmpty()) return Arrays.asList("");`
  - **Recursion Call**:
    ```python
    List<String> result = new ArrayList<>();
    for (String word : wordDict) {
        if (s.startsWith(word)) {
            List<String> sublist = wordBreakII(s.substring(word.length()), wordDict);
            for (String sub : sublist) {
                result.add(word + (sub.isEmpty() ? "" : " ") + sub);
            }
        }
    }
    return result;
    ```
- **Bottom-Up (Tabulation)**
  - **Dimensions**: `dp[s.length() + 1]`
  - **Base Case**: Initialize `dp[0] = Arrays.asList("");`
  - **Iteration Call**:
    ```python
    for (int i = 1; i <= s.length(); i++) {
        List<String> list = new ArrayList<>();
        for (String word : wordDict) {
            if (i >= word.length() && s.substring(i - word.length(), i).equals(word)) {
                for (String sub : dp[i - word.length()]) {
                    list.add(sub + (sub.isEmpty() ? "" : " ") + word);
                }
            }
        }
        dp[i] = list;
    }
    ```

#### Best Time to Buy and Sell Stock III - DP on Stock Problems
The Best Time to Buy and Sell Stock III problem involves finding the maximum profit with at most two transactions.
- **Logic**: Use dynamic programming to track the maximum profit up to each day with at most one and two transactions.
- **Top-Down (Memoization)**
  - **Function Signature**: `int maxProfit(int[] prices)`
  - **Base Case**: `if (prices.length == 0) return 0;`
  - **Recursion Call**:
    ```python
    int[] leftProfits = new int[prices.length];
    int[] rightProfits = new int[prices.length];
    int minPrice = prices[0];
    for (int i = 1; i < prices.length; i++) {
        leftProfits[i] = Math.max(leftProfits[i - 1], prices[i] - minPrice);
        minPrice = Math.min(minPrice, prices[i]);
   
    int maxPrice = prices[prices.length - 1];
    for (int i = prices.length - 2; i >= 0; i--) {
        rightProfits[i] = Math.max(rightProfits[i + 1], maxPrice - prices[i]);
        maxPrice = Math.max(maxPrice, prices[i]);
    }
    int maxProfit = 0;
    for (int i = 0; i < prices.length; i++) {
        maxProfit = Math.max(maxProfit, leftProfits[i] + rightProfits[i]);
    }
    return maxProfit;
    ```

#### Best Time to Buy and Sell Stock IV - DP on Stock Problems
The Best Time to Buy and Sell Stock IV problem involves finding the maximum profit with at most `k` transactions.
- **Logic**: Use dynamic programming to track the maximum profit up to each day with at most `k` transactions.
- **Top-Down (Memoization)**
  - **Function Signature**: `int maxProfit(int k, int[] prices)`
  - **Base Case**: `if (prices.length == 0) return 0;`
  - **Recursion Call**:
    ```python
    int[][] dp = new int[k + 1][prices.length];
    for (int i = 1; i <= k; i++) {
        int maxDiff = -prices[0];
        for (int j = 1; j < prices.length; j++) {
            dp[i][j] = Math.max(dp[i][j - 1], prices[j] + maxDiff);
            maxDiff = Math.max(maxDiff, dp[i - 1][j] - prices[j]);
        }
    }
    return dp[k][prices.length - 1];
    ```

#### Regular Expression Matching - DP on Strings (Similar to LCS)
The Regular Expression Matching problem involves checking if a given string matches a pattern where '.' matches any single character and '*' matches zero or more of the preceding element.
- **Logic**: Use dynamic programming to store the results of subproblems. Consider the cases where the current characters match or where '*' is involved.
- **Top-Down (Memoization)**
  - **Function Signature**: `boolean isMatch(String s, String p)`
  - **Base Case**: `if (p.isEmpty()) return s.isEmpty();`
  - **Recursion Call**:
    ```python
    boolean firstMatch = (!s.isEmpty() && (p.charAt(0) == s.charAt(0) || p.charAt(0) == '.'));
    if (p.length() >= 2 && p.charAt(1) == '*') {
        return (isMatch(s, p.substring(2)) || (firstMatch && isMatch(s.substring(1), p)));
    } else {
        return firstMatch && isMatch(s.substring(1), p.substring(1));
    }
    ```
- **Bottom-Up (Tabulation)**
  - **Dimensions**: `dp[s.length() + 1][p.length() + 1]`
  - **Base Case**: Initialize `dp[0][0] = true`.
  - **Iteration Call**:
    ```python
    for (int i = 0; i <= s.length(); i++) {
        for (int j = 1; j <= p.length(); j++) {
            if (p.charAt(j - 1) == '*') {
                dp[i][j] = dp[i][j - 2] || (i > 0 && dp[i - 1][j] && (s.charAt(i - 1) == p.charAt(j - 2) || p.charAt(j - 2) == '.'));
            } else {
                dp[i][j] = i > 0 && dp[i - 1][j - 1] && (s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '.');
            }
        }
    }
    ```

#### Wildcard Matching - DP on Strings (Similar to LCS)
The Wildcard Matching problem involves checking if a given string matches a pattern where '?' matches any single character and '*' matches any sequence of characters (including the empty sequence).
- **Logic**: Use dynamic programming to store the results of subproblems. Consider the cases where the current characters match or where '*' is involved.
- **Top-Down (Memoization)**
  - **Function Signature**: `boolean isWildcardMatch(String s, String p)`
  - **Base Case**: `if (p.isEmpty()) return s.isEmpty();`
  - **Recursion Call**:
    ```python
    boolean firstMatch = (!s.isEmpty() && (p.charAt(0) == s.charAt(0) || p.charAt(0) == '?'));
    if (p.charAt(0) == '*') {
        return isWildcardMatch(s, p.substring(1)) || (!s.isEmpty() && isWildcardMatch(s.substring(1), p));
    } else {
        return firstMatch && isWildcardMatch(s.substring(1), p.substring(1));
    }
    ```
- **Bottom-Up (Tabulation)**
  - **Dimensions**: `dp[s.length() + 1][p.length() + 1]`
  - **Base Case**: Initialize `dp[0][0] = true`.
  - **Iteration Call**:
    ```python
    for (int i = 0; i <= s.length(); i++) {
        for (int j = 1; j <= p.length(); j++) {
            if (p.charAt(j - 1) == '*') {
                dp[i][j] = dp[i][j - 1] || (i > 0 && dp[i - 1][j]);
            } else {
                dp[i][j] = i > 0 && dp[i - 1][j - 1] && (s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '?');
            }
        }
    }
    ```


These sections cover a wide range of common dynamic programming problems. Each problem type is accompanied by a logical explanation and code snippets for both the top-down and bottom-up approaches. By studying and understanding these patterns, you can tackle a variety of dynamic programming challenges effectively.
