규칙성이 존재한다.   
하지만 예외가 존재하는데 만약 3이라고 가정할때   
remain은 0이 된다.   
그리고 num은 1이 된다.   
하지만 반복문은 끝나야 하기에 num--를 해준다.   
```
import java.util.Arrays;
class Solution {
    public String solution(int n) {
        String[] numbers = {"4","1","2"};
        StringBuilder sb = new StringBuilder();
        /*
        한자리 3개 
        두자리 9개 
        세자리 27개 
        3 + 9 + 27 + ...
        */
        int num = n;
        while (num > 0) {
            int remain = num%3;
            num /= 3;
            if (remain == 0) num--;
            sb.append(numbers[remain]);
        }
        return sb.reverse().toString();
    }
}

```
