# 33. 搜索旋转排序数组.中等
### 题目：

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

#### 示例：

> 输入: nums = [4,5,6,7,0,1,2], target = 0
> 输出: 4

#### 示例2：

> 输入: nums = [4,5,6,7,0,1,2], target = 3
>
> 输出: -1

------



### 自己的解释

题目给出时间复杂度必须是logn，可以用二分法
给定任意一个位置为断点，分成的两组数组中一定有一组是有序的。
那么只需要判断两组数组的第一个数字是否大于等于要选的数字即可



#### 代码示例

````javascript
 /**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
  var search = function(nums, target) {
    let index = -1;
    let middleIndex  = Math.floor(nums.length/2);
    let start = 0;
    let end = nums.length-1;
    while(start<=end){
      //位运算，相当于/2
      const mid = start+ ((end - start) >> 1);
      if(nums[mid]===target){return mid};
      
      if(nums[mid]>=nums[start]){
        //再start~mid中有序
        if(target>=nums[start] && target <=nums[mid]){
          end = mid-1;
        }else{
          //target 不在 [start,mid]
          start = mid +1;
        } 
      }else{
        //[mid,end]中有序
        if(target >=nums[mid]&&target<=nums[end]){
          start = mid + 1;
        }else{
          end = mid - 1;
        }
      }
    }

    return -1;
  };
````

#### 运行情况

执行用时：**72 ms**

内存消耗：**33.8 MB**