# Fizz Buzz
---
3的倍数，输出"Fizz"，5的倍数，输出"Buzz"，3和5的倍数输出"FizzBuzz"，其余时候输出当前数字。

## 思路

> 1. if判断
> 2. 共同倍数 +"Buzz"
> 3. 如果还没赋值，就输出当前数字

## 代码
```js
/**
 * @param {number} n
 * @return {string[]}
 */
var fizzBuzz = function(n) {
    var array = [];
    var item;
    for(var i=1;i<=n;i++) {
        item = ""; //每次需重置
        if(i%3 === 0) {
            item = "Fizz";
        }
        if(i%5 === 0) {
            item += "Buzz";
        }
        if(!item) item += String(i);
        array.push(item);
    }
    return array;
};
```




