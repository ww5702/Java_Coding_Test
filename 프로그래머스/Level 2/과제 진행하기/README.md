주어진대로 진행하면서 풀이하였다.   
시작시간을 Integer로 변환하여 다시 저장한뒤   
시작시간을 기준으로 정렬해주었다.   
   
   
해당 정렬된 시간표를 기준으로 반복문을 진행한다.      
만약 다음으로 올 시작시간이 현재 진행중인 과제가 끝날때까지 시작되지않는다면   
그냥 추가를 해준다.   
하지만 과제가 끝나기 전에 다음 과제가 시작되려고하면   
stack에 현재 과제의 제목과 남은 시간을 저장한다.   
다시 다음 과제를 시작하고, 다음과제를 끝냈음에도 다음 과제가 시작될떄까지   
시간이 남아있다면   
while문을 시작한다.   
stack이 빌때까지 반복하거나, 다음과제가 시작될때까지 반복하는데,   
제일 최근에 저장된 남은 과제를 진행하고,   
저장된 과제를 끝냈다면 answer에 추가,   
또 과제를 진행하다가 다음 시간이 다가왔다면 조금이라도 진행된 시간을 다시 저장   
   
   
   
 그리고 남은 stack을 차례차례 저장해준다.       
```
import java.util.*;
import java.util.Arrays;
class Point {
    String title;
    int time;
    public Point(String title, int time) {
        this.title = title;
        this.time = time;
    }
}
class Solution {
    public String[] solution(String[][] plans) {
        String[] answer = new String[plans.length];
        int answerIdx = 0;
        String[][] newPlan = new String[plans.length][plans[0].length];
        for (int i = 0; i < plans.length; i++) {
            newPlan[i][0] = plans[i][0];
            newPlan[i][2] = plans[i][2];
            String[] value = plans[i][1].split(":");
            int time = Integer.valueOf(value[0])*60;
            int min = Integer.valueOf(value[1]);
            newPlan[i][1] = String.valueOf(time+min);
        }
        Arrays.sort(newPlan, (o1,o2) -> {
            return Integer.valueOf(o1[1]) - Integer.valueOf(o2[1]);
        });
        System.out.println(Arrays.deepToString(newPlan));
        
        Stack<Point> stack = new Stack<>();
        String name = newPlan[0][0];
        int time = Integer.valueOf(newPlan[0][1]);
        int duration = Integer.valueOf(newPlan[0][2]);
        for (int i = 1; i < newPlan.length; i++) {
            int startTime = Integer.valueOf(newPlan[i][1]);
            int startDuration = Integer.valueOf(newPlan[i][2]);
            System.out.println("다음 시작시간 "+startTime);
            if (time+duration > startTime) {
                System.out.println("시간이 모자라서 스택에 추가" + name+ (duration - (startTime - time)));
                stack.add(new Point(name, duration - (startTime - time)));
                name = newPlan[i][0];
                time = startTime;
                duration = startDuration;
            } else {
                answer[answerIdx++] = name;
                int restTime = startTime - (time+duration);
                while (!stack.isEmpty()) {
                    System.out.println("시간 남음 "+restTime);
                    String restTitle = stack.peek().title;
                    int restDuration = stack.peek().time;
                    System.out.println(restTitle+" "+restDuration);
                    if (restTime >= restDuration) {
                        answer[answerIdx++] = restTitle;
                        restTime -= restDuration;
                        stack.pop();
                    } else {
                        stack.pop();
                        stack.add(new Point(restTitle, restDuration - restTime));
                        restTime = 0;
                    }
                    
                    if (restTime == 0) { 
                        System.out.println("남은 시간 끝");
                        break; 
                    }
                }
                name = newPlan[i][0];
                time = startTime;
                duration = Integer.valueOf(newPlan[i][2]);
            }
                          
        }
        System.out.println(Arrays.toString(answer));
        System.out.println("반복문 끝 "+name+" "+time+" "+duration);
        answer[answerIdx++] = name;
        while (!stack.isEmpty()) {
            System.out.println(stack.peek().title+" "+stack.peek().time);
            answer[answerIdx++] = stack.peek().title;
            stack.pop();
        }
        
        return answer;
    }
}
```
