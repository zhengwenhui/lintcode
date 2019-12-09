[Expression Expand](http://www.lintcode.com/zh-cn/problem/expression-expand/)

``` java
public class Solution {
    /**
     * @param s  an expression includes numbers, letters and brackets
     * @return a string
     */
    public String expressionExpand(String s) {
        // Write your code here
        Stack<String> stack = new Stack<String>();
        StringBuilder sb = new StringBuilder();
        String str;
        
        for (char achar : s.toCharArray()){
            if ( achar != ']'){
                stack.push(String.valueOf(achar));
            } else {
                sb.delete(0, sb.length());
                
                while( !( str = stack.pop() ).equals("[") ){
                    sb.insert(0, str);
                }
                
                int count = 0;
                int dan = 1;
                do {
                  str = stack.peek();   
                  if ( isANumeric(str) ){
                      count += Integer.valueOf(stack.pop()) * dan;
                  } else {
                      break;
                  }
                  dan *= 10;
                } while( stack.size()>0);
                
                str = sb.toString();
                sb.delete(0, sb.length());
                while(count-- > 0){
                    sb.append(str);
                }
                stack.push(sb.toString());
            }
        }
        
        sb.delete(0, sb.length());
        while( stack.size() > 0 ){
            sb.insert(0, stack.pop());
        }
        
        return sb.toString();
        
    }
    
    public boolean isANumeric(String str){
        if ( str.length() == 1 ){
            int chr = str.charAt(0);
            if(chr >= 48 && chr <= 56) {
                return true;
            }
        }
        return false;
    }
}

//方法2
public class Solution {
    /**
     * @param s: an expression includes numbers, letters and brackets
     * @return: a string
     */
    public String expressionExpand(String s) {
        // write your code here
        StringBuilder stringBuilder;
            char temp;

            LinkedList<Character> stack = new LinkedList<>();
            char[] chars = s.toCharArray();
            for (char achar : chars){
                if(achar!=']'){
                    stack.push(achar);
                }else{
                    stringBuilder = new StringBuilder();
                    while ((temp = stack.pop()) != '['){
                        stringBuilder.append(temp);
                    }

                    int sw = 1;
                    int count = 0;
                    while ( stack.peek() != null) {
                        char cchar = stack.peek();
                        int t = cchar - 48;
                        if (t < 0 || t > 9) {
                            break;
                        }
                        stack.pop();
                        count += (t * sw);
                        sw *= 10;
                    }
                    String subStr = stringBuilder.reverse().toString();
                    for (int i =0; i<count; i++){
                        for (char bchar : subStr.toCharArray()){
                            stack.push(bchar);
                        }
                    }
                }
            }

            stringBuilder = new StringBuilder();
            while (stack.peek()!=null){
                stringBuilder.append(stack.pop());
            }

            return stringBuilder.reverse().toString();
    }
}
```
