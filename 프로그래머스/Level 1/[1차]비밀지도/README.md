int형으로 진법을 계싼할 경우 2,6 테스트케이스가 런타임에러가 난다;    
Long형으로 변환시킬 경우 통과하게된다.   
```
class Solution {
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] answer = new String[n];
        for (int i = 0; i < n; i++) {
            answer[i] = "";
            Long num1 = Long.valueOf(Integer.toString(arr1[i],2));
            String num11 = String.format("%0"+n+"d",num1);
            
            Long num2 = Long.valueOf(Integer.toString(arr2[i],2));
            String num22 = String.format("%0"+n+"d",num2);
            
            for (int j = 0; j < n; j++) {
                //System.out.println(num11.charAt(j) == '1');
                if (num11.charAt(j) == '1' || num22.charAt(j) == '1') {
                    answer[i] += "#";
                } else {
                    answer[i] += " ";
                }
            }
        }
        return answer;
    }
}
```
풀이를 보았을 때 result[i] = Integer.toBinaryString(arr1[i] | arr2[i]);   
를 사용하는것이 완벽한 의도 같았다.   
```
import java.util.Arrays;
class Solution {
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] answer = new String[n];
        String[] result = new String[n];
        for (int i = 0; i < n; i++) {
            result[i] = Integer.toBinaryString(arr1[i] | arr2[i]);
        }
        //System.out.println(Arrays.toString(result));
        for (int i = 0; i < n; i++) {
            result[i] = String.format("%"+n+"s",result[i]);
            result[i] = result[i].replaceAll("1", "#");
            result[i] = result[i].replaceAll("0", " ");
        }
        return result;
    }
}
```
