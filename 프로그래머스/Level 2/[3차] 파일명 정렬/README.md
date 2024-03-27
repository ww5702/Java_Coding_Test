pattern을 이용하면 쉽게 풀이할 수 있었다.   
```
import java.util.*;
import java.util.regex.*;
class Solution {
    public String[] solution(String[] files) {
        
        Pattern p = Pattern.compile("([a-z\\s.-]+)([0-9]{1,5})");
        // Matcher m = p.matcher(files[0].toLowerCase());
        // m.find();
        // System.out.println(m.group(2));

        Arrays.sort(files, new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                Matcher m1 = p.matcher(s1.toLowerCase());
                Matcher m2 = p.matcher(s2.toLowerCase());
                m1.find();
                m2.find();

                if(!m1.group(1).equals(m2.group(1))) {
                    return m1.group(1).compareTo(m2.group(1));
                } else {
                    return Integer.parseInt(m1.group(2)) - Integer.parseInt(m2.group(2));
                }
            }
        });
        return files;
    }
    
}
```
