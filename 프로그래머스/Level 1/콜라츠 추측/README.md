int 와 long의 차이점   
```
class Solution {
    public int solution(int num) {
        Long n = Long.valueOf(num);
        int answer = 0;
        while (n != 1) {
            answer += 1;
            if (n%2 == 0) {
                n /= 2;
            } else {
                n *= 3;
                n += 1;
            }
            if (answer == 500) { break; }
        }
        return answer == 500 ? -1 : answer;
    }
}
```
