혹 다 맞는거 같은데 런타임 에러가 발생한다면   
무조건 int -> long을 의심해봐라   
string을 int로 바꾸는 과정에서 overflow발생   
```
import java.util.Arrays;
class Solution {
    public int solution(int n, int k) {
        int answer = 0;
        String radix = Integer.toString(n,k);
        String[] arr = radix.split("0");
        for (String a : arr) {
            Long num = Long.valueOf(0);
            if (!a.equals("")) {
                num = Long.parseLong(a);
            }
            
            if (num != 0) {
                // System.out.println(num);
                // System.out.println(isPrime(num));
                answer += isPrime(num) ? 1 : 0;
            }
        }
        return answer;
    }
    
    public boolean isPrime(Long n) {
        if (n == 1) return false;
        double num = Math.sqrt(n);
        for (long i = 2; i <= (long)num; i++) {
            if (n % i == 0) { return false;}
        }
        
        return true;
    }
}
```
