기다리는 사람이 10억명 이상인것을 보자마자 이분탐색을 떠올려야한다.   
쉽게 생각해서 가장 오래 걸리는 사람한테 n명이 전부 심사를 본다   
그렇다면 해당 숫자가 가장 오래 걸릴때이다.   
1분~해당숫자 / 2 부터 시작하여 각 심사관을 나눠 몫을 구한다.   
그렇다면 각 심사관마다 해당 시간으로 처리할 수 있는 사람의 수가 나온다.   

```
import java.util.Arrays;
class Solution {
    public long solution(int n, int[] times) {
        long answer = 0;
        int max = 0;
        for(int i = 0; i < times.length; i++) {
            if(max < times[i]) {
                max = times[i];
            }
        }
        long start = 1, end = (long)max * n;
        
        while (start <= end) {
            long middle = (start+end)/2;
            long sum = 0;
            for(int i = 0; i < times.length; i++) {
                sum += middle / times[i];
            }
            
            if (sum < n) {
                start = middle+1;
            } else {
                end = middle-1;
                answer = middle;
            }
        }
        
        return answer;
    }
}
```
