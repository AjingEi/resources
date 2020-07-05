# [leetcode.102 二叉树的锯齿形层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
```
var levelOrder = function(root) {
    if(!root) return [] // 如果根节点不存在，返回空数组
    let res = []; // 记录最总结果数组
    let queue = []; // 队列
    queue.push(root); // 把第一层推到队列里面
    let level = 0; // 记录res数组索引
    while(queue.length){ // 当这一层不为空时
        res.push([]); // res添加一个新的数组
        let size = queue.length; // 获取这一层有多少个元素
        while(size--){ // 循环这一层的所有元素
            let item = queue.shift(); // 把当前元素推出并且记录
            res[level].push(item.val); // 当前元素的值推入当前这一层
            if(item.left) queue.push(item.left) // 记录下一层的值
            if(item.right) queue.push(item.right)
        }
        iif(level%2) res[level].reverse() // 倒置
        level++; // 层数++
    }
    return res;
}
```