구현 문제이라고 생각했다.   
```
import java.util.Arrays;
class Solution {
    public int solution(String name) {
        int answer = 0;
        String[] word = new String[name.length()];
        Arrays.fill(word,"A");
        int idx = 0;
        System.out.println(Arrays.toString(word));
        int temp = 0;
        while (true) {
            if (String.join("",word).equals(name)) {
                System.out.println("일치");
                System.out.println(answer);
                break;
            }
            System.out.println((int)name.charAt(idx));
            if ((int)name.charAt(idx) - 65 < 90 - (int)name.charAt(idx)) {
                System.out.println("정방향");
                answer += (int)name.charAt(idx) - 65;
                word[idx] = String.valueOf(name.charAt(idx));
                idx = findIdx(name, idx);
                System.out.println("다음 인덱스 "+idx);
            } else {
                System.out.println("역방향");
                answer += (90 - (int)name.charAt(idx));
                word[idx] = String.valueOf(name.charAt(idx));
                idx = findIdx(name, idx);
                System.out.println("다음 인덱스 "+idx);
            }
        }
        
       
        System.out.println(Arrays.toString(word));
        return answer;
    }
     public int findIdx(String name, int idx) {
         int next = 0;
         int n = name.length();
         int start = idx, end = idx;
         int limit = n;
         boolean Go = true;
         while (limit > 0) {
             start += 1;
             end -= 1;
             if (start >= n) start = 0;
             if (end < 0) end = n-1;
             
             if (name.charAt(start) != 'A') {
                 break;
             } else if (name.charAt(start) != 'A') {
                 Go = false;
                 break;
             }
             limit--;
         }
         return Go ? start : end;
    }
}
```
앞으로 가는것과 뒤로 가는것중에 어느게 더 가까운지만 구하면 되는 문제였다.   

```
import java.util.Arrays;
class Solution {
    public int solution(String name) {
        int answer = 0;
        int idx = 0;
        int move = name.length()-1;
        
        for (int i =0 ; i < name.length(); i++) {
            answer += Math.min(name.charAt(i) - 'A', 'Z' - name.charAt(i) + 1);
            idx = i + 1;
            while (idx < name.length() && name.charAt(idx) == 'A') {
                idx += 1;
            }
            //
            move = Math.min(move, i*2 + name.length()-idx);
            move = Math.min(move, (name.length()-idx)*2 + i);
        }
        
        return answer + move;
    }
}
```
