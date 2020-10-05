给定一个整数矩阵. 找出矩阵中的最长连续上升子序列, 返回它的长度.
最长连续上升子序列可以从任意位置开始, 向上/下/左/右移动.

样例：
输入: 
    [
      [1, 2, 3, 4, 5],
      [16,17,24,23,6],
      [15,18,25,22,7],
      [14,19,20,21,8],
      [13,12,11,10,9]
    ]
输出: 25
解释: 1 -> 2 -> 3 -> 4 -> 5 -> ... -> 25

***
通过dp数组记录某个点的最长上升子序列，防止重复搜索

```Java
public class Solution {

    int[][] dp;
    int n, m;

    public int longestContinuousIncreasingSubsequence2(int[][] A) {
        if (A.length == 0) {
            return 0;
        }

        n = A.length;
        m = A[0].length;
        int ans = 0;
        dp = new int[n][m]; // dp[i][j] means the longest continuous increasing path from (i,j)
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                dp[i][j] = -1; // dp[i][j] has not been calculated yet
            }
        }

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                search(i, j, A);
                ans = Math.max(ans, dp[i][j]);
            }
        }

        return ans;
    }

    int[] dx = { 1, -1, 0, 0 };
    int[] dy = { 0, 0, 1, -1 };

    // dfs
    void search(int x, int y, int[][] A) {
        if (dp[x][y] != -1) { // if dp[i][j] has been calculated, return directly
            return;
        }

        int nx, ny;
        dp[x][y] = 1;
        for (int i = 0; i < 4; ++i) {
            nx = x + dx[i];
            ny = y + dy[i];
            if (nx >= 0 && nx < n && ny >= 0 && ny < m) {
                if (A[nx][ny] > A[x][y]) {
                    search(nx, ny, A); // dp[nx][ny] must be calcuted
                    dp[x][y] = Math.max(dp[x][y], dp[nx][ny] + 1);
                }
            }
        }
    }
}
```