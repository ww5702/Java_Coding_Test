```
class Solution {
    public int[] solution(String s) {
        int[] answer = new int[s.length()];
        String arr[] = s.split("");
        for (int i = 0; i < arr.length; i++) {
            String now = arr[i];
            //System.out.println(now);
            boolean check = false;
            for (int j = i-1; j >= 0; j--) {
                String cur = arr[j];
                if (now.equals(cur)) {
                    check = true;
                    answer[i] = i-j;
                    break;
                }
                //System.out.println(j);
            }
            if (!check) {
                answer[i] = -1;
            }
        }
        return answer;
    }
}
```
더 깔끔하다.   
```
class Solution {
    public int[] solution(String s) {
        int[] result = new int[s.length()];

        for(int i=0;i<s.length();i++){

            String subStr = s.substring(0,i);
            if(subStr.indexOf(s.charAt(i))==-1) {
                result[i] = -1;
            }else {
                result[i] = i-subStr.lastIndexOf(s.charAt(i));
            }
        }
        return result;
    }
}
```
