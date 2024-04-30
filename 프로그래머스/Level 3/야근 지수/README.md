단순하게 가장 크게 남은 작업량을 1씩 빼주는 일이다.   
즉, 우선순위 큐가 있다면 쉽게 풀이가 가능하다.   
Java에는 pq가 있어 쉽게 풀이가 가능하다.   

```
import java.util.*;
class Solution {
    public long solution(int n, int[] works) {
        long answer = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
        for (int w: works) {
            pq.add(w);
        }
        //System.out.println(pq);
        for (int i = 0; i < n; i++) {
            int num = pq.poll();
            num -= 1;
            pq.add(num);
        }
        //System.out.println(pq);
        for (int x : pq) {
            if (x >= 1) {
                answer += Math.pow(x, 2);
            }
        }
        return answer;
    }
}
```
