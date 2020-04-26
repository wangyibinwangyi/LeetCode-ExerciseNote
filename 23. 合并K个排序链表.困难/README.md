# 23. 合并K个排序链表.困难
### 题目：

合并 *k* 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

#### 示例：

> 输入:
> [
>   1->4->5,
>   1->3->4,
>   2->6
> ]
> 输出: 1->1->2->3->4->4->5->6

------



### 自己的解释

使用双指针，过程中两两合并。

时间复杂度：O(kn)(k为链表个数，n为当前两个合并中链表的长度)
空间复杂度：O(1)



#### 代码示例

````javascript
    /**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function(lists) {
  let list = new ListNode();
  let mergeTwoLists = (l1,l2)=>{
      let preHead = new ListNode(-1);
      let preNode = preHead;
      while(l1 && l2){
            if(l1.val <= l2.val){
                preNode.next = l1
                l1 = l1.next
            }else{
                preNode.next = l2
                l2 = l2.next
            }
            preNode = preNode.next
        }
        preNode.next = l1 ? l1 : l2;
      return preHead.next;
  }
  let n = lists.length;
  if(n===0) return null;
  
  let res = lists[0];
  for(let i=1;i<n;i++)  { 
    if(lists[i]){
      res = mergeTwoLists(res,lists[i])
    }
  }
  return res;
};
````

#### 运行情况

执行用时：**264 ms**

内存消耗：**37.5 MB**