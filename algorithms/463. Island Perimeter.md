# Island Perimeter

标签（空格分隔）： leetcode
---

给出一个只有0和1的二维数组，1是陆地，0是海洋，求陆地周长。

## 思路
> 1. 周长可以分别两部分，横着的和竖着的
> 2. 首先从左到右从上到下进行遍历，如果当前的前面一个不一样，则会产生一个类似上升沿或者下降沿之类的东西，则count++；
> 3. 需要注意的是，首个和最后一个都默认为0
> 4. 然后就是纵向遍历，同样如果当前的和前面的不一致，count++；

## 代码
```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    var count = 0, prev;
    //横向
    for(var i=0, len = grid.length; i<len;i++) {
        //初始判断
        prev = 0;
        
        for(var j=0,len2 = grid[i].length;j<len2;j++) {
            if(grid[i][j] !== prev) {
                count++;
            }
            prev = grid[i][j];
        }
        //最后一次判断
        if(prev === 1) {
            count++;
        }
    }
    //纵向
    for(var c=0, len3=grid[0].length;c<len3;c++) {
        prev = 0;
        for(var r=0;r<len;r++) {
           if(grid[r][c] !== prev) {
               count++;
           }
           prev = grid[r][c];
        }
        //最后一次判断
        if(prev === 1) {
            count++;
        }
    }
    
    return count;
};
```

## 更好的算法
因为我的算法需要遍历数组两遍，所以很慢。其实，周长可以用island * 4 - neighbour * 2来表示，island表示陆地数量，neighbour标识陆地的右相邻和下相邻数量和。

## 代码
```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    var count = 0, island = 0, neighbour = 0;
    for(var i=0, len = grid.length; i<len;i++) {
        for(var j=0,len2 = grid[i].length;j<len2;j++) {
            if(grid[i][j] === 1) {
                island++;
                //右相邻
                if(j < len2 - 1) {
                    if(grid[i][j+1] === 1) {
                        neighbour++;
                    }
                }
                //下相邻
                if(i < len -1) {
                    if(grid[i+1][j] === 1) {
                        neighbour++;
                    }
                }
            }
            
        }
    }
    
    count = island * 4 - neighbour * 2;
    
    return count;
};
```



