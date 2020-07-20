# [leetCode.345 反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)
```
/**
 * @param {string} s
 * @return {string}
 */
var reverseVowels = function(s) {
    let yuany = new Set(['a','e','i','o','u','A','E','I','O','U'])
    s = s.split('')
    let l = 0, r = s.length-1;
    while(l<r){
        if(yuany.has(s[l]) && yuany.has(s[r])){
            [s[l], s[r]] = [s[r], s[l]]
            l++;
            r--;
        } else if(!yuany.has(s[l])){
            l++;
        } else{
            r--
        }
    }
    return s.join('')
};
```