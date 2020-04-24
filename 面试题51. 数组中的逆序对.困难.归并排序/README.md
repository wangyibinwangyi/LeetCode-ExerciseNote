# 面试题51. 数组中的逆序对
### 题目：

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

#### 示例：

> 输入: [7,5,6,4]
> 输出: 5

------



### 自己的解释

归并排序，看不太懂

从题解-javascript标签-@糖炒栗子处看到归并排序思路动图：

![](.\gbpx.webp)



#### 代码示例

````javascript
var reversePairs = function(nums) {
    // 归并排序
    let sum = 0;
    mergeSort(nums);
    return sum;

    function mergeSort (nums) {
        if(nums.length < 2) return nums;
        const mid = parseInt(nums.length / 2);
        let left = nums.slice(0,mid);
        let right = nums.slice(mid);
        return merge(mergeSort(left), mergeSort(right));
    }

    function merge(left, right) {
        let res = [];
        let leftLen = left.length;
        let rightLen = right.length;
        let len = leftLen + rightLen;
        for(let index = 0, i = 0, j = 0; index < len; index ++) {
            if(i >= leftLen) res[index] = right[j ++];
            else if (j >= rightLen) res[index] = left[i ++];
            else if (left[i] <= right[j]) res[index] = left[i ++];
            else {
                res[index] = right[j ++];
                sum += leftLen - i;//在归并排序中唯一加的一行代码
            }
        }
        return res;
    }
};
    console.log(reversePairs([7,5,6,4]))
````

#### 运行情况

执行用时 :276 ms, 在所有 JavaScript 提交中击败了36.83%的用户

内存消耗 :76.1 MB, 在所有 JavaScript 提交中击败了100.00%的用户