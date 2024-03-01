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
