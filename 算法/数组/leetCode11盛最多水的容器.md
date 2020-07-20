# [leetCode.11 盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

每次移动最矮的柱子，记录最大面积
```
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    let l = 0, r = height.length-1;
    let maxArea = 0;
    while(l<r){
        let curArea = (r-l)*Math.min(height[l],height[r])
        if(curArea>maxArea){
            maxArea = curArea
        }
        if(height[l] > height[r]){
            r--
        }else {
            l++
        }
    }
    return maxArea
};
```