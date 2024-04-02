```
import java.util.Arrays;
import java.util.*;
import java.util.stream.*;
class Solution {
    public int[] solution(int n) {
        int[][] result = new int[n][n];
        int max = n*(n+1)/2;
        int[] answer = new int[max];
        int num = 1;
        int row = -1, col = 0;
        int i = n, j = 0;
        
        while (i > 0) {
            j = 0;
            while(i > j) {
                row += 1;
                result[row][col] = num++;
                j += 1;
            }
            j = 0;
            while(i-1 > j) {
                col += 1;
                result[row][col] = num++;
                j += 1;
            }
            j = 0;
            while(i-2 > j) {
                row -= 1;
                col -= 1;
                result[row][col] = num++;
                j += 1;
            }
            i -= 3;
        }
        int idx = 0;
        for (int a = 0; a < n; a++) {
            int[] arr = Arrays.stream(result[a]).filter(b -> b != 0).toArray();
            for (int number : arr) {
                answer[idx++] = number;
            }
        }
        return answer;
        /*
        1 2 3 4 5 주루룩(5) 6 5 4 3  n-> 6
        2 3 4 주루룩(2) 5 
        */
    }
}
```
