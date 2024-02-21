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
