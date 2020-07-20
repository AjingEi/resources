# [leetCode.344 反转字符串](https://leetcode-cn.com/problems/reverse-string/)

使用对撞指针:
```
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */
var reverseString = function(s) {
    let l=0,r=s.length-1;
    while(l<r){
        [s[l],s[r]] = [s[r], s[l]]
        l++;
        r--
    }
    return s
};
```