시간초과 발생   
```
import java.util.Arrays;
class Solution {
    public int solution(int n) {
        int answer = 0;
        String num = Integer.toBinaryString(n);
        String[] arr = num.split("");
        long cnt = Arrays.stream(arr)
                .filter(i -> i.equals("1"))
                .count();
        
        while (true) {
            n += 1;
            String num1 = Integer.toBinaryString(n);
            String[] arr1 = num1.split("");
            long cnt1 = Arrays.stream(arr1)
                .filter(i -> i.equals("1"))
                .count();
            //System.out.println(cnt1);
            
            if (cnt == cnt1) { break; }
        }
        return n;
    }
}
```
bitCount를 통해 2진법의 1의 개수를 구해줄 수 있었다.   
```
import java.util.Arrays;
class Solution {
    public int nextBigNumber(int n)
    {
      int a = Integer.bitCount(n);
      int compare = n+1;
      while(true) {
        if(Integer.bitCount(compare)==a)
          break;
        compare++;
      }
      return compare;
    }
    
    public int solution(int n) {
        return nextBigNumber(n);
    }
}
```
