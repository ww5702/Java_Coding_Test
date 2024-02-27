```
class Solution {
    public long solution(int price, int money, int count) {
        long answer = money;

        for (int cnt = 0; cnt < count; ++cnt) {
            answer -= (price * (cnt + 1));
        }

        return (answer > 0 ? 0 : -answer);
    }
}
```
