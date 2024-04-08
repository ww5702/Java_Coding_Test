char로 순서를 따라가면서 구현한다.   
하나씩 넣어주면서 open을 증가시킨다 물론 )이라면 open을 닫아주고,    
올바른 괄호라면 해당 문자열을 남겨두고 뒤 문자열을 다시 반복   
올바르지 않다면 ( 해당 문자열 ) 을 만들고, 앞 뒤 글자 하나씩 제외한 문자열을 뒤집어준다.   

```
class Solution {
    public String solution(String p) {
        String answer = "";
        return order(p,0);
    }
    private String order(String w, int startChar) {
        if (startChar == w.length()) return "";
        int open = 0;
        int cnt = 0;
        for (int i = startChar; i < w.length(); ++i) {
            char c = w.charAt(i);
            if (c == '(') {
                open++;
                cnt++;
            } else {
                if (open > 0) open--;
                cnt--;
            }
            if (cnt == 0) {
                if (open == 0) {
                    // 올바른 괄호 문자열이라면 그 뒤부터 다시 실행
                    return w.substring(startChar, i + 1) + order(w, i + 1);
                } else {
                    // 아니라면 첫 글자에 (를 붙이고 다시 실행한 결과를 붙인다.
                    // 그리고 )를 붙인다
                    // 그리고 나머지 start+1 ~ from까지 뒤집는다.
                    return "(" + order(w, i + 1) + ")" + reverse(w, startChar + 1, i);
                }
            }
        }
        throw new IllegalArgumentException("the input should only contain parens and open and closing paren should match");
    }
    private String reverse(String w, int from, int to) {
        StringBuilder sb = new StringBuilder();
        for (int i = from; i < to; ++i) {
            sb.append((w.charAt(i) == ')' ? '(' : ')'));
        }
        return sb.toString();
    }
}
```
