# 102. 二叉树的层序遍历.中等
### 题目：

给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

#### 示例：

> 二叉树：[3,9,20,null,null,15,7],
>
> ​    3
>
>    / \
>   9  20
> ​      /  \
> ​    15   7
> 返回其层次遍历结果：
>
> [
>   [3],
>   [9,20],
>   [15,7]
> ]



------



### 自己的解释

二叉树的广度优先搜索，贴一张@<https://leetcode-cn.com/u/shetia/> 发的图解

![image.png](https://pic.leetcode-cn.com/5dfceb048458d54eb9b7648ada9a8f1b5b134b3b9f541f5af0324d4a2360a8ee-image.png)



#### 代码示例

````javascript
    /**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function(root) {
  if(!root) return []
  let res = [];
  let queue = [root];
  while(queue.length>0){
    let len = queue.length;
    let arr = [];
    while(len){
      let node = queue.shift();
      arr.push(node.val);
      if(node.left) queue.push(node.left);
      if(node.right) queue.push(node.right);
      len--;
    }
    res.push(arr)
  }
  return res
};
````

#### 运行情况

执行用时：**80 ms**

内存消耗：**34.7 MB**