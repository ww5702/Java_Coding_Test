dfs로 순환하면서 내가 이미 이긴 녀석이 이긴사람도 내가 이기는 구조로 저장한다.   
만약 내가 이긴 사람 + 내가 진 사람이 n-1이라면 순위를 정확하게 알 수 있다.   

```
import java.util.*;
class Solution {
    static boolean[] visited;
    static int[] strongCnt;
    static int[] weakCnt;
    static int cnt;
    public int solution(int n, int[][] results) {
        int answer = 0;
        strongCnt = new int[n+1];
        weakCnt = new int[n+1];
        ArrayList<Integer>[] list = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            list[i] = new ArrayList<>();
        }
        for (int[] result: results) {
            list[result[0]].add(result[1]);
        }
        visited = new boolean[n+1];
        
        for (int i = 1; i <= n; i++) {
            visited = new boolean[n+1];
            cnt = 0;
            dfs(list, i);
            //System.out.println(cnt);
            strongCnt[i] = cnt;
            //System.out.println(Arrays.toString(strongCnt));
            //System.out.println(Arrays.toString(weakCnt));
        }
        
        for (int i = 1; i <= n; i++) {
            answer += (strongCnt[i] + weakCnt[i] == n-1) ? 1 : 0;
        }
        
        return answer;
    }
    public int dfs(ArrayList<Integer>[] list, int n) {
        //System.out.println(list[n].toString());
        visited[n] = true;
        
        for (int next : list[n]) {
            if (!visited[next]) {
                weakCnt[next] += 1;
                cnt += 1;
                dfs(list, next);
            }
        }
        return cnt;
    }
    
    
}
```
좋아요를 가장 많이 받은 풀이이다.   
이 방법은 다익스트라 방법을 사용한 것 같았다.   
경유지를 거쳐서 이동해 카운트를 늘리는 방식인데   
이는 n이 500개 이하일때만 가능하긴하다.   
선수가 100명 이하라서 가능했던거같다.   
하지만 dfs풀이가 당연히 시간이 더 빠르긴하다.   

```
class Solution {
    public int solution(int n, int[][] results) {
        int answer = 0;

        boolean[][] chk = new boolean[n + 1][n + 1];

        for(int i = 0; i < results.length; i++) {
            chk[results[i][0]][results[i][1]] = true;
        }

        for(int k = 1; k < n + 1; k++) {
            for(int i = 1; i < n + 1; i++) {
                for(int j = 1; j < n + 1; j++) {
                    if(i != j && chk[i][k] && chk[k][j]) {
                        chk[i][j] = true;
                    }
                }
            }
        }

        for(int i = 1; i < n + 1; i++) {
            boolean pass = true;
            for(int j = 1; j < n + 1; j++) {
                if(i != j && !(chk[i][j] || chk[j][i])) {
                    pass = false;
                    break;
                }
            }
            if(pass) {
                answer++;
            }
        }

        return answer;
    }
}
```
