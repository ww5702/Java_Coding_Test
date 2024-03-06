```
class Solution {
    public int solution(int n, int m, int[] section) {
        int answer = 1;
        int limit = section[0] + m - 1;
        for (int i = 1; i < section.length; i++) {
            if (section[i] <= limit) { continue; }
            else {
                answer += 1;
                limit = section[i] + m - 1;
            }
        }
        return answer;
    }
}
```
