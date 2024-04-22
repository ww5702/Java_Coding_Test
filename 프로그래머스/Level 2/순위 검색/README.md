각 info들을 - 와 기본일때로 두 가지 경우로 나누어   
map에 삽입한다.   
-도 포함해서 나온 점수들중 이분탐색을 이용해 효율성테스트를 통과하여   
값을 찾아낸다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int[] solution(String[] info, String[] query) {
        int[] answer = new int[query.length];
        int idx = 0;
        Map<String, List<Integer>> map = new HashMap<>();
        
        for (int i = 0; i < info.length; i++) {
            String[] value = info[i].split(" ");
            String[] languages = new String[] {value[0], "-"};
            String[] jobs = new String[] {value[1], "-"};
            String[] careers = new String[] {value[2], "-"};
            String[] soulFood = new String[] {value[3], "-"};
            int score = Integer.valueOf(value[4]);
            
            for (String l : languages) {
                for (String j : jobs) {
                    for (String c : careers) {
                        for (String s : soulFood) {
                            String key = l+""+j+""+c+""+s;
                            if (!map.containsKey(key)) {
                                List<Integer> list = new ArrayList<Integer>();
                                map.put(key, list);
                            }
                            map.get(key).add(score);
                        }
                    }
                }
            }
            //System.out.println(Arrays.toString(value));
        }
        
        // 정렬
        for (String key : map.keySet()) {
            Collections.sort(map.get(key));
        }
        
        //System.out.println(map);
        
        for (int i = 0; i < query.length; i++) {
            String[] value = query[i].replaceAll(" and ", "").split(" ");
            //System.out.println(Arrays.toString(value));
            List<Integer> list = map.get(value[0]);
            int score = Integer.valueOf(value[1]);
            int start = 0, end = list.size()-1;
            while (start <= end) {
                int mid = (start+end)/2;
                if (list.get(mid) < score) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            }
            answer[i] = map.containsKey(value[0]) ? list.size()-start : 0;
        }
        return answer;
    }
}
```
