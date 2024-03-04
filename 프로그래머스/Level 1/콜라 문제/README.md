```
class Solution {
    public int solution(int a, int b, int n) {
        int answer = 0;
        while (n >= a) {
            int cnt = (b*(n/a));
            answer += cnt;
            int newCoke = (b*(n/a));
            int remainCoke = (n%a);
            
            n = newCoke + remainCoke;
            //System.out.println(n);
        }
        return answer;
    }
}
```
