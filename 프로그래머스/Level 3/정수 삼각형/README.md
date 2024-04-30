전형적인 dp문제이다.   
열이 0과 마지막 index가 아니면 비교해서 max값을 넣어준다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(int[][] triangle) {
        int answer = 0;
        int[][] dp = new int[triangle.length][triangle[triangle.length-1].length];
        // for (int i = 0; i < triangle.length; i++) {
        //     System.out.println(Arrays.toString(triangle[i]));
        // }
        dp[0][0] = triangle[0][0];
        for (int i = 1; i < triangle.length; i++) {
            for (int j = 0; j <= i; j++) {
                if (j == 0) {
                    dp[i][j] = dp[i-1][j] + triangle[i][j];
                } else if (j == i) {
                    //System.out.println(i+" "+j);
                    dp[i][j] = dp[i-1][j-1] + triangle[i][j];
                } else {
                    dp[i][j] = Math.max(dp[i-1][j-1], dp[i-1][j]) + triangle[i][j];
                }
                
            }
        }
        
        // for (int i = 0; i < triangle.length; i++) {
        //     System.out.println(Arrays.toString(dp[i]));
        // }
        
        return Arrays.stream(dp[triangle.length-1]).max().getAsInt();
    }
}
```

좋아요가 가장 많은 풀이   
dp를 만들지 않고, triangle 배열 자체에 내려가면서 값을 변경시켜주었다.   
```
import java.util.*;
class Solution {
    public int solution(int[][] triangle) {
        for (int i = 1; i < triangle.length; i++) {
            triangle[i][0] += triangle[i-1][0];
            triangle[i][i] += triangle[i-1][i-1];
            for (int j = 1; j < i; j++) 
                triangle[i][j] += Math.max(triangle[i-1][j-1], triangle[i-1][j]);
        }

        return Arrays.stream(triangle[triangle.length-1]).max().getAsInt();
    }
}
```
