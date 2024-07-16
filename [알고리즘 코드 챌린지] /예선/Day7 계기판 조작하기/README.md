그냥 set을 만들어 +1씩 하면서 각각이 다른 숫자가 k개인지 확인   
하지만 80점 4개가 틀렸다.   
시간초과 발생은 아니었다.   

```
import java.util.*;
import java.io.*;


class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        int[] input = new int[2];
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());

        while (true) {
            n += 1;
            String arr = String.valueOf(n);
            Set<Character> check = new HashSet<>();
            for (char ch : arr.toCharArray()) {
                check.add(ch);
            }
            if (check.size() == k) break; 
        }   
        System.out.println(n);
    }
}
```
