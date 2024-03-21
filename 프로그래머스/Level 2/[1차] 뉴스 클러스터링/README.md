```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(String str1, String str2) {
        str1 = str1.toLowerCase();
        str2 = str2.toLowerCase();
        String[] str1Arr = str1.split("");
        String[] str2Arr = str2.split("");
        
        //System.out.println(Arrays.toString(str2Arr));
        Map<String, Long> str1List = group(str1);
        Map<String, Long> str2List = group(str2);
        //System.out.println(str1List);
        //System.out.println(str2List);        
        
        int num1 = intersection(str1List, str2List);
        int num2 = union(str1List, str2List);
        if (num1 == 0 && num2 == 0) {
            num1 = 1;
            num2 = 1;
        }
        //System.out.println(num1);
        //System.out.println(num2);
        int answer = (int)Math.floor(((double)num1/(double)num2)*65536);
        return answer;
    }
    private Map<String, Long> group(String word) {
        Map<String, Long> list = new HashMap<>();
        for (int i = 0; i < word.length()-1; i++) {
            int s1 = word.charAt(i);
            int s2 = word.charAt(i+1);
            if (s1 >= 97 && s1 <= 122 && s2 >= 97 && s2 <= 122) {
                String value = String.valueOf((char)s1) + String.valueOf((char)s2);
                //System.out.println(value);
                list.put(value, list.getOrDefault(value, Long.valueOf(0)) + 1);
            }
        }
        return list;
    }
    private Integer intersection(Map<String, Long> list1, Map<String, Long> list2) {
        int sum = 0;
        List<String> keySet = new ArrayList<>(list1.keySet());
        for (int i = 0; i < keySet.size(); i++) {
            // System.out.println(keySet.get(i));
            // System.out.println(list2.get(keySet.get(i)));
            Long num1 = list1.get(keySet.get(i));
            Long num2 = list2.get(keySet.get(i));
            if (num1 != null && num2 != null) {
                sum += Math.min(num1,num2);
            }
            
        }
        return sum;
    }
    private Integer union(Map<String, Long> list1, Map<String, Long> list2) {
        list2.forEach((key, value) -> list1.merge(key, value, (v1,v2) -> Math.max(v1,v2)));
        //System.out.println(list1);
        List<Long> valueSet = new ArrayList<>(list1.values());
        return valueSet.stream().mapToInt(Long::intValue).sum();
    }
}
```
