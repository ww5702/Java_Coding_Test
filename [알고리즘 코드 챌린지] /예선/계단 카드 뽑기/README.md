hashset과 left,right를 이용해서 풀이하는것같다.   
첫 제출 40점   

```
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        StringTokenizer st = new StringTokenizer(br.readLine()," ");
        HashSet<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            set.add(arr[i]);
        }
        HashMap<Integer, Integer> dict = new HashMap<Integer, Integer>();
        Iterator<Integer> iterSet = set.iterator();
        while(iterSet.hasNext()) {
            int next = iterSet.next();
            dict.put(next, dict.getOrDefault(next, 0));
        }
        System.out.println(dict);
        
        int notOne = 0;
        int cnt = 0;
        int result = 0;

        int start = 0, end = 0;
        while (end < n) {
            int value = dict.get(arr[end]);
            System.out.println(arr[end]);
            System.out.println(start+" "+end);
            
            if (value == 0) {
                dict.put(arr[end], value + 1);
                result = Math.max(result, end-start+1);
                end += 1;
            } else {
                dict.put(arr[start], value - 1);
                start += 1;
            }
            System.out.println(dict);
            System.out.println(result);
            
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
