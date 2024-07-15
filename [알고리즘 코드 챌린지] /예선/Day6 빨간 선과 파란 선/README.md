```
/*
1과 2를 고른다
1에서 2가 가지고있는 연결된 간선들을 다 연결해준다 없다면 1,2만
[1](2) 가 연결된다
[2](1) 도 연결된다. 

서로 간선이 없는 3과 2를 고른다
3에서 2와 연결되어있는 간선들을 다 연결해준다 1,2 
[1](2,3)
[2](1,3)
[3](1,2)
가 된다.

서로 간선이 없는 4,5를 고른다
4,5만 연결된다. (빨간줄)

5와 2를 고른다
2에서 가지고있는 간선들을 향해 연결해준다 (1,2,3)
[1](2,3,5)
[2](1,3,5)
[3](1,2,5)
[4](5)
[5](1,2,3,4)

즉 빨간색 선을 칠할때 가장 연결리스트가 적은 노드를 고르는것이 포인트
*/
```
일단 위와 같이 생각하여 dict와 연결리스트를 활용하여 풀이해보았다.   

```
import java.util.*;
import java.io.*;

class Main {
    static ArrayList<Integer>[] graph;
    static int n;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        int[] order = new int[n-1];
        for (int i = 0; i < n-1; i++) {
            order[i] = Integer.parseInt(st.nextToken());
        }
        graph = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }
        boolean[][] visited = new boolean[n+1][n+1];
        for (int i = 0; i <= n; i++) {
            visited[i][i] =  true;
        }
        HashMap<Integer, Integer> dict = new HashMap<Integer,Integer>();
        for (int i = 1; i <= 5; i++) {
            dict.put(i, 0);
        }
        int red = 0;
        int turn = 0;

        while (true) {
            // 각 간선이 연결한 노드가 n-1개라면 종료
            if (isFinish(graph)) break;

            // 연결해줄 노드 두개 구하기
            // 만약 파란간선 차례면 간선이 많은순서대로
            // 빨간간선 차례면 적은 순서대로
            int first = 0;
            List<Integer> keySet = new ArrayList<>(dict.keySet());
            if (order[turn] == 1) {
                keySet.sort((o1,o2) -> dict.get(o2).compareTo(dict.get(o1)));
            } else {
                keySet.sort((o1,o2) -> dict.get(o1).compareTo(dict.get(o2)));
            }
            //System.out.println(keySet);
            int tempIdx = 0;
            int second = 0;
            while (true) {
                first = keySet.get(tempIdx++);
                //System.out.println("연결할 노드 "+ first);

                second = 0;
                //System.out.println(graph[first].toString());
            
                for (int i = 1; i < n; i++) {
                    int key = keySet.get(i);
                    if (!graph[key].contains(first) && i != first) {
                        second = key;
                        break;
                    }
                }
                //System.out.println("first로 이어질 노드 "+second);

                if (second != 0) break;
            }

            
            // 파란간선이면 체크 x
            if (order[turn] == 1) {
                // first가 가진 노드 전부 연결
                for (int next : graph[first]) {
                    //System.out.println("first가 가진 연결노드 "+next);
                    if (!graph[next].contains(second)) {
                        graph[next].add(second);
                    }
                    if (!graph[second].contains(next)) {
                        graph[second].add(next);
                    }
                    
                    visited[next][second] = true;
                    visited[second][next] = true;
                    int valueNext = dict.get(next);
                    int valueSecond = dict.get(second);
                    dict.put(next, valueNext+1);
                    dict.put(second, valueSecond+1);
                }
                // 둘도 그리고 연결
                if (!graph[first].contains(second)) {
                    graph[first].add(second);
                }
                if (!graph[second].contains(first)) {
                    graph[second].add(first);
                }
                visited[first][second] = true;
                visited[second][first] = true;

                int valueFirst = dict.get(first);
                int valueSecond = dict.get(second);
                dict.put(first, valueFirst+1);
                dict.put(second, valueSecond+1);
            } else {
                // first가 가진 노드 전부 연결
                for (int next : graph[first]) {
                    //System.out.println("first가 가진 연결노드 "+next);
                    if (!graph[next].contains(second)) {
                        graph[next].add(second);
                    }
                    if (!graph[second].contains(next)) {
                        graph[second].add(next);
                    }
                    visited[next][second] = true;
                    visited[second][next] = true;
                    int valueNext = dict.get(next);
                    int valueSecond = dict.get(second);
                    dict.put(next, valueNext+1);
                    dict.put(second, valueSecond+1);
                    red += 1;
                }
                // 둘도 그리고 연결
                if (!graph[first].contains(second)) {
                    graph[first].add(second);
                }
                if (!graph[second].contains(first)) {
                    graph[second].add(first);
                }
                visited[first][second] = true;
                visited[second][first] = true;

                int valueFirst = dict.get(first);
                int valueSecond = dict.get(second);
                dict.put(first, valueFirst+1);
                dict.put(second, valueSecond+1);

                red += 1;
            }

            //System.out.println("연결 완료 빨간 선 개수"+red);
            turn += turn == n-2 ? 0 : 1;
            //System.out.println("다음 턴"+turn);
        }

        System.out.println(red);
    }

    public static boolean isFinish(ArrayList<Integer>[] graph) {
        for (int i = 1; i <= n; i++) {
            if (graph[i].size() != n-1) {
                return false;
            }
        }

        return true;
    }
}
```
