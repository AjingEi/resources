# [leetCode.75 颜色分类](https://leetcode-cn.com/problems/sort-colors/)

解法一：
```
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    nums.sort()
};
```

解法二：
```
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let zero = -1;
    let two = nums.length;
    for(let i=0;i<two;){
        if(nums[i] === 1){
            i++
        } else if(nums[i] === 0) {
            zero++;
            [nums[zero], nums[i]] = [nums[i], nums[zero]]
            i++
        } else {
            two--;
            [nums[two], nums[i]] = [nums[i], nums[two]]
        }
    }
    return nums
};
```
解法三： 循环列表，计算所有的0有多少，所有的1有多少，所有的2有多少，再按数量顺序都放进数组。