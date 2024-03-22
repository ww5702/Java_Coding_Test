간단한 dfs문제이다.   
```
class Solution {
    public int solution(int[] numbers, int target) {
        int answer = dfs(0, numbers, 0, target);
        return answer;
    }
    
    int dfs(int n, int[] numbers, int sum, int target) {
        if (n == numbers.length) {
            return sum == target ? 1 : 0;
        }
        
        return dfs(n+1, numbers, sum + numbers[n], target) + dfs(n+1, numbers, sum - numbers[n], target);
    }
}
```
