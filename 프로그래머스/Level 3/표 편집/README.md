주어진 조건 그대로 풀이하니 정확성 테스트는 통과하나   
효율성 테스트가 실패한다.   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    static boolean[] visited;
    public String solution(int n, int k, String[] cmd) {
        String answer = "";
        visited = new boolean[n];
        ArrayList<Integer> list = new ArrayList<>();
        int idx = k;
        
        for (int i = 0; i < cmd.length; i++) {
            String[] now = cmd[i].split(" ");
            String order = now[0];
            //System.out.println(Arrays.toString(now));
            if (order.equals("U")) {
                int cnt = 0;
                while (cnt != Integer.valueOf(now[1])) {
                    if (idx - 1 >= 0 && !visited[idx-1]) {
                        idx -= 1;
                        cnt += 1;
                    } else if (idx - 1 >= 0 && visited[idx-1]) {
                        idx -= 1;
                    } else if (idx == 0) {
                        cnt += 1;
                    }
                }
            } else if (order.equals("D")) {
                int cnt = 0;
                while (cnt != Integer.valueOf(now[1])) {
                    if (idx + 1 < n && !visited[idx+1]) {
                        idx += 1;
                        cnt += 1;
                    } else if (idx + 1 < n && visited[idx+1]) {
                        idx += 1;
                    } else if (idx == n-1) {
                        cnt += 1;
                    }
                }
            } else if (order.equals("C")) {
                visited[idx] = true;
                list.add(idx);
                int lastIdx = idx;
                boolean goUp = false;
                while (true) {
                    if (idx == n-1) {
                        goUp = true;
                        idx = lastIdx;
                        break;
                    }
                    
                    if (idx + 1 < n) {
                        idx += 1;
                    }
                    if (!visited[idx]) {
                        break;
                    }
                }
                
                if (goUp) {
                    while (true) {
                        
                        if (idx-1 >= 0) {
                            idx -= 1;
                        }
                        if (!visited[idx]) {
                            break;
                        }
                    }
                }
                
            } else {
                int lastIdx = list.remove(list.size()-1);
                visited[lastIdx] = false;
            }
            //System.out.println(Arrays.toString(visited));
            //System.out.println(idx);
            //System.out.println(list.toString());
        }
        
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                answer += "O";
            } else {
                answer += "X";
            }
        }
        
        return answer;
    }
}
```
따라서 연결리스트로 문제를 풀이해야 한다.   
next와 cur, prev을 이용해   
사라진 노드들을 서로 이어준다.   
```
import java.util.*;
import java.util.Arrays;
public class Node{
    int pre, cur, nxt;
        
    public Node(int pre, int cur, int nxt) {
        this.pre = pre;
        this.cur = cur;
        this.nxt = nxt;
    }
}

class Solution {
    public String solution(int n, int k, String[] cmd) {
        int[] pre = new int[n];
        int[] next = new int[n];
        for (int i = 0; i < n; i++) {
            pre[i] = i-1;
            next[i] = i+1;
        }
        next[n-1] = -1;
        //System.out.println(Arrays.toString(pre));
        //System.out.println(Arrays.toString(next));
        
        Stack<Node> stack = new Stack<>();
        StringBuilder sb = new StringBuilder("O".repeat(n));
        for (int i = 0; i < cmd.length; i++) {
            //System.out.println(Arrays.toString(pre));
            //System.out.println(Arrays.toString(next));
            char c = cmd[i].charAt(0);
            if (c == 'U') {
                int num = Integer.valueOf(cmd[i].substring(2));
                while(num-- > 0) {
                    k = pre[k];
                }
            } else if (c == 'D') {
                int num = Integer.valueOf(cmd[i].substring(2));
                while(num-- > 0) {
                    k = next[k];
                }
            } else if (c == 'C') {
                stack.push(new Node(pre[k], k, next[k]));
                if(pre[k] != -1) next[pre[k]] = next[k];
                if(next[k] != -1) pre[next[k]] = pre[k];
                sb.setCharAt(k, 'X');
                
                if(next[k] != -1) k = next[k];
                else k = pre[k];
            } else {
                Node node = stack.pop();
                if(node.pre != -1) next[node.pre] = node.cur;
                if(node.nxt != -1) pre[node.nxt] = node.cur;
                sb.setCharAt(node.cur, 'O');
            }
            
            //System.out.println("이동");
            //System.out.println(Arrays.toString(pre));
            //System.out.println(Arrays.toString(next));
            //System.out.println(k);
        }
        
        return sb.toString();
    }
}
```
좋아요를 가장 많이 받은 풀이 또한 연결리스트로 풀이하였다.   
