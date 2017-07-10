[删除链表中倒数第n个节点](http://www.lintcode.com/zh-cn/problem/remove-nth-node-from-end-of-list/)
``` java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param head: The first node of linked list.
     * @param n: An integer.
     * @return: The head of linked list.
     */
    ListNode removeNthFromEnd(ListNode head, int n) {
        // write your code here
        int size = size(head);
        int index = size - n + 1;
        
        if (index > 0 && index <= size){
            ListNode pre = null;
            
            while( index-- > 1){
                if ( pre == null ){
                    pre = head;
                }else{
                    pre = pre.next;
                }
            }
            
            if ( pre == null ){
                head = head.next;
            } else{
                pre.next = pre.next.next;
            }
            
        }
        
        return head;
    }
    
    private int size(ListNode head){
        int size = 0;
        while(head != null){
            size++;
            head = head.next;
        }
        return size;
    }
}

```
