[二叉树的层次遍历 II](http://www.lintcode.com/zh-cn/problem/binary-tree-level-order-traversal-ii/)
``` java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
 
 
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: buttom-up level order a list of lists of integer
     */
    public ArrayList<ArrayList<Integer>> levelOrderBottom(TreeNode root) {
        // write your code here
        ArrayList<ArrayList<Integer>> treeMap = new ArrayList<ArrayList<Integer>>();
        if ( root != null ){
            Queue<TreeNode> queue = new LinkedList<TreeNode>();
            queue.add(root);
            
            while(queue.size() > 0){
                int count = queue.size();
                ArrayList<Integer> treeList = new ArrayList<Integer>();
                
                for ( int i = 0; i < count; i++ ){
                    TreeNode node = queue.remove();
                    treeList.add(node.val);
                    
                    if ( node.left != null){
                        queue.add( node.left);
                    }
                    
                    if ( node.right != null){
                        queue.add( node.right);
                    }
                }
                
                treeMap.add( 0, treeList);
            }
        }
        
        return treeMap;
    }
}
```
