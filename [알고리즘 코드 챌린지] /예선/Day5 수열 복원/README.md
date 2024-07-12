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
다시 풀이해보았다   
dfs를 실행하여 가지고있는 숫자로 합을 만들 수 있으면 패스   
없다면 새로추가된 값을 추가   
48점 갱신   
그릐고 시간초과 발생   

```
import java.util.*;
import java.io.*;
class Main {
    static boolean visited;
    static List<Integer> sumList;
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
        //System.out.println(Arrays.toString(sum));

        int[] result = new int[n];
        List<Integer> list = new ArrayList<>();
        List<Integer> ihave = new ArrayList<>();
        list.add(0);
        for (int i = 1; i < idx; i++) {
            //System.out.println("내가 가지고 있는 수"+ihave.toString());
            list.add(sum[i]);
            sumList = new ArrayList<>();
            dfs(ihave, 0, 0);
            Collections.sort(sumList);

            //System.out.println(list.toString());
            //System.out.println(sumList.toString());
            
            if (list.size() > sumList.size()) {
                ihave.add(list.get(list.size()-1));
            } else if (list.size() == sumList.size()){
                for (int j = 0; j < list.size(); j++) {
                    if (list.get(j) != sumList.get(j)) {
                        ihave.add(list.get(j));
                        break;
                    }
                }
            }

            if (ihave.size() == n) { break; }
        }

        for (int i = 0; i < n-1; i++) {
            System.out.print(ihave.get(i)+" ");
        }
        System.out.print(ihave.get(ihave.size()-1));

    }

    public static void dfs(List<Integer> ihave, int sum, int depth) {
        if (depth == ihave.size()) {
            sumList.add(sum);
            return;
        }

        dfs(ihave, sum+ihave.get(depth), depth+1);
        dfs(ihave, sum, depth+1);
    }
}
/*
정렬하여 가장 큰 수는 다 더했을때일테고 분명히
1 2 3 6
0 1 2 3 6 3 4 7 5 8 9 6 9 10 11 12
[0, 1, 2, 3, 3, 4, 5, 6, 6, 7, 8, 9, 9, 10, 11, 12]
2 4 6 8
0 2 4 6 8 6 8 10 10 12 14 12 14 16 18 20
[0, 2, 4, 6, 6, 8, 8, 10, 10, 12, 12, 14, 14, 16, 18, 20]
*/
```
