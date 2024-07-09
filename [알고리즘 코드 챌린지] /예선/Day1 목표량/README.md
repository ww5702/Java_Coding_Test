주어진 숫자의 다음으로 큰 숫자를 주어진 숫자 내에서 고르는 문제이다.   
436 이면 634이다.   
84373427이면 84373472이고,   
865631이면 866135이다.   
따라서 뒤에서부터 순환하며 서로 바꿔줘야할 idx를 찾고 변경 후   
나머지 뒤에서부터는 내림차순으로 숫자를 찾는다.   

```
import java.io.*;
import java.util.*;
import java.util.stream.*;

class Main {
    public static void main(String[] args) throws IOException{
        // 숫자 입력받기
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        int num = Integer.parseInt(bf.readLine());

        // 배열로 변환
        int[] digits = Stream.of(String.valueOf(num).split("")).mapToInt(Integer::parseInt).toArray();
        //System.out.println(Arrays.toString(digits));
        //System.out.println(num);

        // 맨 뒤에서부터 서로 위치 바꿀 idx 찾기
        int[] idxArr = findNextNum(digits);
        int temp = digits[idxArr[0]];
        digits[idxArr[0]] = digits[idxArr[1]];
        digits[idxArr[1]] = temp;

        // 바꾼idx 뒤부터 내림차순 정렬
        int[] copyArr = new int[digits.length - idxArr[0] - 1];
        System.arraycopy(digits, idxArr[0]+1, copyArr, 0, copyArr.length);
        Arrays.sort(copyArr);
        int[] answer = new int[digits.length];
        for (int i = 0; i <= idxArr[0]; i++) {
            answer[i] = digits[i];
        }
        for (int i = idxArr[0]+1; i < digits.length; i++) {
            answer[i] = copyArr[i - (idxArr[0]+1)];
        }

        // int[] -> str
        String answerStr = "";
        for (int i = 0; i < digits.length; i++) {
            answerStr += String.valueOf(answer[i]);
        }
        System.out.println(answerStr);
    }

    // idx 바꾸기
    public static int[] findNextNum(int[] arr) {
        int[] result = new int[2];
        int idx = arr.length - 2;
        while (idx >= 0 && arr[idx] >= arr[idx+1]) {
            idx -= 1;
        }
        int idx2 = arr.length - 1;
        while (arr[idx2] <= arr[idx]) {
            idx2 -= 1;
        }
        result[0] = idx;
        result[1] = idx2;

        return result;
    }
}
```
