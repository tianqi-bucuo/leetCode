给定 n 个不同的正整数，整数 k（k <= n）以及一个目标数字 target。　
在这 n 个数里面找出 k 个数，使得这 k 个数的和等于目标数字，求问有多少种方案？

***

dp[i][j][k]:前i个数里选j个和为k的方案数。

```Java
public int  kSum(int A[], int k, int target) {
    int n = A.length;
    int[][][] f = new int[n + 1][k + 1][target + 1];
    for (int i = 0; i < n + 1; i++) {
        f[i][0][0] = 1;
    }
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= k && j <= i; j++) {
            for (int t = 1; t <= target; t++) {
                f[i][j][t] = 0;
                if (t >= A[i - 1]) {
                    f[i][j][t] = f[i - 1][j - 1][t - A[i - 1]];
                }
                f[i][j][t] += f[i - 1][j][t];
            } 
        } 
    }
    return f[n][k][target];
}
```