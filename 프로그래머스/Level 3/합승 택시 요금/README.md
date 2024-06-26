n이 200밖게 안되기에 플로이드워셜 알고리즘으로 문제를 풀이할 수 있다.   
각 출발지에서 각 목표지점까지 최소 거리를 구해둔다.   
그리고 3중 반복문을 통해 i -> j까지 가는 거리를 i -> x + x -> a + x -> b   
이렇게 나눠서 구해준다.   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    static int[][] fee;
    public int solution(int n, int s, int a, int b, int[][] fares) {
        
        int[][] fee = new int[n+1][n+1];
        for (int i = 1; i <= n; i++) {
            Arrays.fill(fee[i], 20000001);
            fee[i][i] = 0;
        }    
        
        for (int[] fare : fares) {
            fee[fare[0]][fare[1]] = fare[2];
            fee[fare[1]][fare[0]] = fare[2];
        }
        
        for (int k = 1; k <= n; k++) {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    fee[i][j] = Math.min(fee[i][j], (fee[i][k] + fee[k][j]));
                }
            }
        }
        
//         for (int i = 1; i <= n; i++) {
//             System.out.println(Arrays.toString(fee[i]));
//         }
        int answer = fee[s][a] + fee[s][b];
        for (int i = 1; i <= n; i++) {
            answer = Math.min(answer, (fee[s][i] + fee[i][a] + fee[i][b]));
        }
        
        return answer;
    }
}
```
