주어진 말 그대로   
사이클이 되는 박스들을 모아서 해당 그룹의 갯수를 정렬한 뒤   
곱해주어 반환해주는 문제이다.   
예외의 경우는 모두 한사이클이 형성되어 정답이 0이 되는 경우이다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    static boolean[] visited;
    public int solution(int[] cards) {
        int answer = 0;
        List<Integer> list = new ArrayList<>();
        visited = new boolean[cards.length+1];
        
        for (int i = 1; i <= cards.length; i++) {
            if (!visited[i]) {
                int[] arr = bfs(i, cards);
                System.out.println(Arrays.toString(arr));
                list.add(arr.length);
            }
            
        }
        System.out.println(list.toString());
        Collections.sort(list, Collections.reverseOrder());
        if (list.size() == 1) { return 0; }
        else { return list.get(0) * list.get(1); }
    }
    public int[] bfs(int start, int[] cards) {
        List<Integer> arr = new ArrayList<>();
        visited[start] = true;
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        while (!q.isEmpty()) {
            int now = q.poll();
            arr.add(now);
            if (!visited[cards[now-1]]) {
                q.add(cards[now-1]);
                visited[cards[now-1]] = true;
            }
        }
        return arr.stream().mapToInt(i -> i).toArray();
    }
}
```
