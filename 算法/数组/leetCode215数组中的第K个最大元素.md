# [leetCode.215 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

使用快排的方式解决：
```
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findKthLargest = function(nums, k) {
    // 使用快速排序的思想
    let n = nums.length
    let quickSort = function(l,r){
        if(l>r) return;
        let p = partition(nums,l,r) // 把当前范围内的小于target的放在左边，大于target的放在右边
        if(p>(n-k)){ // 如果当前数的索引大于n-k，就继续在左边搜索
            quickSort(l,p-1)
        } else{
            quickSort(p+1,r)
        }
    }
    quickSort(0,n-1)
    return nums[n-k]
};

function partition(nums,l,r){
    let target = nums[r]
    let index = l;
    for(let i = l; i<r;i++){
        if(nums[i]<target){
            [nums[index],nums[i]] = [nums[i],nums[index]]
            index++;
        }
    }
    [nums[index], nums[r]] = [nums[r], nums[index]];
    return index
}
```