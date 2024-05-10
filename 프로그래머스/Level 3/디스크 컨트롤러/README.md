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
작업을 시작한 작업은 취소할수 없다는 조건을 적용시키지 않아서   
실패가 난것이었다.   
처음 들어온 작업을 실행시키고, 끝난 시점의 시간을 구해준다.   
끝난 시점의 시간보다 전에 작업요청이 들어온 작업들은 전부 넣어준다.   
그리고 pq에 의해 정렬된 작업들중 가장 빨리 끝나는 작업부터 우선적으로 해결해준다.   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(int[][] jobs) {
        int answer = 0;
        Arrays.sort(jobs, (o1,o2) -> {
            if (o1[0] == o2[0]) {
                return o1[1] - o2[1];
            } else {
                return o1[0] - o2[0];
            }
        });
        int jobIdx = 1;
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        
        pq.add(jobs[0]);
        int time = jobs[0][0];
        
        while (!pq.isEmpty()) {
            System.out.println(pq.size());
            int[] now = pq.poll();
            answer += Math.abs(time - now[0]) + now[1];
            time += now[1];
            System.out.println(time+" "+answer);
            
            while (jobIdx < jobs.length && jobs[jobIdx][0] <= time) {
                pq.add(jobs[jobIdx++]);
            }
            
            // [1,4] / [5,10] 과 같이 만약에 4에 끝난 작업보다
            // 더 뒤에 있는 작업들이 남아있고 추가가 안됐을경우
            if (jobIdx < jobs.length && pq.isEmpty()) {
                pq.add(jobs[jobIdx++]);
            }
        }
        
        return answer/jobs.length;
    }
}
```
