주어진 조건대로 정렬 후    
주어진 조건대로 나머지를 다 더해준 뒤   
주어진 조건대로 XOR 연산을 실행한다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(int[][] data, int col, int row_begin, int row_end) {
        int answer = 0;
        Arrays.sort(data, (o1,o2) -> {
            if (o1[col-1] == o2[col-1]) {
                return Integer.compare(o2[0], o1[0]);
            } else {
                return Integer.compare(o1[col-1], o2[col-1]);
            }
        });
        //System.out.println(Arrays.deepToString(data));
        int sum = Arrays.stream(data[row_begin-1]).map(i -> i%row_begin).sum();
        //System.out.println(sum);
        for (int i = row_begin+1; i <= row_end; i++) {
            int x = i;
            int value = Arrays.stream(data[x-1]).map(num -> num%x).sum();
            sum = sum ^ value;
        }
        return sum;
    }
}
```
