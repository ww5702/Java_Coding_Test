ascii코드로 대소문자를 구분하면서 생난리를 쳤다.   
숫자도 upper,lower이 가능했다.   
따라서 전체를 lower, 첫번째인지는 flag를 통해 구분하여 풀이한다.   
```
import java.util.Arrays;
class Solution {
    public String solution(String s) {
        String[] sp = s.toLowerCase().split("");
        boolean flag = true;
        String result = "";
        
        for (String ss : sp) {
            //System.out.println(ss);
            result += flag ? ss.toUpperCase() : ss;
            flag = ss.equals(" ") ? true : false;
        }
        
        return result;
    }
}
```
