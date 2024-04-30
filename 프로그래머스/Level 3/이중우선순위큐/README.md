pq를 하나로 만들어서 풀이하려고 하니까 어려운거였다.    
그냥 pq를 두개를 만들어 풀이하면 쉽게 풀이가 가능하다;   

```
import java.util.*;
class Solution {
    public int[] solution(String[] operations) {
        int[] answer = new int[2];
        PriorityQueue<Integer> pqL = new PriorityQueue<>();
        PriorityQueue<Integer> pqH = new PriorityQueue<>(Collections.reverseOrder());
        for (String operation : operations) {
            String[] arr = operation.split(" ");
            if (arr[0].equals("I")) {
                int num = Integer.valueOf(arr[1]);
                pqL.add(num);
                pqH.add(num);
            } else {
                if (pqL.size() > 0) {
                    if (arr[1].equals("1")) {
                // 최대값 찾아서 pqH에서도 지워주고 pq에서도 지워주고
                        int max = pqH.poll();
                        pqL.remove(max);
                    }
                    else {
                // 최소값 찾아서 반대로 실행
                        int min = pqL.poll();
                        pqH.remove(min);
                    }
                }
                //System.out.println(pqL);
                //System.out.println(pqH);
            }
        }
        if (pqL.size() > 0) {
            answer[0] = pqH.poll();
            answer[1] = pqL.poll();
        }
        return answer;
    }
}
```
