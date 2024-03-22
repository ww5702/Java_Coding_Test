```
import java.util.Arrays;

class Solution {
    public String solution(int n, int t, int m, int p) {
        String answer = "";
        int num = 0;
        int cnt = 1;
        //011011100
        while (answer.length() <= t) {
            //System.out.println(num);
            String radix = Integer.toString(num++,n);
            String[] arr = radix.split("");
            //System.out.println(Arrays.toString(arr));
            for (String a : arr) {
                if (cnt == p) {
                    answer += a;
                }
                cnt += 1;
                if (cnt > m) { cnt = 1; }
            }
            //System.out.println("정답 : "+answer);
        }
        return answer.toUpperCase().substring(0,t);
    }
}
```
