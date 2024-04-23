겹치는 좌표값은 우선 평행이거나 무수히 많은 교점을 가지고있는지 확인해야한다.   
ad-b가 0이라면 해당사항에 포함된다.   
아니라면 x값과 y값은   
ax + by + m = 0   
cx + dy + n = 0 일때   
nb-md / ad-bc 와 mc-na / ad-bc로 두 좌표를 구할 수 있다.   
해당 좌표가 또한 정수일때만 list에 추가를 해줌과 동시에   
좌표평면상의 y,x의 최대 최소값을 갱신해준다.   
교점들을 구한 뒤 반복문을 돌면서 y - yMin, x - xMin값을 *로 변환시키고   
뒤에서부터 join을 이용해 string으로 출력해준다.   

22~29까지 메모리초과가 발생하는 이유는   
좌표값들이 long이 아니라서 그렇다.   
따라서 Integer.MAX_VALUE들을 long으로, 좌표들을 long으로 변환시켜줘야한다.   

```
import java.util.Arrays;
import java.util.*;
class Point {
    long y;
    long x;
    public Point(long y, long x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    public String[] solution(int[][] line) {
        long yMax = Long.MIN_VALUE, yMin = Long.MAX_VALUE, xMax = -Long.MIN_VALUE, xMin = Long.MAX_VALUE;
        List<Point> list = new ArrayList<>();
        for (int i = 0; i < line.length-1; i++) {
            for (int j = i+1; j < line.length; j++) {
                int[] abe = line[i];
                int[] cdf = line[j];
                // AD-BC
                long adbc = (long)abe[0] * (long)cdf[1] - (long)abe[1] * (long)cdf[0];
                // nB - mD
                long nbmd = (long)abe[1] * (long)cdf[2] - (long)abe[2] * (long)cdf[1];
                // mC - nA
                long mcna = (long)abe[2] * (long)cdf[0] - (long)abe[0] * (long)cdf[2];
                // 교차점이 하나고, 교점 x와 y 둘다 정수로 나눠떨어지면
                if (adbc != 0 && nbmd % adbc == 0 && mcna % adbc == 0) {
                    list.add(new Point(nbmd/adbc, mcna/adbc));
                    long ny = list.get(list.size()-1).y;
                    long nx = list.get(list.size()-1).x;
                    //System.out.println(ny+" "+nx);
                    yMax = Math.max(ny, yMax);
                    yMin = Math.min(ny, yMin);
                    xMax = Math.max(nx, xMax);
                    xMin = Math.min(nx, xMin);
                }
            }
        }
        String[] answer = new String[(int)(xMax-xMin+1)];
        String[][] map = new String[(int)(xMax-xMin+1)][(int)(yMax-yMin+1)];
        for (int i = 0; i < map.length; i++) {
            Arrays.fill(map[i], ".");
        }
        for (int i = 0; i < list.size(); i++) {
            long dy = list.get(i).y - yMin;
            long dx = list.get(i).x - xMin;
            //System.out.println(dy+" "+dx);
            map[(int)dx][(int)dy] = "*";
        }
        // System.out.println(yMax+" "+yMin+" "+xMax+" "+xMin);
        // System.out.println(Arrays.deepToString(map));
        int idx = 0;
        for (int i = map.length-1; i >= 0; i--) {
            answer[idx++] = String.join("",map[i]);
        }
        return answer;
    }
}
```
