친구수가 8명밖에 안되서   
조합처럼 배치를 구한 뒤   
해당 조건을 만족시키는지 확인해본다.   
```
import java.util.Arrays;
class Solution {
    static char[] arr;
    static boolean[] visited;
    static int answer;
    static String[] dt;
    public int solution(int n, String[] data) {
        arr = new char[] {'A','C','F','J','M','N','R','T'};
        answer = 0;
        dt = data;
        visited = new boolean[8];
        
        dfs(0, "");
        
        return answer;
    }
    
    public void dfs(int depth, String line) {
        if (depth == 8) {
            answer += check(line) ? 1 : 0;
            return;
        }
        
        for (int i = 0; i < 8; i++) {
            if (!visited[i]) {
                visited[i] = true;
                dfs(depth+1, line+arr[i]);
                visited[i] = false;
            }
            
        }
        
    }
    
    public boolean check(String line) {
        for (int i = 0; i < dt.length; i++) {
            String[] d = dt[i].split("");
            //System.out.println(Arrays.toString(d));
            int firstIdx = line.indexOf(d[0]);
            int secondIdx = line.indexOf(d[2]);
            int diff = (Math.abs(firstIdx - secondIdx)-1);
            //System.out.println(firstIdx+" "+secondIdx);
            if (d[3].equals("=")) {
                if (diff != Integer.valueOf(d[4])) {
                    return false;   
                }
            } else if(d[3].equals("<")) {
                if (diff >= Integer.valueOf(d[4])) {
                    return false;
                }
            } else {
                if (diff <= Integer.valueOf(d[4])) {
                    return false;
                }
            }
        }
        
        return true;
    }
    
}
```
