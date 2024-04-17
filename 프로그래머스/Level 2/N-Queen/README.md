백트래킹 문제이다.   
각 퀸이 같은 행,열,대각선에 존재하는지 확인하는 문제이다.   
2차원배열도 가능하지만 더 쉽게 생각하면   
1차원 배열로 진행하고 index를 x로 arr[index]를 y로 계산하여 풀이할 수도있다.   

```
class Solution {
    static int answer;
    static int[] arr;
    public int solution(int n) {
        answer = 0;
        // 1차원배열의 인덱스는 x를 가르키고, 엔덱스의 값은 y를 가르킨다.
        // arr[0] = 1 은 (1,0) 을 가르킨다.
        arr = new int[n];
        nqueen(0, n);
        return answer;
    }
    
    public void nqueen(int depth, int n) {
        if (depth == n) {
            answer += 1;
            return;
        }
        
        for (int i = 0; i < n; i++) {
            arr[depth] = i;
            if (isPossible(depth)) {
                nqueen(depth+1, n);
            }
        }
    }
    
    public boolean isPossible(int y) {
        for (int i = 0; i < y; i++) {
            // 같은 행에 존재할 경우
            if (arr[y] == arr[i]) {
                return false;
            } 
            // 대각선에 존재하는 경우
            // 열의 차와 행의 차가 같을 경우 대각선에 놓여있다
            else if (Math.abs(y - i) == Math.abs(arr[y] - arr[i])) {
                return false;
            }
        }
        return true;
    }
}
```
