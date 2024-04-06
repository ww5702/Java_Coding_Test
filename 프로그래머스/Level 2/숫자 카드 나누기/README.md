배열에서 최소의 숫자를 기준으로 약수를 찾는다.   
찾은 약수가 여러개라면 최대를 반환한다.   
반환한 약수가 반대 배열에서 나누어떨어지는지 확인한다.   
안나누어떨어진고 더 크다면 max로 반환한다.   
하지만 중간에 나눠진다면 돌아간다.   

```
import java.util.*;
import java.util.Arrays;

class Solution {
    static int[] arr;
    public int solution(int[] arrayA, int[] arrayB) {
        int answer = 0;
        int aMin = isMin(arrayA);
        int bMin = isMin(arrayB);
        int aGcd = gcd(arrayA, aMin);
        int bGcd = gcd(arrayB, bMin);
        //System.out.println(aGcd+" "+bGcd);
        answer = getAns(arrayB, aGcd, answer);
        answer = getAns(arrayA, bGcd, answer);
        return answer;
    }
    private static int getAns(int[] arr, int gcd, int answer) {
        for (int num : arr) {
            if (num % gcd == 0) {
                return Math.max(answer, 0);
            }
        }
        return Math.max(answer, gcd);
    }
    private static int isMin(int[] arr) {
        return Arrays.stream(arr).min().getAsInt();   
    }
    private static int gcd(int[] array, int min) {
        int result = 1;
        for (int i = 2; i <= min; i++) {
            if (isGcd(array, i)) {
                result = i;
            }
        }
        return result;
    }
    private static boolean isGcd(int[] array, int i) {
        for (int num : array) {
            if (num % i != 0) {
                return false;
            }
        }
        return true;
    }
}
```
