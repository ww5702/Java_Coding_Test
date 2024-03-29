가장 큰 수를 기준으로 내림차순하는건 이해가 된다.   
그렇다면 두 자리수이거나 세자리수이거나 일떄는 어떻게 비교해야할까   
35보다는 39가 크다.   
따라서 3539와 3935를 비교해주는것이다.   
o2+o1이 더 크다면 o1+o2와 자리를 바꾸는 정렬을 사용한다.   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    public String solution(int[] numbers) {
        String answer = "";
        String[] nums = new String[numbers.length];

        for (int i=0; i<nums.length; i++) 
            nums[i] = String.valueOf(numbers[i]);
        
        Arrays.sort(nums, (o1, o2) -> (o2+o1).compareTo(o1 + o2));
        //System.out.println(Arrays.toString(nums));
        for (int i = 0; i < nums.length; i++) {
            answer += nums[i];
        }
        
        return nums[0].equals("0") ? "0" : answer;
    }
}
```
