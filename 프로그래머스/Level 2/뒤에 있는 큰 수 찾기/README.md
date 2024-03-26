배열의 길이가 1,000,000이라 2중반복문은 시간초과가 발생한다.   
```
import java.util.Arrays;
class Solution {
    public int[] solution(int[] numbers) {
        int[] answer = new int[numbers.length];
        int idx = 0;
        for (int i = 0; i < answer.length; i++) {
            answer[i] = -1;
        }
        
        for (int i = 0; i < numbers.length-1; i++) {
            int now = numbers[i];
            for (int j = i+1; j < numbers.length; j++) {
                if (numbers[j] > now) {
                    answer[idx] = numbers[j];
                    break;
                }
            }
            idx += 1;
        }
        return answer;
    }
}
```
스택을 이용해 만약 해당 숫자가 stack의 마지막보다 더 크다면   
스택이 비거나 해당숫자보다 커질때까지 값들을 바꿔준다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int[] solution(int[] numbers) {
        int[] answer = new int[numbers.length];
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < answer.length; i++) {
            answer[i] = -1;
        }
        
        for (int i = 0; i < numbers.length; i++) {
            //System.out.println(stack);
            while (!stack.isEmpty() && numbers[stack.peek()] < numbers[i]) {
                answer[stack.pop()] = numbers[i];
            }
            stack.push(i);
        }
        return answer;
    }
}
```
