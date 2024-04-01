4분면에 따라 dfs반복   
```
class Solution {
    static int[] answer;
    public int[] solution(int[][] arr) {
        answer = new int[2];
        dfs(arr, 0, 0, arr[0].length);
        return answer;
    }
    public void dfs(int[][] arr, int y, int x, int n) {
        int value = arr[y][x];
        for (int i = y; i < y+n; i++){
            for (int j = x; j < x+n; j++) {
                if (value != arr[i][j]) {
                    dfs(arr, y, x, n/2);
                    dfs(arr, y, x+n/2, n/2);
                    dfs(arr, y+n/2, x, n/2);
                    dfs(arr, y+n/2, x+n/2, n/2);
                    
                    return;
                }
            }
        }
        if (value == 0) {
            answer[0] += 1;
        } else {
            answer[1] += 1;
        }
        
    }
}
```
