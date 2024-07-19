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
정답지와 풀이과정은 비슷한것같으나   
k가 10, 9일때의 예외과정을 포함시켰다.   

```
import java.util.Scanner;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String N = scanner.next();
        int K = scanner.nextInt();
        scanner.close();
        
        boolean[] digit = new boolean[10];
        int cnt = 0;
        
        if (K == 10) {
            System.out.println("1023456789");
        } else if (K == 9) {
            System.out.println("102345678");
        } else {
            while (cnt != K) {
                Arrays.fill(digit, false);
                cnt = 0;
                N = Integer.toString(Integer.parseInt(N) + 1);
                for (int i = 0; i < N.length(); i++) {
                    digit[N.charAt(i) - '0'] = true;
                }
                for (int i = 0; i < 10; i++) {
                    if (digit[i]) {
                        cnt++;
                    }
                }
            }
            System.out.println(N);
        }
    }
}
```
