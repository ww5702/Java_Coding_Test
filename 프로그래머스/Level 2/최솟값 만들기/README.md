```
import java.util.Arrays;
import java.util.*;
class Solution
{
    public int solution(int []A, int []B)
    {
        int answer = 0;
        Arrays.sort(A);
        Arrays.sort(B);
        //System.out.println(Arrays.toString(A));
        for (int i = 0; i < A.length; i++) {
            answer += (A[i] * B[A.length-i-1]);
            //System.out.println(answer);
        }
        
        return answer;
    }
}
```
