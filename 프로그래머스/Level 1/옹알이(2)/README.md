```
class Solution {
    public int solution(String[] babbling) {
        int answer = 0;
        for (int i = 0; i < babbling.length; i++) {
            String now = babbling[i];
            
            if (now.equals("ayaaya") || now.equals("yeye") || now.equals("woowoo") || now.equals("mama")) { continue; }
            
            now = now.replace("aya", " ");
            now = now.replace("ye", " ");
            now = now.replace("woo", " ");
            now = now.replace("ma", " ");
            now = now.replace(" ", "");
            
            if (now == "") { answer += 1; }
        }
        return answer;
    }
}
```
