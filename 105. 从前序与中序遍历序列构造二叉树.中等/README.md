# 105. 从前序与中序遍历序列构造二叉树.中等
### 题目：

根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

#### 返回如下的二叉树：：

> ```
>     3
>    / \
>   9  20
>     /  \
>    15   7
> ```

------



### 自己的解释

根据前序遍历可以确定根节点preoeder[0]

随后在中序遍历中确定根节点的位置



#### 代码示例

````javascript
/**
* @param {character[][]} grid
* @return {number}
*/
var numIslands = function(grid) {
      let islandNumber = 0;
      let widthLength = grid.length;
      function downplayIsland(i,j,verticalLength){
        if(i<0||j<0||i>=widthLength||j>=verticalLength||grid[i][j]==='0'){
          return;
        }
        grid[i][j] = '0';
        downplayIsland(i-1,j,verticalLength);
        downplayIsland(i,j-1,verticalLength);
        downplayIsland(i+1,j,verticalLength);
        downplayIsland(i,j+1,verticalLength);
      }
      for(let i = 0;i<widthLength;i++){
        let verticalLength = grid[i].length;
        for(let j = 0;j<verticalLength;j++){
          if(grid[i][j]==='1'){
            islandNumber++;
            downplayIsland(i,j,verticalLength)
          }
        }
      }
      return islandNumber
  };
````

#### 运行情况

执行用时：**72 ms**

内存消耗：**37.7 MB**