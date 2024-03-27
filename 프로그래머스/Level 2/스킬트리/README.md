스택을 이용해 풀이하였다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        Queue<String> q = new LinkedList<>();
        String[] arr = skill.split("");
        System.out.println(q);
        for (String s : skill_trees) {
            Boolean isPossible = true;
            for (String a : arr) {
                q.add(a);
            }   
            
            String[] now = s.split("");
            //System.out.println(Arrays.toString(now));
            String learn = q.poll();
            for (int i = 0; i < now.length; i++) {
                System.out.println(""+now[i]+" "+learn);
                if (now[i].equals(learn)) {
                    learn = q.poll();
                } else if (!now[i].equals(learn) && q.contains(now[i])) {
                    isPossible = false;
                    break;
                }
                
            }
            answer += isPossible ? 1 : 0;
            q.clear();
        }
        
        return answer;
    }
}
```
arraylist로 만들어 iterator를 이용해 한칸씩 전진한다.   
skill의 0번째 선행스킬이 아니라면 넘긴다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        ArrayList<String> skillTrees = new ArrayList<String>(Arrays.asList(skill_trees));
        System.out.println(skillTrees.toString());
        Iterator<String> it = skillTrees.iterator();
        while (it.hasNext()) {
            if (skill.indexOf(it.next().replaceAll("[^" + skill + "]", "")) != 0) {
                it.remove();
            }
            System.out.println(skillTrees.toString());
        }
        answer = skillTrees.size();
        return answer;
    }
}
```
