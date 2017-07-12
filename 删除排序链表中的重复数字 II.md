[删除排序链表中的重复数字 II](http://www.lintcode.com/zh-cn/problem/remove-duplicates-from-sorted-list-ii/)
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
     * @return: ListNode head of the linked list
     */
    public static ListNode deleteDuplicates(ListNode head) {
        // write your code here
        ListNode root = null;
        ListNode pre = null;
        
        ListNode first = head;
        ListNode cur;
        int count;
        
        while( first != null ){
            
            cur = first.next;
            count = 0;
            while( cur != null ){
                if( cur.val != first.val ){
                    break;
                }
                else{
                    count++;
                }
                cur = cur.next;
            }
            
            if( count > 0 ){
                if( pre != null ){
                    pre.next = cur;
                }
                first = cur;
            }
            else{
                if( pre == null ){
                    root = first;
                }
                pre = first;
                first = first.next;
            }
            
        }
        
        return root;
    }
}

```
