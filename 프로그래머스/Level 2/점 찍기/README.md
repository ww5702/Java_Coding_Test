반지름이 d인 원이 있다고 가정하고,   
x좌표를 늘려가면서 찍을수 있는 점의 개수를 구해준다.   
```
class Solution {
    public long solution(int k, int d) {
        long answer = 0;
        long dPow = (long) d*d;
        for(long i=0; i<=d; i+=k){
            long sPow = (long) i*i;
            answer += (long) Math.sqrt(dPow-sPow)/k+1;
        }
        return answer;
    }
}
```
