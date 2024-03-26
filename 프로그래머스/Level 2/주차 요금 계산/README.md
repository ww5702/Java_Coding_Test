구현 문제이다.   
```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int[] solution(int[] fees, String[] records) {
        HashMap<String,Integer>result = new HashMap<>();
        HashMap<String,Integer>In = new HashMap<>();
        int basicTime = fees[0];
        int basicFee = fees[1];
        int perTime = fees[2];
        int perFee = fees[3];
        
        for (String r : records) {
            String[] record = r.split(" ");
            //System.out.println(Arrays.toString(record));
            String[] recordTime = record[0].split(":");
            int hour = Integer.valueOf(recordTime[0])*60;
            int min = Integer.valueOf(recordTime[1]);
            int time = hour + min;
            String carNum = record[1];
            String about = record[2];
            if (about.equals("IN")) {
                In.put(carNum, time);
            } else {
                int InTime = In.get(carNum);
                result.put(carNum, result.getOrDefault(carNum, 0) + time - InTime);
                In.remove(carNum);
                // System.out.println(In);
                // System.out.println(result);
            }
            
        }
        List<String> keySet = new ArrayList<>(In.keySet());
        int maxTime = 23*60 + 59;
        for (int i = 0; i < keySet.size(); i++) {
            int InTime = In.get(keySet.get(i));
            result.put(keySet.get(i), result.getOrDefault(keySet.get(i), 0) + maxTime - InTime);
        }
        //System.out.println(In);
        //System.out.println(result);
        
        int[] answer = new int[result.size()];
        keySet = new ArrayList<>(result.keySet());
        Collections.sort(keySet);
        for (int i = 0; i < keySet.size(); i++) {
            int cost = basicFee;
            int time = result.get(keySet.get(i));
            if (time > basicTime) {
                double per = Math.ceil((double)(time-basicTime) / (double)perTime);
                int total = (int)per * perFee;
                answer[i] = basicFee + total;
            } else {
                answer[i] = basicFee;
            }
        }
        
        return answer;
    }
}
```
