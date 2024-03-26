(0,0) -> (0,1)로 이동했다면   
0001 0100 두개를 다 넣은다음   
Set을 이용해 중복제거를 하는 방식을 생각했다.   
처음부터 set을 배열로 만드는 swift가 더 쉬웠다.   
한 좌표를 왼쪽에서 접근 + 오른쪽에서 접근이므로 /2해준다.   
```
import java.util.*;
class Solution {
    public int solution(String dirs) {
        String[] arr = dirs.split("");
        List<String> list = new ArrayList<>();
        int answer = 0;
        int y = 0, x = 0;
        for (String dir : arr) {
            int dy = y, dx = x;
            if (dir.equals("U")) {
                dy += 1;
            } else if (dir.equals("D")) {
                dy -= 1;
            } else if (dir.equals("R")) {
                dx += 1;
            } else {
                dx -= 1;
            }
            
            if (dy >= -5 && dy <= 5 && dx >= -5 && dx <= 5) { 
                String py = String.valueOf(y);
                String px = String.valueOf(x);
                String ny = String.valueOf(dy);
                String nx = String.valueOf(dx);
                String value1 = py+px+ny+nx;
                String value2 = ny+nx+py+px;
                list.add(value1);
                list.add(value2);
                y = dy;
                x = dx;
            } 
            //System.out.println(list.toString());
        }
        Set<String>set = new HashSet<>(list);
        //System.out.println(set.size()/2);
        return set.size()/2;
    }
}
```
