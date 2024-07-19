hashset과 left,right를 이용해서 풀이하는것같다.   
첫 제출 40점   
```
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] arr = Arrays.stream(br.readLine().split(" ")).mapToInt(Integer::parseInt).toArray();
        HashSet<Integer> set = new HashSet<Integer>();
        //System.out.println(set.toString());
        int result = 0;

        int start = 0, end = 0;
        while (end < n) {
            while (end < n && !set.contains(arr[end])) {
                //System.out.println(arr[end]);
                set.add(arr[end]);
                end += 1;
            }

            //System.out.println(set.toString());
            //System.out.println(start+" "+end);

            result = Math.max(result, end - start);

            if (end < n) {
                set.remove(arr[start]);
                start += 1;
            }
            
        }



        System.out.println(result);
    }
}
/*
10
1 4 6 8 7 3 2 1 4 5     

30
1 3 4 56 7 2 8 39 2 1 3 5 32 1 3 4 5 20 39 59 21 2 3 4 10 29 43 4 2 5
*/
```
