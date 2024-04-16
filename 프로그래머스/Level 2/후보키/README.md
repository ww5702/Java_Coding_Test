먼저 조합을 이용해 길이를 1~relation[0].length로 진행하면서 조합을 구해준다.   
조합에 따라 key가 결정된다 ex) 0, 1, 2, 3, 12, 13, 123...   
해당 key를 이용해 String s를 만들어준다.   
key가 01이라면 100ryan, 200apeach등등이다.   
만약 Hashmap에 있던 값이라면 return   
없던 값들이라면 다음 반복문을 진행한다.   
이제 최소성을 확인해봐야한다.   
index0(학번)이 후보키로 만들어져있다고 가정한다.   
key 0,1을 이용하면 유일성은 만족한다.   
하지만 1을 빼면 0은 이미 후보키로 만들어져있으므로 return된다.   
1,2는 최소성도 충족된다.   

```
import java.util.*;
class Solution {
    List<String> candi = new ArrayList<>();
    public int solution(String[][] relation) {
        for (int i = 0; i < relation[0].length; i++) {
            boolean[] visited = new boolean[relation[0].length];
            dfs(visited, 0,0,i+1,relation);
        }
        return candi.size();
    }
    
    public void dfs(boolean[] visited, int start, int depth, int end, String[][] relation) {
        if (depth == end) {
            List<Integer> list = new ArrayList<>();
            String key = "";
            for (int i = 0; i < visited.length; i++) {
                if (visited[i]) {
                    key += String.valueOf(i);
                    list.add(i);
                }
            }
            System.out.println("key "+key.toString());
            Map<String, Integer>map = new HashMap<>();
            
            for (int i = 0; i < relation.length; i++) {
                String s = "";
                for (Integer j : list) {
                    s += relation[i][j];
                }
                System.out.println(s);
                if (map.containsKey(s)) {
                    return;
                } else {
                    map.put(s, 0);
                }
            }
            
            System.out.println(map);
            System.out.println(candi.toString());
            for (String s: candi) {
                System.out.println("후보키 확인 "+key);
                int cnt = 0;
                for (int i = 0; i < key.length(); i++) {
                    String sub = String.valueOf(key.charAt(i));
                    System.out.println(sub);
                    if (s.contains(sub)) cnt ++;
                }
                if (cnt == s.length()) return;
            }
            candi.add(key);
            
            return;
        }
        
        for (int i = start; i < visited.length; i++) {
            if (visited[i]) continue;
            
            visited[i] = true;
            dfs(visited, i, depth+1, end, relation);
            visited[i] = false;
        }
    }
}
```
