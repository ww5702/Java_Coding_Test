```
import java.util.Arrays;
class Solution {
    public int solution(String dartResult) {
        int[] score = new int[3];
        String[] number = {"0","1","2","3","4","5","6","7","8","9","10"};
        int idx = 0;
        int arridx = 0;
        String[] dart = dartResult.split("");
        
        while (idx <= dart.length-1) {
            String cur = dart[idx];
            // 10인 경우
            if (Arrays.asList(number).contains(cur) && dart[idx+1].equals("0")) {
                score[arridx] = 10;
                idx += 1;
            } else if (Arrays.asList(number).contains(cur)) {
                score[arridx] = Integer.valueOf(cur);
            } 
            
            if (cur.equals("S")) {
                score[arridx++] *= 1;
            } else if (cur.equals("D")) {
                score[arridx] = (int)Math.pow(score[arridx++],2); 
            } else if (cur.equals("T")) {
                score[arridx] = (int)Math.pow(score[arridx++],3);
            }
            
            if (cur.equals("*")) {
                for (int i = arridx-2; i <= arridx-1; i++) {
                    System.out.println(i);
                    if (i == -1) { continue; }
                    score[i] *= 2;
                }
            } else if (cur.equals("#")) {
                score[arridx-1] *= -1;
            }
            idx += 1;
            System.out.println(Arrays.toString(score));
        }
        
        System.out.println(Arrays.toString(score));
        return Arrays.stream(score).sum();
    }
}
```
