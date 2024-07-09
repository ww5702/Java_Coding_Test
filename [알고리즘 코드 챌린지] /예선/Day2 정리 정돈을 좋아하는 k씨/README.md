첫째날보다 훨씬 쉬웠다.   
쉬운걸보니 첫번째 문제를 너무 어렵게 푼거같기도..   
배열을 잘라서 해당 배열 정렬후 idx값을 출력해주면 된다.   
최대 10,000 배열을 500번 테스트케이스가 존재하므로   
구현으로 코딩하여도 풀이가 가능하다.   

```
import java.io.*;
import java.util.*;
class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        int n = Integer.parseInt(st.nextToken());
        int k = Integer.parseInt(st.nextToken());
        //System.out.println(n+" "+k);

        // 배열 입력
        String[] input = br.readLine().split(" ");
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(input[i]);
        }

        // 테스트케이스 실행
        for (int i = 0; i < k; i++) {
            String[] value = br.readLine().split(" ");
            int start = Integer.parseInt(value[0]);
            int end = Integer.parseInt(value[1]);
            int idx = Integer.parseInt(value[2]);

            // 부분 배열 생성
            int[] tempArr = new int[end-start+1];
            System.arraycopy(arr, start-1, tempArr, 0, tempArr.length);
            // 잘라낸 배열 정렬
            Arrays.sort(tempArr);
            System.out.println(tempArr[idx-1]);
        }
    }
}
```
