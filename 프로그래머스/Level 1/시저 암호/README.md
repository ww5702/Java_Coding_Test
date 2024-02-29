```
class Solution {
    public String solution(String s, int n) {
        String answer = "";
        for (int i = 0; i < s.length(); i++) {
            int now = s.charAt(i);
            
            //System.out.println(now);   
            if (Character.isLowerCase(now)) {
                now = ((now - 97 + n) % 26 + 97);
            } else if (Character.isUpperCase(now)) {
                now = ((now - 65 + n) % 26 + 65);
            }
            //System.out.println();
            answer += (char)now;
        }
        return answer;
    }
}
```
