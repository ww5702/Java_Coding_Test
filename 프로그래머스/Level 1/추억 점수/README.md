```
import java.util.Arrays;
class Solution {
    public int[] solution(String[] name, int[] yearning, String[][] photo) {
        int[] answer = new int[photo.length];
        for (int i = 0; i < photo.length; i++) {
            int sum = 0;
            for (String p : photo[i]) {
                int index = Arrays.asList(name).indexOf(p); 
                //System.out.println(Arrays.asList(name).indexOf(p));
                sum += index != -1 ? yearning[index] : 0;
            }
            answer[i] = sum;
            //System.out.println(sum);
        }
        return answer;
    }
}
```
