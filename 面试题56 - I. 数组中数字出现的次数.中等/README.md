# 面试题56 - I. 数组中数字出现的次数.中等
### 题目：

一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

#### 示例：

> 输入：nums = [4,1,4,6]
> 输出：[1,6] 或 [6,1]

#### 示例2：

> 输入：nums = [1,2,10,4,1,4,3,3]
> 输出：[2,10] 或 [10,2]

------



### 自己的解释

最开始想到的是使用数组/对象的方式，如果对象中存在该数字，就在对象中删除掉，最后剩下的就是想要的值。

但是题目要求时间复杂度为O(n)，看题解说用位运算来解决，

利用相同数字异或得0，不是很懂





#### 代码示例

````javascript
  /**
 * @param {number[]} nums
 * @return {number[]}
 */
var singleNumbers = function(nums) {
  let result = [];
  for(let i =0;i<nums.length;i++){
    if(result[nums[i]]){
      delete result[nums[i]];
    }else{
      result[nums[i]] = nums[i]
    }
  }
  return Object.keys(result)
};
    console.log(singleNumbers([4,1,4,6]))
````

#### 运行情况

执行用时：**72 ms**

内存消耗：**37.9 MB**