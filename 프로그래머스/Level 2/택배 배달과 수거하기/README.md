무조건 최대한 멀리 갔다 오면서 배달 및 수거하는게 최소값이었다.   
테스트 케이스가 실패하는 경우가 있었는데   
입력값 〉 3, 2, [2, 4], [4, 2]   
기댓값 〉 8   
이었는데 처음 maxNum을 n으로 설정하고 반복문시 maxNum을 i-1로 받아서   
생기는 문제였다.   
```
import java.util.Arrays;
class Solution {
    public long solution(int cap, int n, int[] deliveries, int[] pickups) {
        long answer = 0;
        /*
        1 0 2 0 1 0 2
        0 2 0 1 0 2 0
        
        7 7 5 5 3 3
        14 10 6
        무조건 최대한 멀리 갔다 오면서 수거도 해오는게 이득
        */
        int maxNum = n-1;
        while (true) {
            int idx = -1;
            for (int i = maxNum; i >= 0; i--) {
                if (deliveries[i] != 0 || pickups[i] != 0) {
                    idx = i;
                    maxNum = i;
                    break;
                }
            }
            //System.out.println(idx);
            // 다 돌때까지
            if (idx == -1) break;
            
            int temp = cap;
            for (int i = idx; i >= 0; i--) {
                if (deliveries[i] > temp) {
                    deliveries[i] -= temp;
                    break;
                } else {
                    temp -= deliveries[i];
                    deliveries[i] = 0;
                }
            }
            temp = cap;
            for (int i = idx; i >= 0; i--) {
                if (pickups[i] > temp) {
                    pickups[i] -= temp;
                    break;
                } else {
                    temp -= pickups[i];
                    pickups[i] = 0;
                }
            }
            //System.out.println(Arrays.toString(deliveries));
            //System.out.println(Arrays.toString(pickups));
            answer += ((idx+1)*2);
        }
        
        return answer;
    }
}
```
위의 문제를 더 쉽게 표현하면 이와 같다.   
뒤에서부터 접근하면서 배달하거나 수거해야하는 상자수를 정해준다.   
이 상자들이 사라질때까지 반복하면서 cap만큼 빼준다.   
훨씬 빠르게 풀이가 가능하다.   

```
import java.util.Arrays;
class Solution {
    public long solution(int cap, int n, int[] deliveries, int[] pickups) {
        long answer = 0;
        int deliver = 0, pickup = 0;
        for(int i = n-1; i >= 0; i--){
            deliver += deliveries[i];
            pickup += pickups[i];
            while (deliver > 0 || pickup > 0){
                deliver -= cap;
                pickup -= cap;
                answer += ((i+1) * 2);
            }

        }
        return answer;
    }
}
```
