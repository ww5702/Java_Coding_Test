```
class Solution {
    public int fibo(int n) {
        int[] arr = new int[n+1];
        arr[0] = 0;
        arr[1] = 1;
        for (int num = 2; num <= n; num++) {
            arr[num] = (arr[num-1]+arr[num-2])%1234567;
        }
        return arr[n];
    }
    public int solution(int n) {
        return fibo(n);
    }
}
```
