[leetCode.209 长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

使用滑动窗口解决
```
/**
 * @param {number} s
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function(s, nums) {
    let l = 0, r = -1;
    let res = nums.length+1;
    let sum = 0;
    while(l<nums.length){
        if(sum < s && r+1<nums.length){
            r++;
            sum = sum+nums[r]
        } else {
            sum = sum-nums[l]
            l++;
        }

        if(sum>=s){
                res = Math.min(r-l+1, res)
        }
    }
    if(res === nums.length+1) res = 0
    return res
};
```