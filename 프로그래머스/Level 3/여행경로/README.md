배열을 조건대로 정렬을 하고 dfs로 순환하였다.   
그렇다면 알파벳순으로 제일 앞에있는 공항을 먼저 방문하게 된다.   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    static boolean[] visited;
    static boolean find;
    static String[] answer;
    public String[] solution(String[][] tickets) {
        visited = new boolean[tickets.length];
        find = false;
        Arrays.sort(tickets, (o1,o2) -> {
            if (o1[0].equals(o2[0])) {
                return o1[1].compareTo(o2[1]);
            } else {
                return o1[0].compareTo(o2[0]);
            }
        });
        HashSet<String> airport = new HashSet<String>();
        for (int i = 0; i < tickets.length; i++) {
            airport.add(tickets[i][0]);
            airport.add(tickets[i][1]);
        }
        
        //System.out.println(Arrays.deepToString(tickets));
        List<String> list = new ArrayList<>();
        list.add("ICN");
        dfs(tickets, "ICN", list);
        
        return answer;
    }
    public void dfs(String[][] tickets, String now, List<String> list) {
        if (find) return;
        
        boolean fin = true;
        for (int i = 0; i < tickets.length; i++) {
            if (!visited[i]) {
                fin = false;
                break;
            }
        }
        
        if (fin) {
            find = true;
            // System.out.println("최종");
            // System.out.println(list.toString());
            answer = new String[list.size()];
            for (int i = 0; i < list.size(); i++) {
                answer[i] = list.get(i);
            }
            return;
        }
        
        for (int i = 0; i < tickets.length; i++) {
            if (tickets[i][0].equals(now) && !visited[i]) {
                //System.out.println(now+" "+ list.toString());
                visited[i] = true;
                List<String> newList = list;
                //System.out.println(newList.toString());
                newList.add(tickets[i][1]);
                dfs(tickets, tickets[i][1], newList);
                visited[i] = false;
                list.remove(list.size()-1);
            }
        }
        
    }
}
```
