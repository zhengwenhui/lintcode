[链表倒数第n个节点](http://www.lintcode.com/zh-cn/problem/nth-to-last-node-in-list/)
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
     * @return: Nth to last node of a singly linked list. 
     */
    ListNode nthToLast(ListNode head, int n) {
        // write your code here
        int size = 0;
        
        ListNode cur = head;
        while(cur != null){
            size++;
            cur = cur.next;
        }
        
        int index = size - n;
        
        cur = head;
        while( index-- > 0 ){
            cur = cur.next;
        }
        
        return cur;
    }
}

```
