```
import java.util.*;
import java.util.Arrays;
class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        List<String> pList = new ArrayList<>();
        for (String name : participant) {
            pList.add(name);
        }
        List<String> cList = Arrays.asList(completion);
        
        for (String name : cList) {
            int idx = pList.indexOf(name);
            //System.out.println(idx);
            pList.remove(idx);
        }
        //System.out.println(pList.toString());
        for (String name : pList) {
            answer = name;
        }
        
        
        return answer;
    }
}
```
해시로 풀이하지 않아 시간초과 발생   
하지만 정렬로 한번 풀어볼까 해서 진행
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        Arrays.sort(participant);
        Arrays.sort(completion);
        for (int i = 0; i < completion.length; i++) {
            if (!participant[i].equals(completion[i])) {
                answer = participant[i];
                break;
            }
        }
        if (answer == "") {
            answer = participant[participant.length-1];
        }
        //System.out.println(Arrays.toString(participant));
        //System.out.println(Arrays.toString(completion));
        
        return answer;
    }
}
```
이 또한 풀이가 가능하긴 했으나 문제가 원하는 방향은 아니었다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        HashMap<String, Integer> map = new HashMap<>();
        for (String player : participant) 
            map.put(player, map.getOrDefault(player, 0) + 1);
        for (String player : completion) 
            map.put(player, map.get(player) - 1);
        
        //System.out.println(map);
        for ( Map.Entry<String, Integer> entry : map.entrySet()) {
            if (entry.getValue() != 0) {
                answer = entry.getKey();
                break;
            }
}
        
        
        return answer;
    }
}
```
훨씬 빠르게 풀이가 가능하다.   
