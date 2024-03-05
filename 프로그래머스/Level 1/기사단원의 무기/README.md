```
class Solution {
    public int calculate(int number) {
        if (number <= 2) { return number; }
        Double limit = Math.sqrt(number);
        int cnt = 0;
        for (int i = 1; i < limit; i++) {
            if (number % i == 0) {
                cnt += 2;
            }
        }
        if ((double)limit.intValue() == limit) {
            cnt += 1;
        }
        return cnt;
    }
    public int solution(int number, int limit, int power) {
        int answer = 0;
        for (int i = 1; i <= number; i++) {
            int p = calculate(i);
            answer += p > limit ? power : p;
        }
        return answer;
    }
}
```
