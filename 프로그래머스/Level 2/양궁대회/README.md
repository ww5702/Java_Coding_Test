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
백트래킹으로 풀이하는건 똑같았다.   
```
import java.util.Arrays;
class Solution {
    static private int[] res = new int[11];//점수차가 최대일때 라이언이 쏜 화살배열
	static private int[] lion= {-1};//정답배열
	static private int max = Integer.MIN_VALUE;//최대값
    public int[] solution(int n, int[] info) {
        back(0,n,info);//라이언이 쏜 화살에 대한 조합
        
        if(max==-1) {//라이언이 어피치를 못 이길떄
        	lion = new int[1];
        	lion[0]=-1;
        }
        return lion;
    }
    
    public static void back(int depth, int n, int[] info) {
    	//화살 다 꽂았을때(종료조건)
    	if(depth==n) {
    		int diff = score(info);//점수차 구하기
    		if(max<=diff) {//점수차 최대값 갱신
    			max = diff;
    			lion = res.clone();
    		}
    		return;
    	}
    	for(int i=0; i<info.length && res[i]<=info[i]; i++) {
    		res[i] += 1;
    		back(depth+1, n, info);
    		res[i] -= 1;
    	}
    }
    
    public static int score(int[] info) {
    	int apeach=0, lion=0;
    	for(int i=0; i<res.length; i++) {
    		if(info[i]==0 && res[i]==0) continue;//i원소에 둘다 0개 맞췄을땐 무시.
    		if(info[i]>=res[i]) apeach += (10-i);
    		else lion += (10-i);
    	}
    	
    	int diff = lion - apeach;
    	if(diff<=0) return -1;
    	return diff;
    }
    
}
```
