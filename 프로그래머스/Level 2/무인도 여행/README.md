```
import java.util.*;
import java.util.Arrays;
class Point {
    int y;
    int x;
    
    public Point(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    static String[][] map;
    static List<Integer> list;
    public int[] solution(String[] maps) {
        list = new ArrayList<>();
        map = new String[maps.length][maps[0].length()];
        for (int i = 0; i < maps.length; i++) {
            String[] input = maps[i].split("");
            for (int j = 0; j < input.length; j++) {
                map[i][j] = input[j];
            }
        }
        //System.out.println(Arrays.deepToString(map));
        for (int i = 0; i < maps.length; i++) {
            for (int j = 0; j < maps[0].length(); j++) {
                if (!map[i][j].equals("X")) {
                    int cnt = bfs(i,j);
                    //System.out.println(cnt);
                    list.add(cnt);
                }
            }
        }
        if (list.size() == 0) {
            list.add(-1);
        }
        Collections.sort(list);
        //System.out.println(list.toString());
        int[] answer = list.stream().mapToInt(i -> i).toArray();
        return answer;
    }
    public int bfs(int y, int x) {
        int[] dy = {1,-1,0,0};
        int[] dx = {0,0,1,-1};
        int result = 0;
        Queue<Point> q = new LinkedList<>();
        q.add(new Point(y,x));
        result += Integer.valueOf(map[y][x]);
        map[y][x] = "X";
        
        while (!q.isEmpty()) {
            int nowY = q.peek().y;
            int nowX = q.peek().x;
            q.poll();
            for (int i = 0; i < 4; i++) {
                int newY = nowY + dy[i];
                int newX = nowX + dx[i];
                if(newY >= 0 && newY < map.length && newX >= 0 && newX < map[0].length) {
                    if (!map[newY][newX].equals("X")) {
                        result += Integer.valueOf(map[newY][newX]);
                        map[newY][newX] = "X";
                        q.add(new Point(newY,newX));
                    }
                }
            }
        }
        return result;
    }
    
}
```
