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
