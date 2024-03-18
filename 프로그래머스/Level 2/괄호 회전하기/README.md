```
import java.util.*;
class Solution {
    public int solution(String s) {
        int answer = 0;
        for (int i = 0; i < s.length(); i++) {
            String word = s.substring(i+1,s.length()) + s.substring(0, i+1);
            String[] arr = word.split("");
            Stack<String> stack = new Stack<>();
            boolean isPossible = true;
            //System.out.println(word);
            for (String a : arr) {
                //System.out.println(a);
                if (a.equals(")")) {
                    if (stack.isEmpty()) {
                        isPossible = false;
                        break;
                    } else {
                        if (!stack.peek().equals("(")) {
                            isPossible = false;
                            break;
                        } else {
                            stack.pop();
                        }
                    }
                } else if(a.equals("}")) {
                    if (stack.isEmpty()) {
                        isPossible = false;
                        break;
                    } else {
                        if (!stack.peek().equals("{")) {
                            isPossible = false;
                            break;
                        } else {
                            stack.pop();
                        }
                    }
                } else if(a.equals("]")) {
                    if (stack.isEmpty()) {
                        isPossible = false;
                        break;
                    } else {
                        if (!stack.peek().equals("[")) {
                            isPossible = false;
                            break;
                        } else {
                            stack.pop();
                        }
                    }
                } else {
                    stack.push(a);
                }
            }
            if (!stack.isEmpty()) { isPossible = false; }
            answer += isPossible ? 1 : 0;
            //System.out.println(isPossible);
        }
        return answer;
    }
}
```
