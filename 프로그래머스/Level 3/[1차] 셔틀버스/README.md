구현 문제이다.   
버스시간과 탑승시간들을 정수로 변환하여 저장하고   
버스가 도착하기 전까지 미리 서있는 사람들의 수를 늘리면서   
만약 한대당 태울수 있는 m을 넘어가기전까지 더해준다.   
그리고 아직 버스에 자리가 남았다면 가장 마지막 버스를 타는것이고   
자리가 없다면 가장 마지막 idx의 크루 앞에 서있어야 한다.   

```
import java.util.Arrays;
class Solution {
    public String solution(int n, int t, int m, String[] timetable) {
        String answer = "";
        int[] busTime = new int[n];
        int startTime = 540;
        for (int i = 0; i < n; i++) {
            busTime[i] = startTime;
            startTime += t;
        }
        //System.out.println(Arrays.toString(busTime));
        int[] list = new int[timetable.length];
        for (int i = 0; i < timetable.length; i++) {
            String[] now = timetable[i].split(":");
            list[i] = Integer.valueOf(now[0]) * 60 + Integer.valueOf(now[1]);
        }
        Arrays.sort(list);
        //System.out.println(Arrays.toString(list));
        
        int result = 0;
        
        int idx = 0;
        for (int i = 0; i < n; i++) {
            int now = busTime[i];
            int cnt = 0;
            while (idx < list.length && cnt < m && list[idx] <= now) {
                idx += 1;
                cnt += 1;
            }
            //System.out.println(idx+" "+cnt);
            if (cnt < m) {
                result = busTime[n-1];
            } else {
                result = list[idx-1]-1;
            }
            if (idx > list.length) { break; }
            
        }
        
        
        //System.out.println(idx+" "+result);
        int hour = result / 60;
        if (hour < 10) {
            answer += "0";
        }
        answer += String.valueOf(hour);
        answer += ":";
        int min = result % 60;
        if (min < 10) {
            answer += "0";
        }
        answer += String.valueOf(min);
        return answer;
    }
}
```
좋아요를 가장 많이 받은 풀이도 위와 같이 풀이하였다.   
