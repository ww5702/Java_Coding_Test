y좌표로 즉 끝나는 길이까지의 순서로 정렬을 한다.   
x좌표를 확인해서 전에 쐈던 레이저가 닿는 y좌표보다 작을경우 같은 레이저로   
요격이 가능하다.   
하지만 쐈던 레이저가 닿지 못하는 x좌표라면 다시 레이저를 쏴야한다.   
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
