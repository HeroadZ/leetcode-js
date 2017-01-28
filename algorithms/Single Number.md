# Single Number

标签（空格分隔）： leetcode

---

## 要求
给一个只包含整数的数组，每个元素出现两次，除了一个元素只出现一次，找出那个元素。
比如[1, 2, -3, -3, 1] => 2
线性时间复杂度，且不占用额外空间

## 思路
这题我没有想出比较好的方法，对位运算一点都不熟练，分享下人们算法。
```md
由A^A = 0, A^B^A = B
得出我们可以让数组所有的数异或，相同的数消除，剩下一个只出现1次的元素。
```

## 代码
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    var result = nums[0];
    for(var i=1,len=nums.length;i<len;i++) {
        result ^= nums[i];
    }
    return result;
};
```




