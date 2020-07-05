# [leetCode-20.有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)  
题解：
```
var isValid = function(s) {
    var stack = [];
    for(let i=0;i<s.length;i++) {
        if(s.charAt(i)==='[' || s.charAt(i)==='{' || s.charAt(i)==='(') {
            stack.push(s.charAt(i))
        } else {
            if(!stack.length) return false;
            if(s.charAt(i)===']' && stack.pop()!=='[') return false;
            if(s.charAt(i)==='}' && stack.pop()!=='{') return false;
            if(s.charAt(i)===')' && stack.pop()!=='(') return false;
        }
    }
    return !stack.length; // 如果栈数组还有剩余的内容，也返回false
};
```