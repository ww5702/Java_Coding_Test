```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int solution(String[] friends, String[] gifts) {
        /*
        더 많이 준 사람이 다음달에는 받는다
        만약 기록이 없거나 받은 수가 같다면 선물지수가 더 큰사람이 받는다
        */
        int answer = 0;
        int n = friends.length;
        int[][] giftList = new int[n][n];
        for (String gift : gifts) {
            String[] value = gift.split(" ");
            String to = value[0];
            String from = value[1];
            int toIdx = Arrays.asList(friends).indexOf(to);
            int fromIdx = Arrays.asList(friends).indexOf(from);
            giftList[toIdx][fromIdx] += 1;
        }
        //System.out.println(Arrays.deepToString(giftList));
        int[] toFromList = new int[n];
        for (int i = 0; i < n; i++) {
            int toSum = Arrays.stream(giftList[i])
                .sum();
            int fromSum = 0;
            for (int j = 0; j < n; j++) {
                fromSum += giftList[j][i];
            }
            toFromList[i] = toSum - fromSum;
        }
        //System.out.println(Arrays.toString(toFromList));
        
        for (int i = 0; i < n; i++) {
            int cnt = 0;
            for (int j = 0; j < n; j++) {
                if (i == j) { continue; }
                int iGive = giftList[i][j];
                int youGive = giftList[j][i];
                //System.out.println(""+iGive+" "+youGive);
                if (iGive > youGive) {
                    cnt += 1;
                } else if (iGive == youGive) {
                    if (toFromList[i] > toFromList[j]) {
                        cnt += 1;
                    }
                }
            }
            answer = answer < cnt ? cnt : answer;
            //System.out.println(cnt);
        }
        return answer;
    }
}
```
