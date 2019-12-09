[翻转链表 II](http://www.lintcode.com/zh-cn/problem/reverse-linked-list-ii/)
``` java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param ListNode head is the head of the linked list 
     * @oaram m and n
     * @return: The head of the reversed ListNode
     */
    public ListNode reverseBetween(ListNode head, int m , int n) {
        // write your code
        ListNode pre = null;
        ListNode next;
        ListNode cur = head;
        
        ListNode left;
        ListNode right;
        
        int size = n - m;
        
        while( m-- > 1 ){
            pre = cur;
            cur = cur.next;
        }
        left = pre;
        right = cur;
        pre = null;
        
        while( size-- >= 0){
            next = cur.next;
            cur.next =  pre;
            
            pre = cur;
            cur = next;
        }
        
        if( left != null ){
            left.next = pre;
        }else{
            head = pre;
        }
        right.next = cur;
        
        return head;
    }
}


//method 2
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param head: ListNode head is the head of the linked list 
     * @param m: An integer
     * @param n: An integer
     * @return: The head of the reversed ListNode
     */
    public ListNode reverseBetween(ListNode head, int m, int n) {
        // write your code here

        ListNode pre = null;
        ListNode next = null;
        ListNode cur = head;
        ListNode start = null;

        int count = 0;
        while (cur != null) {
            count++;
            next = cur.next;

            if (count == m) {
                start = cur;
            } else if (count < m) {
                pre = cur;
            }

            if (count == n) {
                cur.next = null;
                if (pre == null) {
                    head = reverse(start);
                } else {
                    pre.next = reverse(start);
                }
                start.next = next;
                break;
            }
            cur = next;
        }
        return head;
    }


    private ListNode reverse(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        ListNode next;

        while (cur != null) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
```
