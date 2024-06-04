처음에는 백트래킹으로 풀이하려고 했으나 메모리 초과   

```
import java.util.Arrays;
import java.util.*;
import java.util.stream.*;

class Solution {
    static boolean[] visited;
    static List<Integer> arr;
    public int solution(int[] a) {
        int answer = 0;
        arr = new ArrayList<>();
        for (int i = 0; i < a.length; i++) {
            arr.add(a[i]);
        }
        List<Integer> copyList = new ArrayList<>(arr);
        visited = new boolean[a.length];
        dfs(copyList, true);
        
        for (int i = 0; i < visited.length; i++) {
            if (visited[i]) answer += 1;
        }
        
        return answer;
    }
    
    public void dfs(List<Integer> list, boolean chance) {
        if (list.size() == 1) {
            int idx = arr.indexOf(list.get(0));
            visited[idx] = true;
            return;
        }
        
        for (int i = 0; i < list.size()-1; i++) {
            // 더 작은값 제거 가능?
            if (chance) {
                if (list.get(i) < list.get(i+1)) {
                    List<Integer> temp = new ArrayList<>(list);
                    temp.remove(i);
                    dfs(temp, false);
                } else {
                    List<Integer> temp = new ArrayList<>(list);
                    temp.remove(i+1);
                    dfs(temp, false);
                }
            }
            //원래는 더 큰값만 제거
            if (list.get(i) < list.get(i+1)) {
                List<Integer> temp = new ArrayList<>(list);
                temp.remove(i+1);
                dfs(temp, chance);
            } else {
                List<Integer> temp = new ArrayList<>(list);
                temp.remove(i);
                dfs(temp, chance);
            }
        }
        
    }
}
```
