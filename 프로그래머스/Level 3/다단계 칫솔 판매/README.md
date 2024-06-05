단순하게 반복문으로 풀이하려했으나 시간초과   

```
import java.util.Arrays;
class Solution {
    static int[] result;
    public int[] solution(String[] enroll, String[] referral, String[] seller, int[] amount) {
        result = new int[enroll.length];
        for (int i = 0; i < seller.length; i++) {
            String now = seller[i];
            int cnt = amount[i];
            calcul(enroll, referral, now,cnt*100);
        }
        return result;
    }
    
    public void calcul(String[] enroll, String[] referral, String now, int cnt) {
        while (true) {
            //System.out.println(now+" "+cnt);
            int idx = Arrays.asList(enroll).indexOf(now);
            if (cnt < 10) { 
                result[idx] += cnt;
                break; 
            }
            int youhave = cnt / 10 * 1;
            int ihave = cnt - youhave;
            result[idx] += ihave;
            //System.out.println("나눠가질 "+ihave+" "+youhave);
            
            if (!referral[idx].equals("-")) {
                now = referral[idx];
                cnt = youhave;
                // System.out.println(now+" "+cnt);
                // System.out.println();
            } else {
                break;
            }
            
        } 
        //System.out.println(Arrays.toString(result));
    }
    
}
```
