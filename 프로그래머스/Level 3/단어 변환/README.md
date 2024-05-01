dfs로 백트래킹을 사용하여 단어를 추적하는 문제이다.   
```
class Solution {
    static boolean[] visited;
    static int answer;
    public int solution(String begin, String target, String[] words) {
        answer = 51;
        visited = new boolean[words.length];
        
        dfs(words, begin, target, 0);
        //System.out.println(calculate(begin, "hot"));
        return answer == 51 ? 0 : answer;
    }
    
    public void dfs(String[] words, String now, String target, int cnt) {
        if (cnt > answer) { return; }
        if (now.equals(target)) {
            //System.out.println(now+" "+cnt);
            answer = Math.min(cnt, answer);
            return;
        }
        for (int i = 0; i < words.length; i++) {
            int num = calculate(now, words[i]);
            if (!visited[i] && num == 1) {
                visited[i] = true;
                dfs(words, words[i], target, cnt+1);
                visited[i] = false;
            }
        }
    }
    
    
    public int calculate(String str1, String str2) {
        int cnt = 0;
        for (int i = 0; i < str1.length(); i++) {
            cnt += str1.charAt(i) != str2.charAt(i) ? 1 : 0;
        }
        return cnt;
    }
}
```
좋아요를 가장 많이 받은 문제풀이이다.   
풀이 방식은 같으나 나와 다른점이라면 나는 뒤에 단어를 먼저 교환하고   
돌아올 수 있도록 풀이하였다.   
```
import java.util.LinkedList;
import java.util.Queue;

class Solution {

    static class Node {
        String next;
        int edge;

        public Node(String next, int edge) {
            this.next = next;
            this.edge = edge;
        }
    }

    public int solution(String begin, String target, String[] words) {
        int n = words.length, ans = 0;

        // for (int i=0; i<n; i++)
        //  if (words[i] != target && i == n-1) return 0;

        Queue<Node> q = new LinkedList<>();


        boolean[] visit = new boolean[n];
        q.add(new Node(begin, 0));

        while(!q.isEmpty()) {
            Node cur = q.poll();
            if (cur.next.equals(target)) {
                ans = cur.edge;
                break;
            }

            for (int i=0; i<n; i++) {
                if (!visit[i] && isNext(cur.next, words[i])) {
                    visit[i] = true;
                    q.add(new Node(words[i], cur.edge + 1));
                }
            }
        }

        return ans;
    }

    static boolean isNext(String cur, String n) {
        int cnt = 0;
        for (int i=0; i<n.length(); i++) {
            if (cur.charAt(i) != n.charAt(i)) {
                if (++ cnt > 1) return false;
            }
        }

        return true;
    }    
}


```
