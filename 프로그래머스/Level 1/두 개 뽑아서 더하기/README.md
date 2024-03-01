```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int[] solution(int[] numbers) {
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < numbers.length-1; i++) {
            for (int j = i+1; j < numbers.length; j++) {
                System.out.println(""+i+j);
                if (!list.contains(numbers[i]+numbers[j])) {
                    list.add(numbers[i]+numbers[j]);
                }
            }
        }
        Collections.sort(list);
        Integer[] answer = list.toArray(new Integer[list.size()]);
        System.out.println(list.toString());
        return Arrays.stream(answer).mapToInt(i->i).toArray();
    }
}
```
반환형을 public int[] solution에서   
publis List<Integer> solution으로 바꿔도 된다는 사실을   
타인의 정답을 통해 알게 되었다.   
ㅎㅎㅎㅎㅎ...   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public static List<Integer> solution(int[] numbers) {
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < numbers.length-1; i++) {
            for (int j = i+1; j < numbers.length; j++) {
                System.out.println(""+i+j);
                if (!list.contains(numbers[i]+numbers[j])) {
                    list.add(numbers[i]+numbers[j]);
                }
            }
        }
        Collections.sort(list);
        //System.out.println(list.toString());
        return list;
    }
}
```
