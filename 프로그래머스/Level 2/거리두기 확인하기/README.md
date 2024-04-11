dfs로 풀이하면서 2를 넘긴다면 통과하기에 return   
2를 안넘는데 P를 만났다면 해당 index=0   
파티션이 아닌경우에만 dfs를 반복   

```
class Solution {
    static int[] dx = {-1, 0, 1, 0};
    static int[] dy = {0, 1, 0, -1};
    static boolean[][] visit;

    static int[] answer;

    public void dfs(int num, int x, int y, int count, String[] places){
        if (count > 2) return;
        if (count > 0 && count <= 2 && places[x].charAt(y) == 'P'){
            //2칸 범위내에 다른 응시자가 있을 경우 거리두기 미준수로 0처리
            answer[num] = 0;
            return;
        }
        for (int i = 0; i < 4; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];
            //배열 범위 밖으로 초과하는지 여부 검사, 파티션으로 분리되어 있는 경우 상관 없음.
            if (nx >= 0 && nx < 5 && ny >= 0 && ny < 5 && places[nx].charAt(ny) != 'X') {
                if (visit[nx][ny]) continue; //이미 방문한 곳일 경우 생략
                visit[nx][ny] = true;
                dfs(num, nx, ny, count + 1, places);
                visit[nx][ny] = false;
            }
        }
    }

    public int[] solution(String[][] places) {
        answer = new int[places.length];
        for (int i = 0; i < places.length; i++) {
            answer[i] = 1;
        }

        for (int i = 0; i < places.length; i++) {
            visit = new boolean[5][5];
            for (int j = 0; j < 5; j++) {
                for (int k = 0; k < 5; k++) {
                    if (places[i][j].charAt(k) == 'P'){
                        visit[j][k] = true;
                        dfs(i, j, k, 0, places[i]);
                        visit[j][k] = false;
                    }
                }
            }
        }
        return answer;
    }
}
```
