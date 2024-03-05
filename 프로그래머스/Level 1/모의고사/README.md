```
import java.util.*;
class Solution {
    public int[] solution(int[] answers) {
        int a = 0, b = 0, c = 0;
        int aIdx = 0, bIdx = 0, cIdx = 0;
        int[] aAnswer = {1,2,3,4,5};
        int[] bAnswer = {2,1,2,3,2,4,2,5};
        int[] cAnswer = {3,3,1,1,2,2,4,4,5,5};
        for (int i = 0; i < answers.length; i++) {
            if (answers[i] == aAnswer[aIdx++]) {
                a += 1;
            } 
            if (answers[i] == bAnswer[bIdx++]) {
                b += 1;
            }
            if (answers[i] == cAnswer[cIdx++]) {
                c += 1;
            }
            
            if (aIdx == aAnswer.length) { aIdx = 0; }
            if (bIdx == bAnswer.length) { bIdx = 0; }
            if (cIdx == cAnswer.length) { cIdx = 0; }
        }
        int max = Math.max(Math.max(a,b),c);
        List<Integer> list = new ArrayList<>();
        if (a == max) { list.add(1); }
        if (b == max) { list.add(2); }
        if (c == max) { list.add(3); }
        int[] answer = list.stream().mapToInt(i -> i).toArray();
        return answer;
    }
}
```
