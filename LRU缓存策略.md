[LRU缓存策略](http://www.lintcode.com/zh-cn/problem/lru-cache/)
``` java
public class LRUCache {

    private ListNode head;
    int size = 0;
    int capacity;
    // @param capacity, an integer
    public LRUCache(int capacity) {
        // write your code here
        this.capacity = capacity;
    }

    // @return an integer
    public int get(int key) {
        // write your code here
        ListNode cur = head;
        ListNode pre = null;

        while ( cur != null ){
            if ( cur.key == key ){
                break;
            }
            pre = cur;
            cur = cur.next;
        }
        
        if( cur != null && pre != null ){
            pre.next = cur.next;
            cur.next = head;
            head = cur;
        }
        
        return cur == null ? -1 : cur.value;
    }

    // @param key, an integer
    // @param value, an integer
    // @return nothing
    public void set(int key, int value) {
        // write your code here
        ListNode cur = head;
        ListNode pre = null;
        
        while ( cur != null ){
            if ( cur.key == key ){
                break;
            }
            pre = cur;
            cur = cur.next;
        }
        
        if ( cur != null ){
            cur.value = value;
            if(pre != null ){
                pre.next = cur.next;
                cur.next = head;
                head = cur;
            }
        } else{
            // add listNode;
            ListNode s = new ListNode(key, value);
            size++;
            s.next = head;
            head = s;
            
            if(size>capacity){
                cur = head;
                pre = null;
                
                while ( cur.next != null ){
                    pre = cur;
                    cur = cur.next;
                }
                pre.next = null;
                size--;
            }
        }
    }
    
    private class ListNode {
        int key;
        int value;
        ListNode next;
        public ListNode(int key, int value){
            this.key = key;
            this.value = value;
            next = null;
        }
    }
}
```
