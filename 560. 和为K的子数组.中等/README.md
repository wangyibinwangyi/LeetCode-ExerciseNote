# 560. 和为K的子数组.中等
### 题目：

给定一个整数数组和一个整数 **k，**你需要找到该数组中和为 **k** 的连续的子数组的个数。

#### 示例：

> 输入:nums = [1,1,1], k = 2
> 输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。

**说明 :**

1. 数组的长度为 [1, 20,000]。
2. 数组中元素的范围是 [-1000, 1000] ，且整数 **k** 的范围是 [-1e7, 1e7]。

------



### 自己的解释





#### 代码示例

````javascript
   /**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var subarraySum = function(nums, k) {
  let map = new Map();
  let sum = 0,res = 0;
  for(let key in nums){
    sum += nums[key];
    if(sum == k) res++;
    let subSum = sum - k, value = null;
    if(map.has(subSum)) res+=map.get(subSum).length;
    if(map.has(sum)){
      value = map.get(sum)
    } else{
      value = new Array();
    }
    value.push(key);
    map.set(sum,value)
  }
  return res;
};
````

#### 运行情况

执行用时：**96 ms**

内存消耗：**48 MB**

