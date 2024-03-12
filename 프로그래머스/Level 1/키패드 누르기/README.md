```
import java.util.Arrays;
class Solution {
    int[][] numpadPos = {
            {3,1}, //0
            {0,0}, //1
            {0,1}, //2
            {0,2}, //3
            {1,0}, //4
            {1,1}, //5
            {1,2}, //6
            {2,0}, //7
            {2,1}, //8
            {2,2}  //9
        };
    public String solution(int[] numbers, String hand) {
        String answer = "";
        
        //초기 위치
        int[] leftPos = {3,0};
        int[] rightPos = {3,2};
        
        for (int number : numbers) {
            //System.out.println("현재 "+number);
            
            // 1 4 7 일때
            if (number == 1 || number == 4 || number == 7) {
                answer += "L";
                leftPos = numpadPos[number];
            } else if (number == 3 || number == 6 || number == 9) {
            // 3 6 9 일때
                answer += "R";
                rightPos = numpadPos[number];
            } else {
            // 2 5 8 0 일때
                int leftRange = cal(leftPos, number);
                int rightRange = cal(rightPos, number);
                // System.out.println("가운데줄"+Arrays.toString(leftPos)+" "+Arrays.toString(rightPos));
                // System.out.println(""+leftRange+" "+rightRange);
                if (leftRange == rightRange) {
                    if (hand.equals("right")) {
                        answer += "R";
                        rightPos = numpadPos[number];
                    } else {
                        answer += "L";
                        leftPos = numpadPos[number];
                    }
                } else if (leftRange > rightRange) {
                    answer += "R";
                    rightPos = numpadPos[number];
                } else {
                    answer += "L";
                    leftPos = numpadPos[number];
                }
            }
        }
        
        return answer;
    }
    private int cal(int[] pos, int num) {
        return Math.abs(pos[0]-numpadPos[num][0]) + Math.abs(pos[1]-numpadPos[num][1]);
    }
}
```
