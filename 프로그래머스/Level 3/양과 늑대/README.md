생각보다 쉬운 dfs문제이다.   
만약 양이 늑대보다 수가 많다면 진행하고   
늑대인 칸을 밟았는데 양보다 같거나 크면 해당 노드는 일단 남겨둔다.   
그리고 다시 다른 칸부터 방문을 해본다.   
   
   
하지만 한가지 swift와 다른 부분이 있었다.   
방문해야할 nextNode를 새로 newNextNode로 만들어 복사해줘야 한다는 것이다.   
따라서 addAll(newNode)를 이용해 추가해준다.   

```
import java.util.*;

class Solution {
    static ArrayList<Integer>[] list;
    static int answer;
    public int solution(int[] info, int[][] edges) {
        int n = info.length;
        list = new ArrayList[n+1];
        for (int i = 0; i <= n; i++) {
            list[i] = new ArrayList<>();
        }
        for(int[] edge : edges) {
            list[edge[0]].add(edge[1]);
        }
        
        List<Integer> arr = new ArrayList<>();
        arr.add(0);
        answer = -1;
        dfs(info, 0, arr, 0, 0);
        
        
        return answer;
    }
    
    public void dfs(int[] info, int node, List<Integer> nextNode, int sheep, int wolf) {
        int sheepCnt = sheep;
        int wolfCnt = wolf;
        if (info[node] == 0) sheepCnt += 1;
        else wolfCnt += 1;
        
        if (wolfCnt >= sheepCnt) return;
        
        answer = Math.max(answer, sheepCnt);
        
        List<Integer> newNextNode = new ArrayList<>();
        newNextNode.addAll(nextNode);
        // 방문 노드 삭제
        newNextNode.remove(Integer.valueOf(node));
        for (int next : list[node]) {
            System.out.println(next);
            newNextNode.add(next);
        }
        //System.out.println(newNextNode.toString());
        
        
        // 다시 방문 해보기
        for (int n : newNextNode) {
            dfs(info, n, newNextNode, sheepCnt, wolfCnt);
        }
        
    }
}
```
