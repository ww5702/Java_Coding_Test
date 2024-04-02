스택을 이용해 들어온 숫자가 지금까지 stack에 들어간 숫자보다 크다면    
기존에 들어온 숫자를 지워주고 해당 숫자로 다시 넣어준다.   
그리고 다시 그 앞의 숫자보다도 크다면 해당 숫자를 지워주고 현재 숫자를 넣어준다.   
그렇게 k가 다 떨어지면 return   
만약 333222111 과 같이 내림차순으로 숫자가 있을수도 있으니   
answer에 값을 넣어줄때 stack.size()-k로 제한을 걸어둔다.   
```
import java.util.*;
class Solution {
    public String solution(String number, int k) {
        String answer = "";
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < number.length(); i++) {
            int now = Integer.valueOf(number.charAt(i))-48;
            //System.out.println(now);
            while (!stack.isEmpty() && k > 0 && stack.peek() < now) {
                stack.pop();
                k -= 1;
            }
            stack.add(now);
        }
        //System.out.println(stack);
        for (int i = 0; i < stack.size()-k; i++) {
            answer += stack.get(i);
        }
        return answer;
    }
}
```
