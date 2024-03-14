당연히 시간초과 발생   
```
import java.util.Arrays;
class Solution {
    public String[] solution(String[] players, String[] callings) {
        String[] answer = {};
        for (String c : callings) {
            int index = Arrays.asList(players).indexOf(c);
            //System.out.println(index);
            String temp = players[index-1];
            players[index-1] = c;
            players[index] = temp;
            //System.out.println(Arrays.toString(players));
        }
        return players;
    }
}
```
indexOf보다 딕셔너리가 훨씬 빠르다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public String[] solution(String[] players, String[] callings) {
        String[] answer = {};
        HashMap<String, Integer>map = new HashMap<>();
        var idx = 0;
        for (String p : players) {
            map.put(p, idx++);
        }
        //System.out.println(map);
        for (String c : callings) {
            int index = map.get(c);
            String temp = players[index - 1];
            players[index - 1] = players[index];
            players[index] = temp;
            
            map.put(c, index-1);
            map.put(temp, index);
            
            //System.out.println(index);
            //System.out.println(Arrays.toString(players));
        }
        return players;
    }
}
```
