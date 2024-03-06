```
import java.util.Arrays;
class Solution {
    public int[] solution(int N, int[] stages) {
        int[] answer = new int[N];
        double[][] failure = new double[N][2];
        for (int i = 0; i < N; i++) {
            failure[i][0] = i+1;
        }
        System.out.println(Arrays.deepToString(failure));
        int total = stages.length;
        int nowStage = 1;
        int failPeople = 0;
        Arrays.sort(stages);
        
        for (int i = 0; i < stages.length; i++) {
            if (nowStage == stages[i]) {
                failPeople += 1;
            } else {
            // 스테이지가 다르다
                failure[nowStage-1][1] = ((double)failPeople / (double)total);
                total -= failPeople;
                failPeople = 1;
                nowStage = stages[i];
                System.out.println("총: "+total+" 현재 스테이지: "+nowStage);
            }
        }
        System.out.println(nowStage);
        if (nowStage != N+1) {
            failure[nowStage-1][1] = ((double)failPeople / (double)total);
        }
        System.out.println(Arrays.deepToString(failure));
        Arrays.sort(failure, (o1, o2) -> {
            if(o1[1] == o2[1]) {
                return Double.compare(o1[0], o2[0]);
            } else {
                return Double.compare(o2[1], o1[1]);
            }
        });
        System.out.println(Arrays.deepToString(failure));
        for (int i = 0; i < failure.length; i++) {
            answer[i] = (int)failure[i][0];
        }
        return answer;
    }
}
```
