주어진 조건 그대로 풀이하니 정확성 테스트는 통과하나   
효율성 테스트가 실패한다.   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    static boolean[] visited;
    public String solution(int n, int k, String[] cmd) {
        String answer = "";
        visited = new boolean[n];
        ArrayList<Integer> list = new ArrayList<>();
        int idx = k;
        
        for (int i = 0; i < cmd.length; i++) {
            String[] now = cmd[i].split(" ");
            String order = now[0];
            //System.out.println(Arrays.toString(now));
            if (order.equals("U")) {
                int cnt = 0;
                while (cnt != Integer.valueOf(now[1])) {
                    if (idx - 1 >= 0 && !visited[idx-1]) {
                        idx -= 1;
                        cnt += 1;
                    } else if (idx - 1 >= 0 && visited[idx-1]) {
                        idx -= 1;
                    } else if (idx == 0) {
                        cnt += 1;
                    }
                }
            } else if (order.equals("D")) {
                int cnt = 0;
                while (cnt != Integer.valueOf(now[1])) {
                    if (idx + 1 < n && !visited[idx+1]) {
                        idx += 1;
                        cnt += 1;
                    } else if (idx + 1 < n && visited[idx+1]) {
                        idx += 1;
                    } else if (idx == n-1) {
                        cnt += 1;
                    }
                }
            } else if (order.equals("C")) {
                visited[idx] = true;
                list.add(idx);
                int lastIdx = idx;
                boolean goUp = false;
                while (true) {
                    if (idx == n-1) {
                        goUp = true;
                        idx = lastIdx;
                        break;
                    }
                    
                    if (idx + 1 < n) {
                        idx += 1;
                    }
                    if (!visited[idx]) {
                        break;
                    }
                }
                
                if (goUp) {
                    while (true) {
                        
                        if (idx-1 >= 0) {
                            idx -= 1;
                        }
                        if (!visited[idx]) {
                            break;
                        }
                    }
                }
                
            } else {
                int lastIdx = list.remove(list.size()-1);
                visited[lastIdx] = false;
            }
            //System.out.println(Arrays.toString(visited));
            //System.out.println(idx);
            //System.out.println(list.toString());
        }
        
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                answer += "O";
            } else {
                answer += "X";
            }
        }
        
        return answer;
    }
}
```
