11011   
3   
110/11 11011 00000 11/011 11011   
3 8 () 18 23 (1~25)   
11011 / 11011 / 00000 / 11011 / 11011 //   
11011 / 11011 / 00000 / 11011 / 11011 //   
00000 / 00000 / 00000 / 00000 / 00000 //   
3 8 18 23 (5) 28 33 43 48 (25) 78 83 93 98 (5) 103 108   

0이 있는 칸들을 수치화 해둔것이다.   
자세히 보면 중간 연속된 0을 제외하면   
0의 좌우에 4개씩 값이 존재하는것을 알 수 있다.   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    static int num;
    public long solution(int n, long l, long r) {
        num = n;
        return cal(r) - cal(l-1);
    }
    public long cal(long num) {
        // 범위가 5이하일때 단순계산
        if (num <= 5) { 
            int[] arr = {1,1,0,1,1};
            int[] value = Arrays.copyOfRange(arr,0,(int)num);
            //System.out.println(Arrays.toString(value));
            return Arrays.stream(value).sum();
        }
        long base = 1;
        while ((long)Math.pow(5,base+1) < num) {
            base += 1;
        }
        //System.out.println(base);
        long section = num / (long)Math.pow(5,base);
        long remainder = num % (long)Math.pow(5,base);
        //System.out.println(section+" "+remainder);
        // 일단 5개 단위로 4개씩은 1이 있으니 4씩 곱해둔다.
        long answer = section * (long)Math.pow(4,base);
        // 3이후면 그 사이에 0이 있는 구간이 한번 있으니 한번 빼준다.
        if (section >= 3) {
            answer -= (long)Math.pow(4,base);
        }
        //System.out.println(answer);
        
        // 0이 있는 구간이 아니라면 재귀
        if (section == 2) {
            return answer;
        } else {
            return answer + cal(remainder);
        }
    }
}
```
