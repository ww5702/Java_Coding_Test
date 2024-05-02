y좌표로 즉 끝나는 길이까지의 순서로 정렬을 한다.   
x좌표를 확인해서 전에 쐈던 레이저가 닿는 y좌표보다 작을경우 같은 레이저로   
요격이 가능하다.   
하지만 쐈던 레이저가 닿지 못하는 x좌표라면 다시 레이저를 쏴야한다.   
```
import java.util.Arrays;
class Solution {
    public int solution(int[][] targets) {
        int answer = 0;
        Arrays.sort(targets, (o1, o2) -> {
            return o1[1] - o2[1];
        });
        //System.out.println(Arrays.deepToString(targets));
        int s = 0,e = 0;
        for (int[] target: targets) {
            if (target[0] > s) {
                answer += 1;
                s = target[1];
            }
            
        }
        return answer;
    }
}
```
