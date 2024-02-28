```
class Solution {
    public int solution(String t, String p) {
        int answer = 0;
        for (int i = 0; i <= t.length()-p.length(); i++) {
            Long num1 = Long.valueOf(t.substring(i,i+p.length()));
            answer += num1 <= Long.valueOf(p) ? 1 : 0;
            //System.out.println(t.substring(i,i+p.length()));
        }
        return answer;
    }
}
```
