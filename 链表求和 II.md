[链表求和 II](http://www.lintcode.com/zh-cn/problem/add-two-numbers-ii/)
``` java
/**
 * Definition for singly-linked list.
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
     * @param l1: the first list
     * @param l2: the second list
     * @return: the sum list of l1 and l2 
     */
    public ListNode addLists2(ListNode l1, ListNode l2) {
        // write your code here
        l1 = change(l1);
        l2 = change(l2);
        l1 = add(l1, l2);
        return change(l1);
    }  

    private ListNode add(ListNode l1, ListNode l2){
        ListNode head = l1;
        int carryInt = 0;
        ListNode pre = null;
        
        while( l1 != null){
            pre = l1;
            
            carryInt += l1.val;
            if(l2!=null){
                carryInt += l2.val;
            }
            l1.val = carryInt % 10;
            carryInt /= 10;
            l1 = l1.next;
            if(l2!=null){
                l2 = l2.next;
            }
        }

        if( pre != null){
            pre.next = l2;
        }else{
            head = l2;
        }
        
        while( l2 != null){
            pre = l2;
            
            carryInt += l2.val;
            l2.val = carryInt % 10;
            carryInt /= 10;
            l2 = l2.next;
        }

        if ( carryInt != 0 ){
            pre.next = new ListNode(carryInt);
        }
        
        return head;
    }

    /**
     * 反转链表
     */
    private ListNode change( ListNode l1){
        
        ListNode pre = null;
        ListNode current = l1;
        ListNode next = null;
        
        while( current != null ){
            next = current.next;
            current.next = pre;
            pre = current;
            current = next;
        }
        
        return pre;
    }
}
```
