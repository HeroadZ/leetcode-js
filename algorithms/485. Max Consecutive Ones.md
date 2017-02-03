# Max Consecutive Ones
---
寻找一个数组中，连续的1的最大长度，数组只有0和1。

### 思路
> 1. 定义count和max
> 2. 1时count++，0时取max和count中较大值，置零count
> 3. 最后一次循环时，取max和count中较大值（**很重要**）

### 代码
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMaxConsecutiveOnes = function(nums) {
    var count = 0, max = 0;
    for(var i=0;i<nums.length;i++) {
        if(nums[i] === 1) {
            count++;
        } else {
            if(count > max) {
                max = count;
            }
            count = 0;
        }
        //如果一个数组全是1的话，如果没有这一步，max就没有赋值，而且最后count也要和max比较一次，这一步是最容易遗漏的
        if(i === nums.length-1) {
            max = count>max? count:max;
        }
    }
    return max;
};
```




