```
import java.util.Arrays;
class Solution {
    public int[] solution(String[] park, String[] routes) {
        int n = park.length;
        int m = park[0].length();
        String[][] board = new String[n][m];
        int y = 0;
        int x = 0;
        for (int i = 0; i < n; i++) {
            String[] input = park[i].split("");
            for (int j = 0; j < m; j++) {
                board[i][j] = input[j];
                if (input[j].equals("S")) {
                    y = i;
                    x = j;
                }
            }
        }
        //System.out.println(Arrays.deepToString(board));
        
        for (String route : routes) {
            int newY = y, newX = x;
            boolean isOk = true;
            //System.out.println("현재위치"+y+" "+x);
            String[] order = route.split(" ");
            int num = Integer.valueOf(order[1]);
            String direction = order[0];
            //System.out.println(Arrays.toString(order));
            
            if (direction.equals("E")) {
                for (int i = 0; i < num; i++) {
                    newX += 1;
                    if (newX >= m || board[newY][newX].equals("X")) {
                        isOk = false;
                        continue;
                    }
                }
            } else if (direction.equals("W")) {
                for (int i = 0; i < num; i++) {
                    newX -= 1;
                    if (newX < 0 || board[newY][newX].equals("X")) {
                        isOk = false;
                        continue;
                    }
                }
            } else if (direction.equals("S")) {
                for (int i = 0; i < num; i++) {
                    newY += 1;
                    if (newY >= n || board[newY][newX].equals("X")) {
                        isOk = false;
                        continue;
                    }
                }
            } else {
                for (int i = 0; i < num; i++) {
                    newY -= 1;
                    if (newY < 0 || board[newY][newX].equals("X")) {
                        isOk = false;
                        continue;
                    }
                }
            }
            
            if (isOk) {
                y = newY;
                x = newX;
            } 
            
        }
        //System.out.println("현재위치"+y+" "+x);
        int[] answer = {y,x};
        return answer;
    }
    
}
```
