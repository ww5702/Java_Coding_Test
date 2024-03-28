구현 문제이다.   
```
import java.util.Arrays;
import java.util.*;
class Point {
    public int y;
    public int x;
    
    public Point(int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    static String[][] map;
    static List<Point> list;
    public int solution(int m, int n, String[] board) {
        int answer = 0;
        map = new String[board.length][board[0].length()];
        for (int i = 0; i < board.length; i++) {
            String[] value = board[i].split("");
            for (int j = 0; j < value.length; j++) {
                map[i][j] = value[j];
            }
        }
        System.out.println(Arrays.deepToString(map));
        while (true) {
            int cnt = 0;
            list = new ArrayList<>();
            for (int i = 0; i < map.length-1; i++) {
                for (int j = 0; j < map[0].length-1; j++) {
                    String word = map[i][j];
                    if (map[i][j+1].equals(word) && map[i+1][j].equals(word) && map[i+1][j+1].equals(word)) {
                        cnt += 1;
                        list.add(new Point(i,j));
                        list.add(new Point(i+1,j));
                        list.add(new Point(i,j+1));
                        list.add(new Point(i+1,j+1));
                    }
                    
                }
            }
            removeMap(map, list);
            // for (int i = 0; i < map.length; i++) {
            //     System.out.println(Arrays.toString(map[i]));
            // }
            moveMap(map);
            // for (int i = 0; i < map.length; i++) {
            //     System.out.println(Arrays.toString(map[i]));
            // }
            answer += cnt;
            if (cnt == 0) { break; }
        }
        
        
        return answer;
    }
    public void removeMap(String[][] map, List<Point> list) {
        for (int i = 0; i < list.size(); i++) {
            int y = list.get(i).y;
            int x = list.get(i).x;
            map[y][x] = " ";
        }
    }
    public void moveMap(String[][] map) {
        for (int i = map.length-1; i > 0; i--) {
            for (int j = 0; j < map[0].length; j++) {
                if (map[i][j].equals(" ")) {
                    int idx = i;
                    while(idx >= 0) {
                        idx -= 1;
                        if (idx == -1) { break;}
                        if (!map[idx][j].equals(" ")) { 
                            break;
                        }
                    }
                    if (idx != -1) {
                        map[i][j] = map[idx][j];
                        map[idx][j] = " ";
                    }
                    
                }
            }
        }
    }
}
```
삭제된 횟수가 아니라 지워진 빈칸의 개수를 구하는 문제이다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public int solution(int m, int n, String[] board) {
        int answer = 0;
      char[][] boardArr = new char[m+2][n+2];
      int answerbefor = -1;
                   for(int  i =0; i<m; i++){
          for(int  j =0; j<n; j++){
          boardArr[i][j]= board[i].toCharArray()[j];
         }  
      }

      while(true){
          if(answer == answerbefor){
              break;
          }
          answerbefor = answer;

        boolean[][] boardCleaner = new boolean[m+2][n+2];
              for(int  i =0; i<m; i++){
          for(int  j =0; j<n; j++){
              if(boardArr[i][j]==boardArr[i][j+1]&&boardArr[i][j]!=' '){
                   if(boardArr[i][j]==boardArr[i+1][j+1]){
                    if(boardArr[i][j]==boardArr[i+1][j]){
                        boardCleaner[i][j] = true;
                        boardCleaner[i+1][j] = true;
                        boardCleaner[i+1][j+1] = true;
                        boardCleaner[i][j+1] = true;
                    }
                    }
              }
         }  
      }

      for(int  i =0; i<m; i++){
          for(int  j =0; j<n; j++){
              if(boardCleaner[i][j]){
                   boardArr[i][j] = ' ';
                  answer++;
                  boardCleaner[i][j] = false;
              }

         }  

      }
        for(int k = 0; k<m; k++){
        for(int  i =m; i>0; i--){
          for(int  j =0; j<n; j++){
              if(boardArr[i][j]==' '){
                  // System.out.print("!");
              boardArr[i][j] = boardArr[i-1][j];
              boardArr[i-1][j] = ' ';
              }
         }  
           //System.out.println();
      }
        }
      }

      return answer;
    }
}
```
