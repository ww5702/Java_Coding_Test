```
class Solution {
    boolean solution(String s) {
        boolean answer = true;
        s.toUpperCase();
        int p = 0;
        int y = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.toUpperCase().substring(i,i+1).equals("P")) {
                p += 1;
            } else if (s.toUpperCase().substring(i,i+1).equals("Y")) {
                y += 1;
            }
            //System.out.println(s.toUpperCase().substring(i,i+1));
        }
        
        
        return p == y ? answer : !answer;
    }
}
```
두 방법 모두 가능   
```

import java.util.Arrays;
import java.util.stream.*;
class Solution {
    boolean solution(String s) {
        s.toUpperCase();
        long p = s.chars().filter( e -> 'P'== e).count();
        long y = s.chars().filter( e -> 'Y'== e).count();
        
        return p == y ? true : false;
    }
}
```
