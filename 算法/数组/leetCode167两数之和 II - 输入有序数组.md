# [leetCode.167 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

解法一：使用二分查找
```
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(numbers, target) {
    for(let i=0;i<numbers.length;i++){ //循环第一个值
        let index = binarySearch(numbers, target-numbers[i]) // 使用二分查找的方式找第二个值
        if(index !=-1 && index != i){
            return index>i ? [i+1, index+1]: [index+1, i+1]
        }
    }
    return [];
}
const binarySearch = function(numbers, target) {
    let l = 0, r = numbers.length;
    while(l<=r){
        let mid = parseInt((l+r)/2)
        if(numbers[mid]===target){
           return mid
        }else if(numbers[mid]<target){
            l=mid+1
        }else{
            r=mid-1
        }
        // if(numbers[mid] > target){
        //     r = mid-1
        // } else if(numbers[mid] < target){
        //     l = mid+1
        // } else {
        //     return mid
        // }
    }
    return -1
};

```

解法二：使用对撞指针
```
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(numbers, target) {
    let l = 0, r = numbers.length-1; // 头尾两个指针
    while(l<r){
        if(numbers[l]+numbers[r] === target){
            return [l+1,r+1]
        } else if(numbers[l]+numbers[r] > target){ // 大了就往左移一点
            r--
        } else{
            l++
        }
    }
    return []
};
```