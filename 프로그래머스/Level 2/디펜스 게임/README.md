우선순위큐를 반대로 돌려서   
n으로 막을수있을때까지 라운드를 진행한다.   
못막는 병사들이 나온다면 무적권을 사용한다.   
```
import java.util.*;
class Solution {
    public int solution(int n, int k, int[] enemy) {
        int answer = 0;
        PriorityQueue<Integer> q = new PriorityQueue<>(Collections.reverseOrder());
        for (int e : enemy) {
            q.add(e);
            answer++;
            n -= e;
            if (n < 0) {
                if(k==0){
                    return answer-1;
                }
                n = n + q.poll();
                k--;
            }
        }
        return enemy.length;
    }
}
```
