# [leetCode.125 验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

使用对撞指针
```
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {

    let str = s.replace(/\W|_/g, '').toLowerCase()
    let l = 0, r = str.length-1;
    while(l<r){
        if(str[l] != str[r]){
            return false
        }
        l++;
        r--;
    }
    return true
};
```