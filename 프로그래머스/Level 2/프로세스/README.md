pq를 이용하여 풀이한 문제이다.   
만약 기본 배열의 순서가 pq로 정렬한 순서와 값이 같아진 순간이 온다면   
해당 Index가 제일 먼저 빠져나가는 순번이므로 해당 순번을 return   
하지만 원하는 location이 아니라면 answer++ 해준뒤 해당 pq값을 제거   
이미 Index는 지나가고 있는 도중이므로 배열을 한바퀴 다 돌고 난 다음   
다시 0번 인덱스로 돌아간다.   

```
import java.util.*;
class Solution {
    public int solution(int[] priorities, int location) {
        int answer = 1;
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
        
        for (int priority: priorities) {
            pq.add(priority);
        }
        while(!pq.isEmpty()){
            for(int i=0; i<priorities.length; i++){
                
                if(priorities[i] == (int)pq.peek()){
                    //System.out.println(""+i+" "+pq.peek());
                    if(i == location){
                        return answer;
                    }
                    pq.poll();
                    answer++;
                }
                System.out.println(pq);
            }
        }
        return answer;
    }
}
```
