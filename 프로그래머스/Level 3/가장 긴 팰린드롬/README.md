```
import java.util.Arrays;
class Solution
{
    /*
    홀수면 가운데 빼고 같아야하고
    짝수면 반으로 나눠서 같아야한다.
    */
    public int solution(String s)
    {
        int answer = 0;
        String[] arr = s.split("");
        //System.out.println(Arrays.toString(arr));
        
        for (int i = 0; i < arr.length; i++) {
            for (int j = arr.length-i; j > answer; j--) {
                int start = i, end = i+j-1;
                //System.out.println(start+" "+end);
                while (start <= end && arr[start].equals(arr[end])) {
                    start += 1;
                    end -= 1;
                }
                
                if (start >= end) {
                    answer = Math.max(answer, j);
                }
                
            }
        }

        return answer;
    }
}
```
좋아요를 가장 많이 받은 풀이또한 위오 ㅏ비슷하게 풀이하였다.   
