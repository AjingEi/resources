# [leetCode.283 移动零](https://leetcode-cn.com/problems/move-zeroes/)
解法一：
```
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
    let k=0;
    for(let i=0;i<nums.length;i++){
        if(nums[i]){ // 如果不是零
            if(k!=i) [nums[i],nums[k]]=[nums[k],nums[i]] // 如果不是同一个位置
            k++;
        }
    }
    return nums
};
```
解法二：
```
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    let index = 0;
    for(let i=0;i<nums.length;i++){
        if(nums[i] !== val){
            if( index !== i)
            nums[index] = nums[i];
            index++
        }
    }
    return index
};
```
