```
import java.util.Arrays;
class Solution {
    int answer = 0;
    public boolean isPrime(int num) {
        //System.out.println(num);
        if (num == 1) { return false; }
        int n = (int)Math.sqrt(num);
        //System.out.println(n);
        for (int i = 2; i <= n; i++) {
            if (num % i == 0) { return false; }
        }
        return true;
    }
    public void combination(int[] arr, boolean[] visited, int start, int n, int r) {
        if (r == 0) {
            int[] list = new int[3];
            int idx = 0;
            for (int i = 0; i < visited.length; i++) {
                if (visited[i]) {
                    list[idx++] = arr[i];
                }
            }
            //System.out.println(Arrays.toString(list));
            //System.out.println(isPrime(Arrays.stream(list).sum()));
            answer += isPrime(Arrays.stream(list).sum()) ? 1 : 0;
            return;
        }
        
        for (int i = start; i < n; i++) {
            visited[i] = true;
            combination(arr, visited, i+1, n, r-1);
            visited[i] = false;
        }
    }
    public int solution(int[] nums) {
        boolean[] visited = new boolean[nums.length];
        
        combination(nums, visited, 0, nums.length, 3);
        return answer;
    }
}`
```
