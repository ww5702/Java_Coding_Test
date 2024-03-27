```
import java.util.*;

class Solution {
    public String[] solution(String[] record) {
        HashMap<String, String> nickname = new HashMap<>();
        List<String> order = new ArrayList<>();
        
        for (String r : record) {
            String[] now = r.split(" ");
            String move = now[0];
            if (move.equals("Change")) {
                nickname.put(now[1], now[2]);
            } else {
                order.add(now[0]+" "+now[1]);
                if (move.equals("Enter")) {
                    nickname.put(now[1], now[2]);
                }
            }
        }
        // System.out.println(order.toString());
        // System.out.println(nickname);
        String[] answer = new String[order.size()];
        int idx = 0;
        for (String o : order) {
            String[] value = o.split(" ");
            String name = nickname.get(value[1]);
            if (value[0].equals("Enter")) {
                answer[idx++] = name+"님이 들어왔습니다.";
            } else {
                answer[idx++] = name+"님이 나갔습니다.";
            }
        }
        return answer;
    }
}
```
