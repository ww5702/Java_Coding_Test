구현으로 문제를 풀이하였다.   

```
class Solution {
    public int solution(String s) {
        int answer = s.length()+1;
        for (int i = 1; i <= s.length(); i++) {
            //System.out.println(i);
            String word = "";
            String temp = s.substring(0,i);
            int cnt = 1;
            //System.out.println(temp);
            for (int j = i; j <= s.length()-i; j+=i) {
                //System.out.println(i+" "+j);
                //System.out.println(s.substring(j,j+i));
                if (temp.equals(s.substring(j,j+i))) {
                    cnt += 1;
                } else {
                    if (cnt != 1) {
                        word += String.valueOf(cnt);
                    }
                    word += temp;
                    temp = s.substring(j,j+i);
                    cnt = 1;
                }
            }
            // 나머지 뒷부분
            if (s.length() % i != 0) {
                //System.out.println("남음");
                if (cnt != 1) {
                    word += String.valueOf(cnt);
                }
                word += temp;
                //System.out.println(s.substring(i*(s.length()/i),s.length()));
                word += s.substring(i*(s.length()/i),s.length());
            } else {
                if (cnt != 1) {
                    word += String.valueOf(cnt);
                }
                word += temp;
            }
            //System.out.println(word);
            answer = Math.min(answer, word.length());
        }
        return answer;
    }
}
```
