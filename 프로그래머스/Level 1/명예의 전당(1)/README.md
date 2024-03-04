```
import java.util.*;
class Solution {
    public int[] solution(int k, int[] score) {
        int[] answer = new int [score.length];
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < score.length; i++) {
            if (i < k) {
                list.add(score[i]);
                Collections.sort(list);
                //System.out.println(list.get(0));
                answer[i] = list.get(0);
            } else {
                list.add(score[i]);
                Collections.sort(list);
                answer[i] = list.get(i-k+1);
            }
        }
        
        return answer;
    }
}
```
하지만 자바에는 우선순위 큐가 이미 만들어져있다   
따라서 더 쉽게 풀이가 가능하다.   
```
import java.util.*;
class Solution {
    public int[] solution(int k, int[] score) {
        int[] answer = new int [score.length];
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        int idx = 0;
        for (int s : score) {
            pq.add(s);
            //System.out.println(pq);
            if (pq.size() > k) {
                pq.poll();
            }
            answer[idx++] = pq.peek();
        }
        return answer;
    }
}
```
