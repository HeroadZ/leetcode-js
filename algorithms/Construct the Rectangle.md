# Construct the Rectangle

标签（空格分隔）： leetcode

---

## 要求
```md
给出长方形的面积，正整数。给出长和宽，也为正整数。
L>=W
L和W的差距尽量小
例如 4 => [2, 2] 
```

## 思路
```md
先计算出area的平方，最好是能够开方的，如果非整数，取整数部分。
如果area不能被w整除，则w--
最后当w = 1时，area是可以整除的
输出[area/w, w]
```

## 代码
```js
/**
 * @param {number} area
 * @return {number[]}
 */
var constructRectangle = function(area) {
    var w = Math.floor(Math.sqrt(area));
    while(area%w !== 0) w--;
    return [area/w, w];
};
```




