레벨2의 요격 시스템과 비슷한 문제이다.   
나오는 시간을 기준으로 오름차순정렬을 진행한다.   
만약 [0]의 나오는 시간이 [1]의 출발시간보다 더 뒤에있다면   
[0]안의 감시카메라로 [1]도 확인이 가능하다는 의미이다.   
하지만 [1]이 들어오는 시간이 [0]이 나가는 시간보다 더 뒤라면 감시카메라를   
새로 달아야 한다.   
```
import java.util.Arrays;

class Solution {
    public int solution(int[][] routes) {
        int answer = 1;
        Arrays.sort(routes, (o1, o2) -> {
           return o1[1] - o2[1];
        });
        System.out.println(Arrays.deepToString(routes));
        int value = routes[0][1];
        for (int i = 1; i < routes.length; i++) {
            int start = routes[i][0];
            int end = routes[i][1];
            if (start > value) {
                value = end;
                answer += 1;
            }
        }
        return answer;
    }
}
```
