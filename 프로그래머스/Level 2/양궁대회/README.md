dfs로 풀이한 첫번재 제출이다.   

```
import java.util.Arrays;
class Solution {
    static int[] arr;
    static int[] answer;
    static int maxScore;
    public int[] solution(int n, int[] info) {
        answer = new int[info.length];
        int[] a = {1, 1, 2, 0, 1, 2, 2, 0, 0, 0, 0};
        maxScore = 0;
        int apeachScore = 0;
        for (int i = 0; i < info.length; i++) {
            if (info[i] != 0) apeachScore += (10-i);
        }
        System.out.println(apeachScore);
        
        arr = new int[info.length];
        dfs(n, info, 0, arr, apeachScore);
        
        return answer;
    }
    
    public void dfs(int n, int[] info, int index, int[] arr, int apeachScore) {
        
        if (index == 10) {
            int temp = 0;
            if (n >= 1) {
                arr[10] += n;
            }
            for (int i = 0; i < 10; i++) {
                if (arr[i] != 0) temp += (10-i);
            }
            // if (Arrays.equals(a,arr)) {
            //     System.out.println("ass");
            //     System.out.println(Arrays.toString(arr)+" "+temp+" "+apeachScore);
            // }
            // 더 점수 많이 가졌을 경우만
            if (temp > apeachScore) {
                // 기존에 저장했던 더 큰 점수차로 이겼을 경우
                if ((temp - apeachScore) > maxScore) {
                    System.out.println(Arrays.toString(arr)+" "+temp);
                    System.arraycopy(arr, 0, answer, 0, 10);
                    maxScore = Math.max(maxScore, (temp - apeachScore));
                } 
                // 같은 점수차라면 더 낮은 점수를 쏜 사람거로
                else if ((temp - apeachScore) == maxScore) {
                    System.out.println("같음 "+Arrays.toString(arr)+" "+temp);
                    whoisbetter(answer, arr);
                }
                
            }
            
            return;
        }
        
        for (int i = index; i < 10; i++) {
            // 해당 점수판을 더 많이 쏠 수 있는 경우
            if (n >= (info[i]+1)) {
                arr[i] = info[i]+1;
                // 어피치가 안쏜 과녁을 겨냥할 경우 어필치가 점수가 깎이지는 않는다.
                if (info[i] == 0) {
                    dfs(n-(info[i]+1) , info, i+1, arr, apeachScore);
                }
                // 어피치의 점수를 깎으면서 자신의 점수 +
                else {
                    dfs(n-(info[i]+1) , info, i+1, arr, apeachScore - (10-i));
                }
                
            } 
            // 더 크더라도 지나갈 경우
            arr[i] = 0;
            dfs(n, info, i+1, arr, apeachScore);
        }
        
    }
    
    public void whoisbetter(int[] arr, int[] newArr) {
        
    }
}
```
