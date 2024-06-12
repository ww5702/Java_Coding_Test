dfs와 set을 이용해 풀이했으나   
정확성테스트는 전부 통과했으나 효율성 테스트를 실패   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    static int cnt;
    static int[] arr;
    static Set<String> set;
    public int solution(int n, int[] money) {
        arr = new int[money.length];
        set = new HashSet<>();
        dfs(n, money, arr);
        return set.size() % 1_000_000_007;
    }
    
    public void dfs(int num, int[] money, int[] arr) {
        int[] tempArr = arr.clone();
        if (num == 0) {
            //System.out.println(Arrays.toString(arr));
            String word = "";
            for (int a : arr) {
                word += String.valueOf(a);
            }
            //System.out.println(word);
            set.add(word);
            return;
        }
        
        for (int i = 0; i < money.length; i++) {
            //System.out.println(num+" "+money[i]);
            if (num >= money[i]) {
                tempArr[i] += 1;
                dfs(num-money[i], money, tempArr);
            } else {
                return;
            }
        }
    }
}
```
dp로 풀어 시간을 줄일 수 있다.   
d[i][j] = i개의 화폐(moeny[0..i])로 j 금액을 낼 수 있는 방법 수
d[i][j] = d[i-1][j] + d[i][j-money[i]] 가 된다
즉 에를들어 5원까지 4개의 방법으로 만들수있었고   
6원을 만들거라면   
5원까지 만든 경우의 수 + 1원을 만드는 경우의 수를 더하는 것과 같다.   

 
```
import java.util.Arrays;
import java.util.*;

class Solution {
    public static final int INF = -1;
    
    public int solution(int n, int[] money) {
        int answer = 0;
        Arrays.sort(money);
        
        // variable
        long[] d = new long[n+1];
    
        // 초기화(화폐 한개 지불 방법)
        for(int i =0; i<=n ;i++){
             if(i % money[0] == 0)
                 d[i]=1;
        }
        System.out.println(Arrays.toString(d));
         
        // 화폐단위 개수별로 for문
        for(int i=1; i<money.length ; i++) {
            // 화폐 이전까지의 합 + 새로운 화폐로 낼 수 있는 방법
            for(int j=money[i]; j<=n; j++) {
                d[j] += d[j-money[i]];
            }
        }
        
        System.out.println(Arrays.toString(d));
        
        
        // 형 변환
        answer = (int)(d[n] % 1000000007);
        return answer;
    }
}
```
