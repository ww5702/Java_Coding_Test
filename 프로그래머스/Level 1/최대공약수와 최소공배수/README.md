```
class Solution {
    public int[] solution(int n, int m) {
        int[] answer = new int[2];
        // 최대공약수
        answer[0] = gcd(Math.min(n,m),Math.max(n,m));
        // 최소공배수
        answer[1] = n*m/answer[0];
        return answer;
    }
    public static int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a%b);
    }
}
```
