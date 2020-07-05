# [leetCode.80 删除排序数组中的重复项 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let j = 0;
    for(let i=0;i<nums.length;i++){
        if(nums[i] !== nums[j-2]){
            nums[j] = nums[i];
            j++
        }
    }
    return j
};
```