```
class Solution {
    public int solution(int left, int right) {
        int answer = 0;
        for (int i = left; i <= right; i++) {
            answer += Math.sqrt(i) == (double)(int)Math.sqrt(i) ? -1*i : 1*i;
        }
        return answer;
    }
}
```
