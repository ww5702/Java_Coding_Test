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
좋아요를 가장 많이 받은 풀이이다.   
풀이 방식은 똑같았지만      
while문을 이용해 해당 index에 +1을 해주는 방식이었다.   
하지만 이 방식은 n이 10,000 이하라서 가능한 풀이인것 같다.   
```
import java.util.Arrays;

public class BestSet {

    public int[] bestSet(int n, int s){
       int[] answer = null; 
      if(n>s) {
          answer = new int[1];
          answer[0] = -1;
        } else {
         answer = new int[n];
         int i = 0;
         while(s>0) {
            answer[(i%n)]++;
          i++;
          s--;
         }

        }
                Arrays.sort(answer);
        return answer;  
    }
    public static void main(String[] args) {
        BestSet c = new BestSet();
        //아래는 테스트로 출력해 보기 위한 코드입니다.
        System.out.println(c.bestSet(3,13));
    }

}

```
