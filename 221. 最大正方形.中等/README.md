# 221. 最大正方形.中等
### 题目：

在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。

#### 示例：

> 输入:
>
> 10100
>
> 10111
>
> 11111
>
> 10010
>
> 输出: 4


------



### 自己的解释

先从左往右依次找到1，将它视为正方形的顶点，然后开始判断长和宽以及内部是否满足条件。



#### 代码示例

````javascript
/**
* @param {character[][]} grid
* @return {number}
*/
var maximalSquare = function(matrix) {
  if (matrix.length === 0) return 0;
  const dp = [];
  const rows = matrix.length;
  const cols = matrix[0].length;
  let max = Number.MIN_VALUE;

  for (let i = 0; i < rows + 1; i++) {
    if (i === 0) {
      dp[i] = Array(cols + 1).fill(0);
    } else {
      dp[i] = [0];
    }
  }

  for (let i = 1; i < rows + 1; i++) {
    for (let j = 1; j < cols + 1; j++) {
      if (matrix[i - 1][j - 1] === "1") {
        dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1;
        max = Math.max(max, dp[i][j]);
      } else {
        dp[i][j] = 0;
      }
    }
  }

  return max * max;
};
````

#### 运行情况

执行用时：**84 ms**

内存消耗：**41.8 MB**