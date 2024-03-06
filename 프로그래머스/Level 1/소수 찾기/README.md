```
class Solution {
    public boolean isPrime(int n) {
        if (n == 1) { return false; }
        Double num = Math.sqrt(n);
        
        for (int i = 2; i < num; i++) {
            if (n % i == 0) { return false; }
        }
        if ((double)num.intValue() == num) {
            return false;
        }

        return true;
    }
    public int solution(int n) {
        int answer = 0;
        for (int i = 1; i <= n; i++) {
            answer += isPrime(i) ? 1 : 0;
        }
        return answer;
    }
}
```
