# Number Complement
---
取一个正整数的补码，即二进制取反。（其实这里关于补码和反码的概念是不对的，正数的反码、补码及其本身都是一样的）
那这里就按照二进制取反来做

### 思路
> 1. 转为二进制
> 2. for遍历，取反

### 代码
```js
/**
 * @param {number} num
 * @return {number}
 */
var findComplement = function(num) {
    var bin = (num).toString(2);
    var complement = '';
    for(var i=0;i<bin.length;i++) {
        complement += bin[i] === '0' ? 1 : 0;
    }
    return parseInt(complement, 2);
};
```

值得注意的是，不能直接对bin[i]进行修改，但是可以对bin整个进行修改，这跟JavaScript的存储方式有关吧？

还有就是为什么不能用~，因为JavaScript中的~是这样操作的：
> 1. 将 `1` (这里叫：原码)转二进制 ＝ `00000001`
> 2. 按位取反 ＝ `11111110`
> 3. 发现符号位(即最高位)为1(表示负数)，将除符号位之外的其他数字取反 ＝ `10000001`
> 4. 末位加1取其补码 ＝ `10000010`
> 5. 转换回十进制 ＝ `-2`



