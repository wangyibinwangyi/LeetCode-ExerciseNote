# 200.岛屿数量.中等
### 题目：

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

#### 示例：

> 输入:
>
> 11110
>
> 11010
>
> 11000
>
> 00000
>
> 输出: 1

#### 示例2：

> 输入:
>
> 11000
>
> 11000
>
> 00100
>
> 00011
>
> 输出: 3

------



### 自己的解释

每座岛屿只能由水平和/或竖直方向上相邻的陆地连接而成。



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