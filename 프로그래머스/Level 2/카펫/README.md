brown+yellow로 약수들을 뽑아낸다.   
가운데 1개의 노란 카펫이 들어가려면 최소 가로 3, 세로 3의 길이가 필요하므로   
하나라도 3이하인 경우에는 뺴준다.   
가로-2 * 세로-2 가 노란카펫의 수와 같다면 반환해준다.   
```
class Solution {
    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];
        System.out.println(Math.sqrt(brown+yellow));
        for (int i = 1; i <= Math.sqrt(brown+yellow); i++) {
            if ((brown+yellow) % i == 0) {
                int width = Math.max(i, (brown+yellow)/i);
                int height = Math.min(i, (brown+yellow)/i);
                
                if (width < 3 || height < 3) { continue; }
                
                // System.out.println(width);
                // System.out.println(height);
                
                if ((width-2)*(height-2) == yellow) {
                    answer[0] = width;
                    answer[1] = height;
                }
                
            }
        }
        // if ((double)(int)Math.sqrt(brown+yellow) == Math.sqrt(brown+yellow)) {
        //     arr.add((int)Math.sqrt(brown+yellow));
        // }
        
        return answer;
    }
}
```
