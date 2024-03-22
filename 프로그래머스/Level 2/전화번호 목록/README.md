startsWith로 만나자마자 break 하려고 헀으나   
테스트케이스는 전부 통과하고 효율성 테스트에서 2개가 실패   

```
class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        for (int i = 0; i < phone_book.length; i++) {
            for (int j = 0; j < phone_book.length; j++) {
                if (i == j) { continue; }
                if (phone_book[j].startsWith(phone_book[i])) {
                    answer = false;
                    break;
                }
            }
            if (!answer) { break; }
        }
        return answer;
    }
}
```
반복문을 하나 줄이니 통과하긴했다   
```
import java.util.Arrays;
class Solution {
    public boolean solution(String[] phone_book) {
        Arrays.sort(phone_book);
        for (int i = 0; i < phone_book.length-1; i++) {
            if (phone_book[i+1].startsWith(phone_book[i])) {
                return false;
            }
        }
        return true;
    }
}
```
문제에서 원하는 hash로 풀이해도 보았다.   
97674223이라면   
9일때 97일때 976일때로 substring을 나눈다음 해당 숫자가   
map.containsKey()로 해당 키가 존재하는지 확인한다.   

```
import java.util.Arrays;
import java.util.*;

class Solution {
    public boolean solution(String[] phone_book) {
        Map<String, Integer> map = new HashMap<>();
        
        for (int i = 0; i < phone_book.length; i++)  {
            map.put(phone_book[i], i);
        }
            
        
        for (int i = 0; i < phone_book.length; i++) {
            for (int j = 0; j < phone_book[i].length(); j++) {
                if (map.containsKey(phone_book[i].substring(0,j))) {
                    // System.out.println(phone_book[i]);
                    // System.out.println(phone_book[i].substring(0,j));
                    return false;
                }
            }
        }
        return true;
    }
}
```
