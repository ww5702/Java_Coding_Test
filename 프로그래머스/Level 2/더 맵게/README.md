자바에는 heap 함수가 있어 쉽게 구현이 가능했다.   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int s : scoville) {
            pq.offer(s);
        }
        System.out.println(pq.size());
        
        while (pq.peek() < K && pq.size() > 1) {
            int first = pq.poll();
            int second = pq.poll();
            pq.offer(first + (second*2));
            answer += 1;
        }
        
        return pq.size() <= 1 ? -1 : answer;
    }
}
```
16,22,23 테케가 실패하였다.   
이는    
scoville이 2개인 경우에 대한 테스트이다.     
heap의 size가 2보다 작아 루프에서 탈출했을 때,   
heap.peek이 K 이상인지 확인 후 answer를 return 하는가   
이 두가지를 더 확인해준다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int s : scoville) {
            pq.offer(s);
        }
        while (pq.peek() < K && pq.size() > 1) {
            int first = pq.poll();
            int second = pq.poll();
            pq.offer(first + (second*2));
            answer += 1;
        }
        //System.out.println(pq);
        return pq.size() <= 1 ? pq.peek() >= K ? answer : -1 : answer;
    }
}
```
return 문을 3중으로 작성하여 풀이해주면 된다.   
