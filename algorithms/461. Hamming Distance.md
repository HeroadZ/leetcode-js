# 汉明距离
---
汉明距离是使用在数据传输差错控制编码里面的，
汉明距离是一个概念，它表示两个（相同长度）字对应位不同的数量。
## 进制之间的转换
### 正整数
* 十进制转二进制，八进制，十六进制
```js
(3).toString(2) //"11"
```
* 二进制转八进制等，必须先转到十进制
```js
parseInt("1010", 2).toString(8) //"12"
```
### 负数
* 负数的二进制为正数二进制的补码（即反码+1）,但是js的toString方法只对正数有效，如果是负数的话，则保留其符号。
```js
(-3).toString(2) //"-11"
```
* 值得注意的是，虽然得到的二进制码是错误的，但是如果再转回十进制，仍然可以得到正确的数，因为-这个符号一直保留着。
```js
parseInt((-3).toString(2), 2) //-3
```
* 那么如何得到正确的负数的二进制码呢
```js
(-3 >>> 0).toString(2)   //to uint32
// "11111111111111111111111111111101"
parseInt((-3 >>> 0).toString(2), 2)
// 4294967293
parseInt((-3 >>> 0).toString(2), 2) >> 0  // to int32
// -3
```
首页 >>> 在JavaScript中会把参数强制转换为uint32（无符号整形），这样就可以用toString得到正确的二进制码。然而，在解析的时候，解析出来的数依然是unit32的，所以我们需要>>来将其转化为int32类型。

## 汉明距离
### 思路
> 1. 得到数字的二进制字符串
> 2. 得到最长字符串的长度，另外一个字符串补0保证长度一样
> 3. 每个字符进行比较，不等count++  

### 代码
```js
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
var hammingDistance = function(x, y) {
    var xBin = x.toString(2);
    var yBin = y.toString(2);
    var xBinLen = xBin.length;
    var yBinLen = yBin.length;
    var length = Math.max(xBinLen, yBinLen);
    if(length === yBinLen) { //短的补0
        // +1是因为join()最后一个不加
        // substr()是应该要补的字符串（总长-原来长度）
        xBin = Array(length+1).join('0').substr(xBinLen) + xBin;
    } else {
        yBin = Array(length+1).join('0').substr(yBinLen) + yBin;
    }
    var count = 0;
    for(var i=0;i<length;i++) {
        if(xBin[i] !== yBin[i]) count++;
    }
    return count;
};
```

### 更好的写法
```js
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
var hammingDistance = function(x, y) {
    return (x ^ y).toString(2).replace(/0/g, '').length;
};
```
利用位运算符^得到不同，再转化为二进制，此时1是不同位，0是相同位。再用正则全局匹配，去除0，去length得到汉明距离。

