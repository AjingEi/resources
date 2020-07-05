# [leetcode.199 二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)
```
var rightSideView = function(root) {
    if(!root) return []
    let queue = [];
    let res = [];
    queue.push(root);
    while(queue.length){ //层序遍历
        res.push(queue[0].val) // 每次记录最右边的值
        let size = queue.length
        while(size--) {
            let item = queue.shift();
            if(item.right) queue.push(item.right)
            if(item.left) queue.push(item.left)
        }
    }
    return res
};
```