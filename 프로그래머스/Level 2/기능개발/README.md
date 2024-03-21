```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < speeds.length; i++) {
            if ((100 - progresses[i]) % speeds[i] != 0) {
                queue.add(((100 - progresses[i]) / speeds[i]) + 1);
            } else {
                queue.add(((100 - progresses[i]) / speeds[i]));
            }
            
        }
        //System.out.println(queue);
        List<Integer> list = new ArrayList<>();
        int now = queue.poll();
        int cnt = 1;
        while (!queue.isEmpty()) {
            if (now >= queue.peek()) {
                cnt += 1;
                queue.poll();
            } else {
                list.add(cnt);
                cnt = 1;
                now = queue.poll();
            }
        }
        list.add(cnt);
        int[] answer = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            answer[i] = list.get(i);
        }
        return answer;
    }
}
```
같은 방식이지만 완료날짜가 더 커지지않으면 +1,   
만약 더 커진다면 q를 clear해주는 방식이 더 깔끔해보였다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        Queue<Integer> q = new LinkedList<>();
        List<Integer> answerList = new ArrayList<>();

        for (int i = 0; i < speeds.length; i++) {
            double remain = (100 - progresses[i]) / (double) speeds[i];
            int date = (int) Math.ceil(remain);

            if (!q.isEmpty() && q.peek() < date) {
                answerList.add(q.size());
                q.clear();
            }

            q.offer(date);
        }

        answerList.add(q.size());

        int[] answer = new int[answerList.size()];

        for (int i = 0; i < answer.length; i++) {
            answer[i] = answerList.get(i);
        }

        return answer;
    }
}
```
