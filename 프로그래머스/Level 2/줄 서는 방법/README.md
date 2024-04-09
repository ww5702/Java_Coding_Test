리스트에 1,2,3,4가 들어가있다   
24개의 팩토리얼이 있고 9번째 순서를 구하는것이라면   
각 자리수는 6개씩 들어갈 수 있다.   
9는 6으로 나눴을때 몫이 1이다.   
따라서 1번째 인덱스의 값이 들어간다.   
2 가 삽입되고   
   
9에서 6으로 나머지를 구한다 -> 3   
리스트에는 1 3 4가 있고   
각 자리마다 2개씩 들어갈 수 있다.   
3을 2로 나눴을때 몫은 1이다.   
인덱스 1의 값인 3이 들어간다.   
2 3이 된다.   
   
리스트에는 1 4가 남고,   
3에서 2를 나눈 나머지를 구한다 -> 1   
각 자리마다 1개씩 들어갈 수 있다.   
1을 1로 나눴을때 몫은 1이다.   
인덱스 1의 값이 들어간다.   
2 3 1    
n이 0이 될때가지 반복한다.   

```
import java.util.*;
class Solution {
    static int num;
    public int[] solution(int n, long k) {
        int[] answer = new int[n];
        List<Integer> list = new ArrayList<>();
        long factorial = 1;
        int idx = 0;
        for (int i = 1; i <= n; i++) {
            factorial *= i;
            list.add(i);
        }
        k--;
        while (n > 0) {
            factorial /= n;
            int val = (int)(k/factorial);
            answer[idx++] = list.get(val);
            list.remove(val);
            
            k %= factorial;
            n--;
        }
        return answer;
    }
}
```
