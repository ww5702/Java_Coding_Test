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
좋아요를 가장 많이 받은 코드를 보았지만   
예전 테스트케이스일때를 기준으로 -1 후 정렬, -1 후 정렬로 풀이한 방식이었다.   
이 방식은 계속해서 정렬을 해줘야함으로 O(N)이다.   
따라서 pq를 사용한 방식이 맞는것 같다.   
