```
import java.util.Arrays;
import java.util.stream.*;
import java.util.*;
class Solution {
    public int solution(int[] queue1, int[] queue2) {
        int answer = 0;
        Queue<Integer> q1 = new LinkedList<>();
        Queue<Integer> q2 = new LinkedList<>();
        long q1Sum = 0;
        long q2Sum = 0;
        for (int i = 0; i < queue1.length; i++) {
            q1.add(queue1[i]);
            q2.add(queue2[i]);
            q1Sum += queue1[i];
            q2Sum += queue2[i];
        }
        
        while (true) {
            if (answer > queue1.length * 3) {
                answer = -1;
                break;
            }
            
            if (q1Sum == q2Sum) {
                break;
            }
            
            if (q1Sum > q2Sum) {
                q2.add(q1.peek());
                q2Sum += q1.peek();
                q1Sum -= q1.poll();
            } else {
                q1.add(q2.peek());
                q1Sum += q2.peek();
                q2Sum -= q2.poll();
            }
            answer += 1;
            
        }
        
        
        
        return answer;
    }
}
```
