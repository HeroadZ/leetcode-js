# Reverse String
---
反转字符串

## 思路
> 1. 由于JavaScript的字符串不带原生reverse方法，而数组可以reverse。
> 2. 将字符串分割成数组，reverse，再合并。

## 代码
```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseString = function(s) {
    return s.split("").reverse().join('');
};
```




