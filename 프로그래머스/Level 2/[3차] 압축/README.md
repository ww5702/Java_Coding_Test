```
import java.util.*;
import java.util.stream.*;
class Solution {
    public int[] solution(String msg) {
        String[] arr = msg.split("");
        List<Integer> list = new ArrayList<>();
        HashMap<String, Integer> dictionary = new HashMap<>();
        int lastnum = 1;
        for (int i = 65; i <= 90; i++) {
            dictionary.put(String.valueOf((char)i), lastnum++);
        }
        //System.out.println(dictionary);
        int cnt = 0;
        while (cnt < msg.length()) {
            int idx = 0;
            for (int i = cnt+1; i <= msg.length(); i++) {
                //System.out.println(msg.substring(cnt,i));
                //System.out.println(dictionary.containsKey(msg.substring(cnt,i)));
                if (!dictionary.containsKey(msg.substring(cnt,i))) {
                    list.add(dictionary.get(msg.substring(cnt, i-1)));
                    //System.out.println(msg.substring(cnt, i));
                    dictionary.put(msg.substring(cnt, i), lastnum++);
                    break;
                } else if (i == msg.length()){
                    list.add(dictionary.get(msg.substring(cnt, i)));
                    idx += 1;
                } else {
                    idx += 1;
                }
            }
            cnt += idx;
            //System.out.println(cnt);
        }
        // System.out.println(dictionary);
        // System.out.println(list.toString());
        int[] answer = list.stream().mapToInt(i -> i).toArray();
        return answer;
    }
}
```
