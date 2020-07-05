# [leetCode.26 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

解法一：
使用双指针
```
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let j = 0;
    for(let i=0;i<nums.length;i++){
        if(nums[i] !== nums[j]){
            j++
            nums[j] = nums[i]
        }
    }
    return j+1
};
```