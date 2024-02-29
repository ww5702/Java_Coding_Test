```
import java.util.Arrays;
class Solution {
    public static int result = 0;
    public int solution(int[] number) {
        int answer = 0;
        boolean[] visited = new boolean[number.length];
        
        combi(number,visited,0,number.length,3);
        return result;
    }
    
    static void combi(int[] arr, boolean[] visited, int start, int n, int r) {
        if (r == 0) {
            int sum = 0;
            for (int i = 0; i < n; i++) {
                if (visited[i]) {
                    sum += arr[i];
                }
            }
            result += sum == 0 ? 1 : 0;
            return;
        }
        
        for (int i = start; i < n; i++) {
            visited[i] = true;
            combi(arr, visited, i+1, n, r-1);
            visited[i] = false;
        }
        
    }
    
    
}
```
