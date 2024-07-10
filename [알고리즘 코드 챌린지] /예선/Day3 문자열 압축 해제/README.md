문제를 해석하는데 더 오래 걸린 문제이다.   
11(18(72(7)))   
일때   
7   
괄호 닫기가 나왔을때   
바로 앞 2를 뽑아서 2번 반복된 값을 저장   
77   
그리고 (가 나올때까지 추가 7 + 77   
(가 나오면 pop()   
그리고 다음 진행   
다시 )가 나옴   
바로 앞 8을 뽑아서 8번 반복된 값을 저장   
777 * 8   
그리고 (가 나올때까지 앞에 추가 1 777*   
(가 나왔으니 pop()   
위와 같은 방식으로 11 777 * 8번 으로 26이 나오게 된다.   

```
import java.util.*;
import java.io.*;
class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        String input = bf.readLine();
        
        System.out.println(decompress(input));

    }

    public static int decompress(String input) {
        Stack<String> stack = new Stack<>();
        StringBuilder currentString = new StringBuilder();
        StringBuilder result = new StringBuilder();

        for (char ch : input.toCharArray()) {
            if (ch == ')') {
                currentString.setLength(0);
                while (!stack.peek().equals("(")) {
                    currentString.insert(0, stack.pop());
                }
                stack.pop(); // Remove the '(' from the stack
                
                int repeatCount = Integer.parseInt(stack.pop());
                String temp = currentString.toString().repeat(repeatCount);
                stack.push(temp);
            } else {
                stack.push(Character.toString(ch));
            }
        }

        while (!stack.isEmpty()) {
            result.insert(0, stack.pop());
        }
        //System.out.println(result.toString());
        return result.length();
    }
}
```
