# 1095. 山脉数组中查找目标值.困难
### 题目：

（这是一个 交互式问题 ）

给你一个 山脉数组 mountainArr，请你返回能够使得 mountainArr.get(index) 等于 target 最小 的下标 index 值。

如果不存在这样的下标 index，就请返回 -1。

 

何为山脉数组？如果数组 A 是一个山脉数组的话，那它满足如下条件：

首先，A.length >= 3

其次，在 0 < i < A.length - 1 条件下，存在 i 使得：

A[0] < A[1] < ... A[i-1] < A[i]
A[i] > A[i+1] > ... > A[A.length - 1]


你将 不能直接访问该山脉数组，必须通过 MountainArray 接口来获取数据：

MountainArray.get(k) - 会返回数组中索引为k 的元素（下标从 0 开始）
MountainArray.length() - 会返回该数组的长度


注意：

对 MountainArray.get 发起超过 100 次调用的提交将被视为错误答案。此外，任何试图规避判题系统的解决方案都将会导致比赛资格被取消。

为了帮助大家更好地理解交互式问题，我们准备了一个样例 “答案”：https://leetcode-cn.com/playground/RKhe3ave，请注意这 不是一个正确答案。

#### 示例：

> 输入：array = [1,2,3,4,5,3,1], target = 3
> 输出：2
> 解释：3 在数组中出现了两次，下标分别为 2 和 5，我们返回最小的下标 2。

#### 示例2：

> 输入：array = [0,1,2,4,2,1], target = 3
> 输出：-1
> 解释：3 在数组中没有出现，返回 -1。

提示：

3 <= mountain_arr.length() <= 10000
0 <= target <= 10^9
0 <= mountain_arr.get(index) <= 10^9

------



### 自己的解释

最开始想法是二分法，从中间取数，如果中间值小于目标值target，则一定在右边。否则看中间位+1的值大于中间值，则一定在左边，否则一定在右边。继续二分法。

如此忘了另一种情况：目标值在山峰右侧

若再执行一次，不能保证中位右侧一定不存在山峰的情况。

因此需要先找到山峰，然后分成左右两侧进行二分法。



#### 代码示例

````javascript
 /**
 * // This is the MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * function MountainArray() {
 *     @param {number} index
 *     @return {number}
 *     this.get = function(index) {
 *         ...
 *     };
 *
 *     @return {number}
 *     this.length = function() {
 *         ...
 *     };
 * };
 */

/**
 * @param {number} target
 * @param {MountainArray} mountainArr
 * @return {number}
 */
  function MountainArray(arr) {
      let Arr=arr;
      this.get = function(index) {
          return Arr[index]
      };
      this.length = function() {
          return Arr.length;
      };
  };
var findInMountainArray = function(target, mountainArr) {
  //查找峰值
  
    let arrLength = mountainArr.length()-1;
    let left = 0;
    let right = arrLength;
    while(left<right){
      const mid = (left+right)/2|0;
      if(mountainArr.get(mid)>=mountainArr.get(mid+1)){
        //峰值一定在左侧
        right = mid;
      }else{
        //峰值一定在右侧
        left = mid + 1;
      }
    }
    const mountainTop = left;
    const index = searchTarget(mountainArr,target,0,mountainTop,v=>v)
    if(index!=-1)return index;
    return searchTarget(mountainArr,target,mountainTop+1,arrLength,v=>-v)
    
    function searchTarget(list,target,l,r,fn){
      target = fn(target);
      while(l<=r){
        const mid = (l+r)/2|0;
        const cur = fn(list.get(mid));
        if(cur === target)return mid;
        if(cur < target){
          l = mid +1;
        }else{
          r = mid -1;
        }
      }
      return -1;
    }
};
let arr = new MountainArray([1,5,2]);
    console.log(findInMountainArray(2,arr))
````

#### 运行情况

执行用时：**68 ms**

内存消耗：**34.3 MB**