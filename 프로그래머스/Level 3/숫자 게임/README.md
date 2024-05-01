배열의 크기가 크지 않아서 각 배열을 내림차순으로 정렬후    
큰 숫자이면 +1로 해주었다.   
```
import java.util.*;
class Solution {
    public int solution(int[] A, int[] B) {
        Integer[] newA = Arrays.stream(A).boxed().toArray(Integer[]::new);
        Integer[] newB = Arrays.stream(B).boxed().toArray(Integer[]::new);
        
        Arrays.sort(newA, Collections.reverseOrder());
        Arrays.sort(newB, Collections.reverseOrder());
        int result = 0;
        int bIndex = 0;
        for (int i = 0; i < newA.length; i++) {
            if (newB[bIndex] > newA[i]) {
                bIndex += 1;
                result += 1;
            }
        }
        return result;
    }
}
```
좋아요를 가장 많이 받은 문제풀이도 내 풀이와 같았다.   
