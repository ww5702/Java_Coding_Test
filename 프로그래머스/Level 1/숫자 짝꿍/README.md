```
import java.util.Arrays;
import java.util.*;
class Solution {
    public String solution(String X, String Y) {
        String answer = "";
        String[] Xarr = X.split("");
        String[] Yarr = Y.split("");
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i <= 9; i++) {
            long num = i;
            long xnum = Arrays.stream(Xarr)
                .filter(n -> Long.parseLong(n) == num)
                .count();
            long ynum = Arrays.stream(Yarr)
                .filter(n -> Long.parseLong(n) == num)
                .count();
            
            for (int j = 0; j < Math.min(xnum,ynum); j++) {
                list.add(i);
            }
        }
        Collections.sort(list, Collections.reverseOrder());
        if (list.size() < 1) { return "-1"; }
        
        String num = "";
        for (long i: list) {
            num += i;
        }
        if (num.charAt(0) == '0') {
            return "0";
        } else {
            return num;
        }
    }
}
```
시간초과가 발생하여 수정하였다   

```
import java.util.Arrays;
import java.util.*;
class Solution {
    public String solution(String X, String Y) {
        String answer = "";
        int[] Xnum = new int[10];
        for(int i=0; i<X.length(); i++){
            int idx = (int)X.charAt(i) - '0';
            Xnum[idx]++;
        }

        //Y에서 0~9까지의 개수
        int[] Ynum = new int[10];
        for(int i=0; i<Y.length(); i++){
            int idx = (int)Y.charAt(i) - '0';
            Ynum[idx]++;
        }

        //X와 Y 비교
        int[] XYnum = new int[10];
        for(int i=0; i<10; i++){
            if(Xnum[i] > 0 && Ynum[i] > 0) {
                if(Xnum[i] <= Ynum[i]) XYnum[i] = Xnum[i];
                else if(Xnum[i] > Ynum[i]) XYnum[i] = Ynum[i];
            }
        }
        System.out.println(Arrays.toString(XYnum));
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i <= 9; i++) {
            long num = XYnum[i];
            for (int j = 0; j < num; j++) {
                list.add(i);
            }
        }
        
        Collections.sort(list, Collections.reverseOrder());
        if (list.size() < 1) { return "-1"; }
        
        String num = "";
        for (long i: list) {
            num += i;
        }
        if (num.charAt(0) == '0') {
            return "0";
        } else {
            return num;
        }
    }
}
```
또 시간초과가 발생하여 수정해주었다.   
```
import java.util.Arrays;
import java.util.*;
class Solution {
    public String solution(String X, String Y) {
        int[] Xnum = new int[10];
        for(int i=0; i<X.length(); i++){
            int idx = (int)X.charAt(i) - '0';
            Xnum[idx]++;
        }

        //Y에서 0~9까지의 개수
        int[] Ynum = new int[10];
        for(int i=0; i<Y.length(); i++){
            int idx = (int)Y.charAt(i) - '0';
            Ynum[idx]++;
        }

        //X와 Y 비교
        int[] XYnum = new int[10];
        for(int i=0; i<10; i++){
            if(Xnum[i] > 0 && Ynum[i] > 0) {
                if(Xnum[i] <= Ynum[i]) XYnum[i] = Xnum[i];
                else if(Xnum[i] > Ynum[i]) XYnum[i] = Ynum[i];
            }
        }
        System.out.println(Arrays.toString(XYnum));
        
        String str = "";
        int cnt = 0;
        for(int i=0; i<10; i++){
            cnt += XYnum[i];
            if(XYnum[i] > 0){
                for(int j=0; j<XYnum[i]; j++){
                    str += i;
                }
            }
        }

        //split을 통해서 배열로 만들고 내림차순 정렬
        String[] strArr = str.split("");
        String answer = "";
        Arrays.sort(strArr, Collections.reverseOrder());
        for(int i=0; i<strArr.length; i++){
            answer += strArr[i];
        }

        //0일경우 cnt와 XYnum[0]의 값이 같음.
        if(cnt == XYnum[0]) answer = "0";

        return cnt > 0 ? answer : "-1";
    }
}
```
