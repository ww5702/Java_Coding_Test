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
좋아요를 가장 많이 받은 풀이   
stack을 이용해 방문하지 않은 장소면서 출발지가 같으면 추가 형식으로   
res를 만든다. 그리고 res를 result 배열에 추가해준다.   
그리고 만든 result배열을 알파벳 순으로 정렬한다.   
풀이방식은 같으나 먼저 정렬을 하는 내 방법이 더 빠르게 풀이가 가능했다.   
```
import java.util.*;

class Solution {
    List<Stack<String>> result;
    String[][] tickets;

    public String[] solution(String[][] tickets) {
        result = new ArrayList<>();
        this.tickets = tickets;

        boolean[] visited = new boolean[tickets.length];
        Stack<String> st = new Stack<>();
        st.push("ICN");

        dfs(visited, st, 0);

        if (result.size() > 1) {
            Collections.sort(result, new Comparator<Stack<String>>() {
                @Override
                public int compare(Stack<String> o1, Stack<String> o2) {
                    for (int i = 0; i < o1.size(); i++) {
                        String s1 = o1.get(i);
                        String s2 = o2.get(i);

                        if (!s1.equals(s2)) {
                            return s1.compareTo(s2);
                        }
                    }

                    return 0;
                }
            });
        }

        Stack<String> res = result.remove(0);
        String[] answer = new String[res.size()];

        for (int i = 0; i < answer.length; i++) {
            answer[i] = res.get(i);
        }

        return answer;
    }

    public void dfs(boolean[] visited, Stack<String> st, int len) {
        if (len == tickets.length) {
            Stack<String> res = new Stack<>();
            for (String s : st) {
                res.push(s);
            }

            result.add(res);
            return;
        }

        String arrive = st.peek();

        for (int i = 0; i < tickets.length; i++) {
            String[] tic = tickets[i];

            if (!visited[i] && arrive.equals(tic[0])) {
                st.push(tic[1]);
                visited[i] = true;

                dfs(visited, st, len + 1);

                visited[i] = false;
                st.pop();
            }
        }
    }
}
```
