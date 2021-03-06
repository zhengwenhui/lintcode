[K组翻转链表](http://www.lintcode.com/zh-cn/problem/reverse-nodes-in-k-group/)
``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    private ListNode cur;
    /**
     * @param head a ListNode
     * @param k an integer
     * @return a ListNode
     */
    public ListNode reverseKGroup(ListNode head, int k) {
        // Write your code here
        ListNode left = head;
        ListNode right = head;
        
        ListNode pre = null;
        ListNode next;
        
        ListNode temp;

        int n;
        
        while( right != null){
            n = k;
            
            temp = right;
            while( n-- > 0){
                right = temp;
                if(right == null){
                    break;
                }
                temp = right.next;
            }
            
            if( n <= 0 && right!= null){
                next = right.next;
                right.next = null;
                
                temp = change(left);
                
                if(pre == null ){
                    head = temp;
                }else{
                    pre.next = temp;
                }
                
                while(temp.next != null){
                    temp = temp.next;
                }
                temp.next = next;
                
                pre = temp;
                left = next;
                right = left;
            }
        }
        return head;
    }
    
    private ListNode change(ListNode head){
        ListNode pre = null;
        ListNode current;
        
        while( head != null ){
            current = head;
            head = head.next;
            current.next = pre;
            pre = current;
        }
        
        return pre;
    }
}

//方法2
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
     * @param head: a ListNode
     * @param k: An integer
     * @return: a ListNode
     */
    public ListNode reverseKGroup(ListNode head, int k) {
        // write your code here
        ListNode pre = null;
        ListNode start = head;
        ListNode cur = head;
        ListNode next;

        int count = 0;
        while (cur != null) {
            count++;
            next = cur.next;

            if (count % k == 0) {
                cur.next = null;

                if (pre != null) {
                    pre.next = reverse(start);
                }else{
                    head = reverse(start);
                }
                start.next = next;

                pre = start;
                start = next;
            }
            cur = next;
        }

        return head;
    }
    
    //全翻转
    private ListNode reverse(ListNode head) {
        ListNode pre = null;
        ListNode next;
        ListNode cur = head;
        while (cur != null) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        head = pre;

        return head;
    }
}
```
