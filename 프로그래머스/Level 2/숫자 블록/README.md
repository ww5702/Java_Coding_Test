소수라면 1이고, 뒷자리부터 시작하여 /2부터 시작이니   
10이라면 5부터 시작하여 5로 나눠진다면 5,   
9이라면 4부터 시작하여 3으로 나눠지니 3   
위와 같이 풀이하였다.   
하지만 시간초과 발생   

```
import java.util.Arrays;
class Solution {
    static boolean[] arr;
    public int[] solution(long begin, long end) {
        int[] answer = new int[(int)end-(int)begin+1];
        arr = new boolean[(int)end+1];
        Arrays.fill(arr,true);
        arr[0] = false;
        arr[1] = false;
        isPrime(end);
        //System.out.println(Arrays.toString(arr));
        
        int idx = answer.length-1;
        for (long i = end; i >= begin; i--) {
            if (arr[(int)i]) {
                answer[idx--] = 1;
            } else {
                long limit = i/2;
                while (limit >= 2) {
                    if (i % limit == 0) {
                        answer[idx--] = (int)limit;
                        break;
                    } else {
                        limit -= 1;
                    }
                }
            }
        }
        
        return answer;
    }
    public void isPrime(long n) {
        if (n >= 4) {
            for (int i = 2; i <= (int)Math.sqrt((double)n); i++) {
                for (int j = 2; j <= n/i; j++) {
                    arr[i*j] = false;
                }
            }
        }
    }
}
```
