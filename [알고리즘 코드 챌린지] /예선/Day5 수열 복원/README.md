어차피 정렬을 한다면 하나씩 더했을때가 제일 구하기 쉬운 방법이라고 생각했다.   
하지만 20점   

```
import java.util.*;
import java.io.*;
class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine()," ");
        int idx = (int)Math.pow(2,n);
        int[] sum = new int[idx];
        for (int i = 0; i < idx; i++) {
            sum[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(sum);
        System.out.println(Arrays.toString(sum));

        int[] result = new int[n];

        for (int i = 0; i < n; i++) {
            result[i] = sum[(1<<(i+1))-1] - sum[(1<<i)-1];
        }


        //System.out.println(Arrays.toString(result));
        for (int i = 0; i < n; i++) {
            System.out.print(result[i]+" ");
        }
    }
}
/*
정렬하여 가장 큰 수는 다 더했을때일테고 분명히
1 2 3 6
0 1 2 3 6 3 4 7 5 8 9 6 9 10 11 12
*/
```
