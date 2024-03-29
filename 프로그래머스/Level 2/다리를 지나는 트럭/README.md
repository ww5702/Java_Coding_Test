다리와 트럭을 큐로 구현해준다.   
구현한 다리가 빌때까지 실행한다.   
0 0 이라고 가정하자   
7이 들어오려고 한다.   
맨앞 0이 나가고, 제한무게 - 0 을 해준다.   
truck이 비지 않았다면 맨앞 트럭의 크기를 t로 두고   
다리무게 제한을 넘기지않았다면 맨뒤에 t가 들어오고,   
제한을 넘겨서 아무도 못들어간다면 0이 들어간다.   
계속 반복하다보면   
트럭들이 나가고 마지막 트럭이 들어간다.   
0 6   
1초가 지나면 0이 나가고 6만 남는다.   
대기트럭에 아무런 트럭도 남지 않았으므로 0도 들어오지 않는다.   
다시 1초가 지나고 6이 나간다.   

```
import java.util.*;
class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int answer = 0;
        Queue<Integer> bridge = new LinkedList<>();
        Queue<Integer> truck = new LinkedList<>();
        int limit = 0;
        for (int i = 0; i < bridge_length; i++) {
            bridge.add(0);
        }
        for (int t : truck_weights) {
            truck.add(t);
        }
        while (!bridge.isEmpty()) {
            answer += 1;
            // 맨 앞에 나가기
            limit -= bridge.poll();
            if (!truck.isEmpty()) {
                int t = truck.peek();
                // 더 올라갈 수 있으면
                if (t + limit <= weight) {
                    limit += t;
                    bridge.add(truck.poll());
                } else {
                // 없다면 진행
                    bridge.add(0);
                }
            }
        }
        return answer;
    }
}
```
