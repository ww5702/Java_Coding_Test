먼저 set을 이용해 젬의 종류를 구해준다.   
반복문을 통해 먼저 각 종류가 다 들어갈떄까지 반복해준다.   
다 들어갔다면 해당 순간의 인덱스가 더 작다면 start,end의 값을 변경해준다.   
그와 별개로 left를 한칸씩 움직이며 해당 값들을 뺴본다.   
만약 보석을 하나씩 빼더라도 다 쇼핑이 가능할수도 아닐수도 있다.   
가능하면 또 다시 인덱스 풀을 비교해보고, 불가능하다면 또다시 다음 값을    
추가해주는 방식으로 진행된다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int[] solution(String[] gems) {
        int[] answer = new int[2];
        Set<String> set = new HashSet<String>(Arrays.asList(gems));
        int size = set.size();
        HashMap<String,Integer> map = new HashMap<>();
        
        int start = 0, end = gems.length;
        int left = 0, right = -1, cnt = 0;
        
        while (left < gems.length && right < gems.length) {
            cnt = map.size();
            // 다 들어갔다면
            if (cnt == size) {
                if (right-left < end-start) {
                    end = right;
                    start = left;
                }
                int value = map.get(gems[left]);
                if (value - 1 == 0) {
                    map.remove(gems[left]);
                } else {
                    map.put(gems[left], value-1);
                }
                left += 1;
            } else {
                right += 1;
                if (right < gems.length) {
                    map.put(gems[right], map.getOrDefault(gems[right], 0) + 1);
                }
            }
            //System.out.println(map);
        }
        answer[0] = start+1;
        answer[1] = end+1;
        
        return answer;
    }
}
```
좋아요를 가장 많이 받은 문제 또한 같은 방식으로 풀이하였다.   
