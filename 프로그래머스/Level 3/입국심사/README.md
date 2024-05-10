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
좋아요를 가장 많이 받은 풀이는 이분탐색은 같으나   
dfs를 추가로 구성하여 풀이하였다.   
하지만 while문으로 푸나 dfs나 같다.   
```
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.util.Arrays;

class Solution {
    public int solution(int n, int[] times) {
        Arrays.sort(times);
        return (int) find((long) n, times, (long) times.length, times[0], (long) ((long) times[0] * (long) n));
    }

    public long find(long n, int[] times, long nExamination, long from, long to) {
        long minTime;
        long tmp = n;
        if (from == to) {
            return from;
        }
        else {
            minTime = (from + to) / 2;// + ((from + to) % 2 == 1? 1 : 0);
            for (int i = 0; i < nExamination; i++) {
                tmp -=  minTime / (long) times[i];
            }
            if (tmp > 0) {
                return find(n, times, nExamination, minTime + 1, to);
            }
            else {
                return find(n, times, nExamination, from, minTime);
            }
        }
    }
}

```
