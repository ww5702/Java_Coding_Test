user_id배열이 8까지밖에 없어서 쉽게 풀이가 가능했다.   
dfs를 사용하여 밴리스트와 일치하다면 재귀하였다.   
최종적으로 hashset을 이용하여 중복을 제거하고 개수를 파악했다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    static boolean[] visited;
    Set<String> hashSet;
    public int solution(String[] user_id, String[] banned_id) {
        int answer = 0;
        visited = new boolean[user_id.length];
        hashSet = new HashSet<>();
        
        dfs(user_id, banned_id, 0);
        return hashSet.size();
    }
    
    public void dfs(String[] user_id, String[] banned_id, int index) {
        if (index >= banned_id.length) {
            String answer = "";
            for (int i = 0; i < user_id.length; i++) {
                if (visited[i]) {
                    answer += user_id[i];
                }
            }
            hashSet.add(answer);
            return;
        }
        
        
        for (int i = index; i < banned_id.length; i++) {
            //System.out.println(banned_id[i]);
            for (int j = 0; j < user_id.length; j++) {
                //System.out.println(banned_id[i]+" "+user_id[j]);
                // 길이가 다르면 pass
                if (banned_id[i].length() != user_id[j].length()) { continue; }
                // 만약 방문하지 않았으면서 같은지 확인
                if (!visited[j]) {
                    if (checkOk(user_id[j], banned_id[i])) {
                        //System.out.println("통과");
                        visited[j] = true;
                        dfs(user_id, banned_id, index+1);
                        visited[j] = false;
                    }
                }
            }
            return;
        }
        
    }

    public boolean checkOk(String user, String ban) {
        for (int i = 0; i < user.length(); i++) {
            if (ban.charAt(i) == '*') { continue; }
            if (user.charAt(i) != ban.charAt(i)) {
                return false;
            }
        }
        
        return true;
    }
}
```
좋아요를 가장 많이 받은 풀이이다.   
풀이방식은 같았으나 bit masking을 사용하여 풀이하였다.   
banned_id를 *를 제외하고 만들어 matches를 이용해 같은지 확인한다.   
[\\w\\d]는 알파벳 소문자 or 0~9 숫자가 있는지 라는 뜻이다.   
```

import java.util.HashSet;
import java.util.Set;

public class Solution {

    Set<Integer> set;

    public int solution(String[] user_id, String[] banned_id) {
        set = new HashSet<>();

        go(0, user_id, banned_id, 0);

        return set.size();
    }

    public void go(int index, String[] user_id, String[] banned_id, int bit) {

        if(index == banned_id.length) {
            set.add(bit);
            return;
        }

        String reg = banned_id[index].replace("*", "[\\w\\d]");
        for(int i=0; i<user_id.length; ++i) {
            if((((bit>>i) & 1) == 1) || !user_id[i].matches(reg)) continue;
            go(index + 1, user_id, banned_id, (bit | 1<<i));
        }

    }

}

```
