```
import java.util.Arrays;
class Solution {
    public String solution(String s, String skip, int index) {
        String answer = "";
        Integer[] skipNum = new Integer[skip.length()];
        for (int i = 0; i < skip.length(); i++) {
            int num = skip.charAt(i);
            skipNum[i] = num;
        }
        //System.out.println(Arrays.toString(skipNum));
        
        for (int i = 0; i < s.length(); i++) {
            int wordNum = s.charAt(i);
            int move = index;
            //System.out.println(wordNum);
            while (move != 0) {
                wordNum += 1;
                if (wordNum >= 123) {
                    wordNum -= 26;
                }
                
                if (!Arrays.asList(skipNum).contains(wordNum)) {
                    move -= 1;
                }
                
            }
            //System.out.println(wordNum);
            if (wordNum >= 123) {
                wordNum -= 26;
            }
            //System.out.println(wordNum);
            //System.out.println((char)wordNum);
            answer += (char)wordNum;
        }
        return answer;
    }
}
```
