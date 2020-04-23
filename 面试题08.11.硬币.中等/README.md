# 面试题 08.11. 硬币
### 题目：

硬币。给定数量不限的硬币，币值为25分、10分、5分和1分，编写代码计算n分有几种表示法。(结果可能会很大，你需要将结果模上1000000007)

#### 示例：

> 输入: n = 5
>  输出：2
>  解释: 有两种方式可以凑成总金额:
> ​	5=5
> ​	5=1+1+1+1+1

#### 示例2：

>  输入: n = 10
>  输出：4
>  解释: 有四种方式可以凑成总金额:
> ​	10=10
> ​	10=5+5
> ​	10=5+1+1+1+1+1
> ​	10=1+1+1+1+1+1+1+1+1+1

------



### 自己的解释

使用动态规划

动态规划解释：<https://www.zhihu.com/question/23995189>

#### 代码示例

````javascript
 /**
 * @param {number} n
 * @return {number}
 */
var waysToChange = function(n) {
  if(n===0) return 0;
  var coins = [1,5,10,25];
  var dp = new Array(n+1);
  dp[0] = 1;
  for(let i=1;i<=n;i++){
    dp[i] = 0
  }
  for(let i=0;i<4;i++){
    for(let j=1;j<=n;j++){
      if(j-coins[i]>=0){
        dp[j] += dp[j-coins[i]]
      }
    }
  }
  return dp[n]%1000000007
};
    console.log(waysToChange(5))
````

#### 运行情况

执行用时 :80 ms, 在所有 JavaScript 提交中击败了92.50%的用户

内存消耗 :63.5 MB, 在所有 JavaScript 提交中击败了100.00%的用户