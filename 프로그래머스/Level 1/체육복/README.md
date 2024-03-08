여벌의 체육복을 가져온 사람 있는데 본인이 체육복을 잃어버렸으면   
본인이 먼저 챙겨야 한다. -> 이 문구 때문에 한번 실패   
당연히 배열들이 정렬되어있는 줄 알았으나 안되있어 정렬후 문제 풀이 -> 이 부분 때문에 한번 더 실패   

```
import java.util.*;
import java.util.Arrays;
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int student = n - lost.length;
        Arrays.sort(lost);
        Arrays.sort(reserve);
        List<Integer> lostList = new ArrayList<>();
        List<Integer> reserveList = new ArrayList<>();
        for (int l : lost) {
            lostList.add(l);
        }
        for (int r : reserve) {
            reserveList.add(r);
        }
        //System.out.println(lostList.toString());
        List<Integer> removeidx = new ArrayList<>();
        for (int res : reserveList) {
            if (lostList.contains(res)) {
                lostList.remove(lostList.indexOf(res));
                student += 1;
                removeidx.add(res);
            }
        }
        for (int idx: removeidx) {
            reserveList.remove(Integer.valueOf(idx));
        }
        int temp = lostList.size();
        
        for (int res : reserveList) {
            int frontidx = lostList.indexOf(res-1);
            int backidx = lostList.indexOf(res+1);
            if (frontidx != -1) {
                lostList.remove(frontidx);
            } else if (backidx != -1) {
                lostList.remove(backidx);
            }
            //System.out.println("남은 리스트 "+lostList.toString());
            if (lostList.isEmpty()) { break; }
        }
        student += (temp - lostList.size());
        return student;
    }
}
```
