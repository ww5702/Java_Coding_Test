0으로 전부 덮일때까지 반복   
6~9면 올리고,   
1~4면 내린다.   
5라면 앞글자에 따라서 비교한다.   
만약 맨앞글자라면 그냥 더하고,   
아니라면 해당숫자에 따라서 더하거나 뺀다.   
올릴때 주의 할 점은 앞 인덱스의 값이 1 증가한다.   

```
import java.util.*;
class Solution {
    public int solution(int storey) {
        String str = String.valueOf(storey);
        List<Integer> tree = new ArrayList<>();
        for (int i = 0; i < str.length(); i++) {
            tree.add(Integer.valueOf(str.charAt(i)-48));
        }
        int answer = 0;
        while (true) {
            //System.out.println(tree.toString());
            if (tree.stream().filter(x -> x == 0).count() == tree.size()) {
                break;
            }
            int idx = 0;
            for (int i = tree.size()-1; i >= 0; i--) {
                if (tree.get(i) != 0) {
                    idx = i;
                    break;
                }
            }
            //System.out.println(idx);
            if (tree.get(idx) > 5) {
                if (idx == 0) {
                    answer += (10-tree.get(idx));
                    tree.set(idx,0);
                    tree.add(0,1);
                } else {
                    answer += (10-tree.get(idx));
                    tree.set(idx,0);
                    tree.set(idx-1, tree.get(idx-1)+1);
                }
            } else if (tree.get(idx) < 5) {
                answer += tree.get(idx);
                tree.set(idx,0);
            } else {
                // 맨앞자리가 아니라면
                if (idx-1 > 0) {
                    if (tree.get(idx-1) >= 5) {
                        answer += (10-tree.get(idx));
                        tree.set(idx,0);
                        tree.set(idx-1, tree.get(idx-1)+1);
                    } else {
                        answer += tree.get(idx);
                        tree.set(idx,0);
                    }
                } else {
                // 맨앞자리라면
                    answer += 5;
                    tree.set(idx,0);
                }
            }
            //System.out.println(answer);
        }
        return answer;
    }
}
```
그리고 위의 내용을 반복문으로 이렇게 정리할수도 있다...   

```
import java.util.*;
class Solution {
    public int solution(int storey) {
        int answer = 0;
        while (storey != 0) {
            int upperNumber = (storey %100)/10;
            int number = storey % 10;
            if (number > 5 || number == 5 && upperNumber>=5) {
                storey += 10;
                answer += (10 - number);
            } else {
                answer += number;
            }
            storey = storey / 10;
        }  
        return answer;
    }
}
```
