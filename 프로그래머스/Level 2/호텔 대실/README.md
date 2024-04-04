```
import java.util.*;

class Solution {
    public int solution(String[][] book_time) {
        int answer = 0;
        int[][] bkt = new int[book_time.length][2];
        for (int i = 0; i < book_time.length; i++) {
            String[] now = book_time[i];
            String[] start = now[0].split(":");
            String[] end = now[1].split(":");
            int startTime = Integer.valueOf(start[0])*60 + Integer.valueOf(start[1]);
            int endTime = Integer.valueOf(end[0])*60 + Integer.valueOf(end[1]) + 10;
            bkt[i][0] = startTime;
            bkt[i][1] = endTime;
        }
        Arrays.sort(bkt, (a, b) -> a[0] - b[0]);
        //System.out.println(Arrays.deepToString(bkt));
        // 큐에서 [1]을 기준으로 오름차순
        PriorityQueue<int[]> q = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        for (int i = 0; i < bkt.length; i++) {
            while (!q.isEmpty() && q.peek()[1] <= bkt[i][0]) {
                //System.out.println(q.size());
                q.poll();
            }
            q.add(bkt[i]);
            answer = Math.max(answer, q.size());
        }
        return answer;
    }
}
```
