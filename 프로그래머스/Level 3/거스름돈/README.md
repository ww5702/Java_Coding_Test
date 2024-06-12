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
