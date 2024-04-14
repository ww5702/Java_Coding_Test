유클리드 호제법을 사용한다.
```
class Solution {
    public long solution(int w, int h) {
        return (((long)w*(long)h) - ((long)w+(long)h-gcd(Math.min(w,h), Math.max(w,h))));
    }
    public static long gcd(int a, int b) {
        if (b == 0) { return a; }
        return gcd(b, a%b);
    }
}
```
