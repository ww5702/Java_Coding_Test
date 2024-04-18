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
따라서 자기자신을 제외한 약수중 최대값을 return하는 함수를 만들어 풀이해준다.  n이 1인 경우는 0   
n이 소수인 경우는 1    
n의 약수 중 10^7 이하인 가장 큰 수   
로 풀이하면 된다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int[] solution(long begin, long end) {
        int[] answer = new int[(int)(end - begin) + 1];

        for (int i = (int)begin,idx = 0; i <= end; i++) {
            answer[idx++] = calculate(i);
        }

        return answer;
    }


    private static int calculate(int x) {
        System.out.println(x);
        if (x == 1) {
            return 0;
        }

        List<Integer> l = new ArrayList<>();
        for (int i = 2; i <= Math.sqrt(x); i++) {
            
            if (x % i == 0) {
                l.add(i);
                if (x / i <= 10_000_000) {
                    System.out.println("d "+(x/i));
                    return x/i;
                }
            }

        }
        System.out.println(l.toString());
        if (!l.isEmpty()) {
            return l.get(l.size() - 1);
        }

        return 1;
    }
}
```
