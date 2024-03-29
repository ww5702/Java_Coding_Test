```
import java.util.*;
import java.util.Arrays;
class Solution {
    static int answer;
    static HashSet<Integer> set;
    public int solution(String numbers) {
        answer = 0;
        String[] nums = numbers.split("");
        boolean visited[] = new boolean[nums.length];
        int output[] = new int[nums.length];
        set = new HashSet<Integer>();
        for (int i = 1; i <= nums.length; i++) {
            permutation(nums, output, visited, 0, i);
        }
        Iterator<Integer> iterSet = set.iterator();
        while (iterSet.hasNext()) {
            int input = iterSet.next();
            answer += isPrime(input) ? 1 : 0;
        }
        
        return answer;
    }
    
    public boolean isPrime(int num) {
        if (num == 0) return false;
        if (num == 1) return false;
        Double n = Math.sqrt((double)num);
        for (int i = 2; i <= n; i++) {
            if (num % i == 0) return false;
        }
        
        return true;
    }
    
    public void permutation(String nums[], int output[], boolean[] visited, int depth, int r) {
        if (depth == r) {
            String num = "";
            for (int i = 0; i < r; i++) {
                num += output[i];
            }
            //System.out.println(num);
            set.add(Integer.valueOf(num));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                visited[i] = true;
                output[depth] = Integer.valueOf(nums[i]); 
                permutation(nums, output, visited, depth+1, r);
                visited[i] = false;
            }
        }
    }
}
```
