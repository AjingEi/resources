#  leetCode.103 移除链表元素

删除链表中等于给定值 val 的所有节点。

示例:
```
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```
解法1: 使用虚拟头节点
```
    /**
    * Definition for singly-linked list.
    * function ListNode(val) {
    *     this.val = val;
    *     this.next = null;
    * }
    */
    /**
    * @param {ListNode} head
    * @param {number} val
    * @return {ListNode}
    */
var removeElements = function(head, val) {
    var dummyHead = new ListNode(-1);
    dummyHead.next = head;
    prev = dummyHead;
    while(prev.next!=null){
        if(prev.next.val === val) prev.next = prev.next.next // 直接跳过当前节点
        else prev = prev.next // 继续循环
    }
    return dummyHead.next
};
```

解法2: 不使用虚拟头节点
```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function(head, val) {
    while(head !=null && head.val == val){
        let item = head
        head = head.next;
        item = null
    }
    if(head == null) return head
    let prev = head
    while(prev.next){
        if(prev.next.val === val){
            let item = prev.next
            prev.next = prev.next.next
            item = null
        } else {
            prev = prev.next
        }
    }
    return head
};
```
解法三 使用链表递归
```
var removeElements = function(head, val) {
   if(head === null) return null
   head.next = removeElements(head.next, val)
   return head.val === val ? head.next : head;
};
```