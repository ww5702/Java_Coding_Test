```
class Solution {
    public long solution(int a, int b) {
        long big = Math.max(a,b);
        long small = Math.min(a,b);
        //int[] list = IntStream.rangeClosed(small,big).toArray();
        return (big - small + 1) * (small + big) / 2;
    }
}
```
