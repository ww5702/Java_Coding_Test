```
import java.util.*;
class Solution {
    public String solution(String[] survey, int[] choices) {
        String answer = "";
        HashMap<String, Integer> mbti = new HashMap<>();
        mbti.put("R",0);
        mbti.put("T",0);
        mbti.put("C",0);
        mbti.put("F",0);
        mbti.put("J",0);
        mbti.put("M",0);
        mbti.put("A",0);
        mbti.put("N",0);
        for (int i = 0; i < choices.length; i++) {
            String[] list = survey[i].split("");
            String first = list[0];
            String second = list[1];
            int choice = choices[i];
            
            if (choice < 4) {
                //System.out.println(choice);
                mbti.put(first, mbti.getOrDefault(first, 0) + Math.abs(choice-4));
            } else if(choice > 4) {
                mbti.put(second, mbti.getOrDefault(second, 0) + choice-4);
            }
        }
        
        answer += mbti.get("R") >= mbti.get("T") ? "R" : "T";
        answer += mbti.get("C") >= mbti.get("F") ? "C" : "F";
        answer += mbti.get("J") >= mbti.get("M") ? "J" : "M";
        answer += mbti.get("A") >= mbti.get("N") ? "A" : "N";
        return answer;
    }
}
```
