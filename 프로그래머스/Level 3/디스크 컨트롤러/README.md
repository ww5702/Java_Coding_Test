pq를 구성하여 남은 시간이 가장 적은 순서대로 처리하는 로직을 구현했다.   
하지만 실패하였다.   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(int[][] jobs) {
        int answer = 0;
        //PriorityQueue<int[]> q = new PriorityQueue<>((a,b) -> (a[1]-a[0]) - (b[1]-b[0]));
        // for (int[] job : jobs) {
        //     q.add(job);
        // }
        //System.out.println(q.peek()[0]+" "+q.peek()[1]);
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        
        //q.add(jobs[0]);
        pq.add(jobs[0]);
        int time = jobs[0][0];
        
        for (int i = 1; i < jobs.length; i++) {
            int nextTime = jobs[i][0];
            //System.out.println(nextTime+" "+jobs[i][1]);
            
            // 다음 시간까지 가장 빠르게 해결가능한 문제를 줄여준다.
            if (!pq.isEmpty()) {
                //System.out.println("작업");
                int pqStartTime = pq.peek()[0];
                int duration = pq.poll()[1];
                duration -= (nextTime - time);
                
                //System.out.println(time+" "+duration);
                
                if (duration >= 1) {
                    pq.add(new int[] {pqStartTime, duration});
                } else {
                    answer += ((time+duration) - pqStartTime);
                }
                
            }
            time = nextTime;
            pq.add(new int[] {nextTime, jobs[i][1]});
        }
        
        //System.out.println(time);
        while (!pq.isEmpty()) {
            int st = pq.peek()[0];
            int duration = pq.poll()[1];
            //System.out.println(st+" "+duration);
            time += duration;
            answer += (time - st);
            //System.out.println("끝 "+time+" "+answer);
        }
        
        return answer / jobs.length;
    }
}
```
