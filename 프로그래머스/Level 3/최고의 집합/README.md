3 12   
4 4 4 = 64   

3 13   
4 4 5 = 90   
    
3 14   
4 5 5 100   
처럼 n으로 나눈 값을 기본으로 가지고   
남은 값을 추가로 더해주는값이 정답이다.   
n이 s보다 큰 예외를 제외하고는 다 맞다.   
```
import java.util.Arrays;
class Solution {
    public int[] solution(int n, int s) {
        if (n > s) {
            int[] exception = new int[] {-1};
            return exception;
        }
        int[] answer = new int[n];
        int num = s / n;
        int rest = s % n;
        //System.out.println(num+ " " + rest);
        Arrays.fill(answer, num);
        for (int i = 0; i < rest; i++) {
            answer[n-i-1] += 1;
        }
        return answer;
    }
}
```
