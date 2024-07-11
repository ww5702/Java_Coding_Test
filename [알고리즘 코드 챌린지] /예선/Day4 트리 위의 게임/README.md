진짜 문제 해석이 말이 안된다.   
여튼 1번 노드를 루트노드로 만들어 트리를 만들고   
최선의 선택을 했을떄 선공이 이기는지 지는지 확인하는것같은데   
dfs에서 한번 막혀서 20점으로 제출하였다.   

```
import java.util.*;
import java.io.*;

class Main {
    static int firstPlayer;
    static int secondPlayer;
    static boolean myTurn;
    static boolean[] visited;
    static boolean isWin;
    static ArrayList<Integer>[] list;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[][] edge = new int[n-1][2];
        for (int i = 0; i < n-1; i++) {
            String[] input = br.readLine().split(" ");
            edge[i][0] = Integer.parseInt(input[0]);
            edge[i][1] = Integer.parseInt(input[1]);
        }

        list = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            list[i] = new ArrayList<>();
        }
        for (int[] e: edge) {
            list[e[0]].add(e[1]);
            list[e[1]].add(e[0]);
        }
        List<List<Integer>> tree = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            tree.add(new ArrayList<>());
        }
        visited = new boolean[n+1];
        findChildren(1, tree);

        // 정렬
        for (int i = 0; i <= n; i++) {
            //, Collections.reverseOrder()
            Collections.sort(tree.get(i));
        }
        for (int i = 1; i <= n; i++) {
            System.out.println(tree.get(i).toString());
        }

        // for (int i = 0; i <= n; i++) {
        //     System.out.println(list[i].toString());
        // }
        

        for (int i = 1; i <= n; i++) {
            firstPlayer = 0;
            secondPlayer = 0;
            myTurn = true;
            visited = new boolean[n+1];
            isWin = false;
            dfs(tree, i);
            //System.out.println(firstPlayer+" "+secondPlayer);
            System.out.println(i+" "+isWin);
        }

    }

    public static void findChildren(int cur, List<List<Integer>> tree) {
        visited[cur] = true;
        for (int i = 0; i < list[cur].size(); i++) {
            int node = list[cur].get(i);
            if (!visited[node]) {
                tree.get(cur).add(node);
                findChildren(node, tree);
            }
        }
    }

    public static void dfs(List<List<Integer>> tree, int node) {
        visited[node] = true;
        
        if (myTurn) {
            firstPlayer += node;
            myTurn = false;
        } else {
            secondPlayer += node;
            myTurn = true;
        }

        for (int i = 0; i < tree.get(node).size(); i++) {
            if (!visited[tree.get(node).get(i)]) {
                dfs(tree, tree.get(node).get(i));
            }
        }

        if (firstPlayer >= secondPlayer) {
            System.out.println(firstPlayer+" "+secondPlayer);
            isWin = true;
        }

        return;



    }
}
/*
1 3
4

2 1
3 4

3 4

0 0

5 1
3 4
  1
2 3 5
  4

1 3
4

2 0

3 4

4 0
 
5 0


    1
  2   3
4    5  6

1 2
4

2 4

3 5

4 

*/
```
