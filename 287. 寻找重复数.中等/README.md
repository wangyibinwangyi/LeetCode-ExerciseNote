# 287. 寻找重复数.中等
### 题目：

给定一个包含 n + 1 个整数的数组 nums，其数字都在 1 到 n 之间（包括 1 和 n），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

#### 示例：

> 输入: [1,3,4,2,2]
> 输出: 2

#### 示例2：

> 输入: [3,1,3,4,2]
> 输出: 3

说明：

不能更改原数组（假设数组是只读的）。
只能使用额外的 O(1) 的空间。
时间复杂度小于 O(n2) 。
数组中只有一个重复的数字，但它可能不止重复出现一次。

------



### 自己的解释



#### 代码示例

````javascript
    /**
 * @param {number[]} nums
 * @return {number}
 */
var findDuplicate = function(nums) {
  let slowPointer = 0
  let fastPointer = 0
  while (true) {
    slowPointer = nums[slowPointer]
    fastPointer = nums[nums[fastPointer]]
    if (slowPointer == fastPointer) {
      let _slowPointer = 0
      while (nums[_slowPointer] !== nums[slowPointer]) {
        slowPointer = nums[slowPointer]
        _slowPointer = nums[_slowPointer]
      }
      return nums[_slowPointer]
    }
  }
};
    console.log(findDuplicate([1,3,4,2,2]))
````

#### 运行情况

执行用时：**68 ms**

内存消耗：**35.8 MB**