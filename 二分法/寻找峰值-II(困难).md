给定一个整数矩阵 A, 它有如下特性:

- 相邻的整数不同
- 矩阵有 n 行 m 列。
- 对于所有的 i < n, 都有 A[i][0] < A[i][1] && A[i][m - 2] > A[i][m - 1]
- 对于所有的 j < m, 都有 A[0][j] < A[1][j] && A[n - 2][j] > A[n - 1][j]

我们定义一个位置 [i,j] 是峰值, 当且仅当它满足:

```
A[i][j] > A[i + 1][j] && A[i][j] > A[i - 1][j] && A[i][j] > A[i][j + 1] && A[i][j] > A[i][j - 1]
```

***

```Java
class Solution {
    public List<Integer> findPeakII(int[][] A) {
        // write your code here
        List<Integer> result = new ArrayList<>();
        if (A == null || A.length == 0 || A[0].length == 0){
            return result;
        }
        
        int startRow = 1, endRow = A.length - 2;
        while (startRow + 1 < endRow){
            int midRow = startRow + (endRow - startRow) / 2;
            int maxCol = findMaxCol(A[midRow]);
            if (A[midRow][maxCol] > A[midRow - 1][maxCol] && A[midRow][maxCol] > A[midRow + 1][maxCol]){
                result.add(midRow);
                result.add(maxCol);
                return result;
            }
            if (A[midRow - 1][maxCol] > A[midRow + 1][maxCol]){
                endRow = midRow - 1;
            } else {
                startRow = midRow + 1;
            }
        }
        
        int maxCol = findMaxCol(A[startRow]);
        if (A[startRow][maxCol] > A[startRow - 1][maxCol] && A[startRow][maxCol] > A[startRow + 1][maxCol]){
            result.add(startRow);
            result.add(maxCol);
            return result;
        }
        maxCol = findMaxCol(A[endRow]);
        result.add(endRow);
        result.add(maxCol);
        return result;
    }
    
    private int findMaxCol(int[] arr){
        int result = 0;
        
        for (int i = 1; i < arr.length; i++){
            if (arr[i] > arr[result]){
                result = i;
            }
        }
        
        return result;
    }
}
```