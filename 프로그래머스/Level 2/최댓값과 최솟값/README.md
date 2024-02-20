sort가 min,max 함수보다 아주 조금 빠른것을 확인할 수 있었다.   
sort시 최대 83MB   
```
import java.util.Arrays;
class Solution {
    public String solution(String s) {
        String[] arr = s.split(" ");
        int[] nums = Arrays.stream(arr).mapToInt(Integer::parseInt).toArray();
        Arrays.sort(nums);
        return nums[0]+" "+nums[nums.length-1];
    }
}
```
min,max 함수시 최대 89.3MB   
```
import java.util.Arrays;
class Solution {
    public String solution(String s) {
        String[] arr = s.split(" ");
        int[] nums = Arrays.stream(arr).mapToInt(Integer::parseInt).toArray();
        int min = Arrays.stream(nums).min().getAsInt();
        int max = Arrays.stream(nums).max().getAsInt();
        return min+" "+max;
    }
}
```
