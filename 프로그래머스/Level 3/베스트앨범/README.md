hashmap을 3개 사용했다.   
먼저 총 재생횟수를 저장할 totalPlay   
각 장르마다 index를 넣은 sortedGenre   
index마다 재생횟수를 정렬할 sum   
totalPlay를 value를 기준으로 정렬하여 반복문을 실행한다.   
장르마다 Index를 넣은 sortedGenre를 sum에 값을 넣어서 저장한다.   
저장한 sum을 조건에 맞춰 정렬한다.   
정렬한 sum을 최대 2개씩 넣어준다.   

```
import java.util.*;
import java.util.List;
class Solution {
    public int[] solution(String[] genres, int[] plays) {
        
        HashMap<String, Integer> totalPlay = new HashMap<>();
        HashMap<String, List<Integer>> sortedGenre = new HashMap<>();
        
        for (int i = 0; i < genres.length; i++) {
            String g = genres[i];
            int p = plays[i];
            totalPlay.put(g, totalPlay.getOrDefault(g, 0) + p);
            if (sortedGenre.get(g) == null) {
                System.out.println(i);
                sortedGenre.put(g, List.of(i));
            } else {
                List<Integer> l = new ArrayList<>();
                l.addAll(sortedGenre.get(g));
                l.addAll(List.of(i));
                sortedGenre.put(g, l);
            }
            System.out.println(sortedGenre);
        }
        System.out.println(totalPlay);
        List<Integer> answer = new ArrayList<>();
        //정렬
        List<String> keySet = new ArrayList<>(totalPlay.keySet());
        keySet.sort((o1, o2) -> totalPlay.get(o2).compareTo(totalPlay.get(o1)));
        for (String key : keySet) {
            System.out.print("Key : " + key);
            System.out.println(sortedGenre.get(key));
            HashMap<Integer, Integer> sum = new HashMap<>();
            for (int i = 0; i < sortedGenre.get(key).size(); i++) {
                int idx = sortedGenre.get(key).get(i);
                sum.put(idx, plays[idx]);
            }
            System.out.println(sum);
            
            // 다시 정렬
            List<Integer> kS = new ArrayList<>(sum.keySet());
            //kS.sort((o1, o2) -> sum.get(o2).compareTo(sum.get(o1)));
            kS.sort((o1, o2) -> {
                if (sum.get(o1) == sum.get(o2)) {
                    return o1 - o2;
                } else {
                    return sum.get(o2).compareTo(sum.get(o1));
                }
            });
            int temp = 0;
            if (kS.size() == 1) {
                answer.add(kS.get(0));
            } else {
                for (int index: kS) {
                    if (temp == 2) break;
                    answer.add(index);
                    temp += 1;
                }
            }
            
            System.out.println(answer.toString());
        }
        
        return answer.stream().mapToInt(i -> i).toArray();
    }
}
```
