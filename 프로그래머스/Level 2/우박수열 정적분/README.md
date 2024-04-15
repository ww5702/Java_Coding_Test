```
import java.util.*;
class Point {
    int y;
    int x;
    public Point (int y, int x) {
        this.y = y;
        this.x = x;
    }
}
class Solution {
    public double[] solution(int k, int[][] ranges) {
        double[] answer = new double[ranges.length];
        List<Point> list = new ArrayList<>();
        int listIdx = 0;
        list.add(new Point(listIdx++,k));
        while (k != 1) {
            if (k % 2 == 0) {
                list.add(new Point(listIdx++, k/2));
                k /= 2;
            } else {
                list.add(new Point(listIdx++, (k*3)+1));
                k *= 3;
                k += 1;
            }
        }
        List<Double> map = new ArrayList<>();
        for (int i = 0; i < list.size()-1; i++) {
            //System.out.println(i+" "+(i+1));
            map.add(((double)(list.get(i).x + list.get(i+1).x) / 2.0));
        }
        //System.out.println(map.toString());
        int answerIdx = 0;
        for(int[] range : ranges) {
            int start = range[0];
            int end = map.size() + range[1];
            //System.out.println(start+" "+end);
            if(start > end) {
                answer[answerIdx++] = -1.0;
            } else {
                double sum = 0.0;
                for(int i = start; i < end; i++) {
                    sum += map.get(i);
                }
                answer[answerIdx++] = sum;
            }
        }
        
        return answer;
    }
}
```
