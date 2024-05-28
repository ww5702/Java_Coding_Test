누적합 개념으로 접근한다.   
1,-1,1로 시작하는 경우와   
-1,1,-1로 시작하는 경우 2가지를 구해준다.   
그동안 더해온 누적합에 현재값을 더해주는게 더 큰지, 지금 값부터 시작하는게   
더 큰지 비교해준다.   
그렇다면 자연스럽게 최대값이 나온다.   

```
import java.util.Arrays;
import java.util.stream.*;
class Solution {
    public long solution(int[] sequence) {
        long answer = 0;
        long[] cache1 = new long[sequence.length];
        long[] cache2 = new long[sequence.length];
        Arrays.fill(cache1, Integer.MIN_VALUE);
        Arrays.fill(cache2, Integer.MIN_VALUE);
        long[] giho1 = new long[sequence.length];
        long[] giho2 = new long[sequence.length];
        
        long temp = 1;
        for (int i = 0; i < sequence.length; i++) {
            giho1[i] = 1*temp;
            temp *= -1;
            giho2[i] = 1*temp;
        }
        cache1[0] = sequence[0] * giho1[0];
        cache2[0] = sequence[0] * giho2[0];
        //System.out.println(Arrays.toString(cache1));
        //System.out.println(Arrays.toString(cache2));
        
        for (int i = 1; i < sequence.length; i++) {
            cache1[i] = Math.max(sequence[i]*giho1[i], cache1[i-1] + (sequence[i]*giho1[i]));
            cache2[i] = Math.max(sequence[i]*giho2[i], cache2[i-1] + (sequence[i]*giho2[i]));
            
        }
        //System.out.println(Arrays.toString(cache1));
        //System.out.println(Arrays.toString(cache2));
        long max1 = Arrays.stream(cache1).max().getAsLong();
        long max2 = Arrays.stream(cache2).max().getAsLong();
        return Math.max(max1,max2);
    }
}
```
