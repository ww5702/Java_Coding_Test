스택을 넣다가   
만약 마지막 숫자보다 더 작은 주식이 나온순간,   
그리고 해당 주식순간이 계속해서 작을떄까지 해당 stack.peek의 값을 i-stck.peek() 해준다.   
그리고 pop()   
다 끝나고 남은 stack의 수는 가격이 떨어지지 않은 경우의 수이므로   
해당 index를 prices.length - (stack.pop() + 1)   
해준다.   
```
import java.util.*;
class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < prices.length; i++) {
            
            while (!stack.isEmpty() && prices[stack.peek()] > prices[i]) {
                answer[stack.peek()] = i - stack.peek();
                stack.pop();
            }
            
            stack.add(i);
        }
        //System.out.println(stack);
        while (!stack.isEmpty()) {
            answer[stack.peek()] = prices.length - (stack.pop() + 1);
        }
        return answer;
    }
}
```
