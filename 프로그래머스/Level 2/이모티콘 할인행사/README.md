dfs로 조합을 이용해 할인가격들을 정해준다.   
할인비율이 충족된다면 구매하고, 총 구매가격이 합산을 넘어갈경우 가입한다.   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    static int[] rates = {10,20,30,40};
    static int[] discount;
    static int[] answer;
    public int[] solution(int[][] users, int[] emoticons) {
        answer = new int[2];
        discount = new int[emoticons.length];
        dfs(users, emoticons, 0, discount, emoticons.length);
        //System.out.println(Arrays.toString(answer));
        return answer;
    }
    
    public void dfs(int[][] users, int[] emoticons, int cnt, int[] discount, int N) {
        if (cnt == N) {
            //System.out.println(Arrays.toString(discount));
            int[] arr = calculate(users, emoticons, discount);
            if (answer[0] < arr[0]) {
                answer[0] = arr[0];
                answer[1] = arr[1];
            } else if (answer[0] == arr[0]) {
                if (answer[1] < arr[1]) {
                    answer[1] = arr[1];
                }
            }
            //System.out.println(Arrays.toString(arr));
            return;
        }
        
        for (int i = 0; i < rates.length; i++) {
            discount[cnt] = rates[i];
            dfs(users, emoticons, cnt+1, discount , N);
        }
    }
    
    public int[] calculate(int[][] users, int[] emoticons, int[] discount) {
        int[] arr = new int[2];
        int emoticonPlus = 0;
        int total = 0;
        for (int i = 0; i < users.length; i++) {
            int limit = users[i][0];
            int sum = users[i][1];
            //System.out.println("현재 "+limit+" "+sum);
            for (int j = 0; j < emoticons.length; j++) {
                if (discount[j] >= limit) {
                    
                    int price = emoticons[j] / 100 * (100-discount[j]);
                    //System.out.println("충족 "+price);
                    sum -= price;
                }
            }
            
            if (sum > 0) {
                total += (users[i][1] - sum);
            } else {
                emoticonPlus += 1;
            }
            
        }   
        arr[0] = emoticonPlus;
        arr[1] = total;
        //System.out.println(emoticonPlus+" "+total);
        return arr;
        
    }
}
```
