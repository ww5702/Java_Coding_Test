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
mapping하여 parent관계를 정립한뒤, 값을 더해준다.   

```
import java.util.*;
class Solution {
    Map<String, String> parent = new HashMap<>();
    Map<String, Integer> money = new HashMap<>();

    public int[] solution(String[] enroll, String[] referral, String[] seller, int[] amount) {
        for (int i = 0; i < enroll.length; i++) {
            parent.put(enroll[i], referral[i]);
        }

        for (int i = 0; i < seller.length; i++) {
            share(seller[i], amount[i] * 100);
        }
        
        int[] result = new int[enroll.length];
        for (int i = 0; i < enroll.length; i++) {
            result[i] = money.getOrDefault(enroll[i], 0);
        }

        return result;
    }

    void share(String node, int sales) {
        int nextSales = sales / 10;
        money.put(node, money.getOrDefault(node, 0) + sales - nextSales);

        if (nextSales > 0 && parent.containsKey(node)) {
            share(parent.get(node), nextSales);
        }
    }
}
```
