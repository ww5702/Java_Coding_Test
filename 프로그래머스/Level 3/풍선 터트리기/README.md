처음에는 백트래킹으로 풀이하려고 했으나 메모리 초과   

```
import java.util.Arrays;
import java.util.*;
import java.util.stream.*;

class Solution {
    static boolean[] visited;
    static List<Integer> arr;
    public int solution(int[] a) {
        int answer = 0;
        arr = new ArrayList<>();
        for (int i = 0; i < a.length; i++) {
            arr.add(a[i]);
        }
        List<Integer> copyList = new ArrayList<>(arr);
        visited = new boolean[a.length];
        dfs(copyList, true);
        
        for (int i = 0; i < visited.length; i++) {
            if (visited[i]) answer += 1;
        }
        
        return answer;
    }
    
    public void dfs(List<Integer> list, boolean chance) {
        if (list.size() == 1) {
            int idx = arr.indexOf(list.get(0));
            visited[idx] = true;
            return;
        }
        
        for (int i = 0; i < list.size()-1; i++) {
            // 더 작은값 제거 가능?
            if (chance) {
                if (list.get(i) < list.get(i+1)) {
                    List<Integer> temp = new ArrayList<>(list);
                    temp.remove(i);
                    dfs(temp, false);
                } else {
                    List<Integer> temp = new ArrayList<>(list);
                    temp.remove(i+1);
                    dfs(temp, false);
                }
            }
            //원래는 더 큰값만 제거
            if (list.get(i) < list.get(i+1)) {
                List<Integer> temp = new ArrayList<>(list);
                temp.remove(i+1);
                dfs(temp, chance);
            } else {
                List<Integer> temp = new ArrayList<>(list);
                temp.remove(i);
                dfs(temp, chance);
            }
        }
        
    }
}
```
구현 문제였다.   
쉽게 생각해서 왼쪽 오른쪽 인접한 숫자들보다 크기만 하다면 가능한 숫자이다.   
따라서 왼쪽에서부터 가장 작은수를 정렬하고,   
가장 오른쪽에서부터 가장 작은수를 정렬한다음   
해당 Index가 오른쪽 왼쪽의 배열보다 크기만 하다면 계속 큰수만 없애주다   
작은수를 한번 없앨 수 있다.   

```
import java.util.Arrays;
import java.util.*;
import java.util.stream.*;

class Solution {
    public int solution(int[] a) {
        int[] leftMin = new int[a.length];
        int[] rightMin = new int[a.length];
        int l = a[0];
        int r = a[a.length-1];
        
        for (int i = 1; i < a.length-1; i++) {
            if (l > a[i]) l = a[i];
            leftMin[i] = l;
        }
        for(int i = a.length - 2; i > 0; i--) {
            if(r > a[i]) r = a[i];
            rightMin[i] = r;
        }
        //System.out.println(Arrays.toString(leftMin));
        //System.out.println(Arrays.toString(rightMin));
        if (a.length == 1) return 1;
        
        int answer = 2;
        for (int i = 1; i <= a.length-2; i++) {
            if (a[i] > leftMin[i] && a[i] > rightMin[i]) continue;
            answer += 1;
        }
        
        return answer;
    }
}
```
좋아요를 가장 많이 받은 풀이는 다음과 같다.   
같은 풀이이지만 좀 더 수학적으로 풀이하였다.   

```
import java.util.*;
class Solution {
    public int solution(int[] a) {
        int answer = 0;
        int min1 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;
        HashSet<Integer> hs = new HashSet<>();
        for(int i=0;i<a.length;i++){
            min1=Math.min(min1,a[i]);
            min2=Math.min(min2,a[a.length-1-i]);
            hs.add(min1);
            hs.add(min2);
        }
        return hs.size();
    }
}
```
