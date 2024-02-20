```
class Solution {
    public int solution(int n) {
        int answer = 0;
        double sqrtnum = Math.sqrt(n);
        for (int i = 1; i < (int)sqrtnum; i++) {
            if (n%i == 0) {
                answer += (n/i);
                answer += i;
            }
        }
        if ((double)(int)sqrtnum == sqrtnum) {
            answer += (int)sqrtnum;
        }
        return answer;
    }
}
```
