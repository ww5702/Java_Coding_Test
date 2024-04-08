수식의 우선순위는 6가지밖에 없다.   
해당 우선순위를 기준으로 계산을 하나씩 해준다.   
최대값을 반환한다.   

```
import java.util.*;
import java.util.Arrays;

class Solution {
    public long solution(String expression) {
        long answer = 0;
        ArrayList<Long> numbers = new ArrayList<>();    
        ArrayList<Character> operators = new ArrayList<>();
        String num = "";

        for(int i = 0; i < expression.length(); i++){
            if(expression.charAt(i) == '-' || expression.charAt(i) == '+' || expression.charAt(i) == '*'){
                operators.add(expression.charAt(i));
                numbers.add(Long.parseLong(num));
                num = "";
            }
            else{
                num += expression.charAt(i);
            }
        }
        numbers.add(Long.parseLong(num));
        // System.out.println(numbers.toString());
        // System.out.println(operators.toString());
        long[] result = new long[6];
        result[0] = Math.abs(calculate(numbers, operators, '+', '-', '*'));
        result[1] = Math.abs(calculate(numbers, operators, '+', '*', '-'));
        result[2] = Math.abs(calculate(numbers, operators, '-', '+', '*'));
        result[3] = Math.abs(calculate(numbers, operators, '-', '*', '+'));
        result[4] = Math.abs(calculate(numbers, operators, '*', '-', '*'));
        result[5] = Math.abs(calculate(numbers, operators, '*', '+', '-'));
        //System.out.println(Arrays.toString(result));
        return Arrays.stream(result).max().getAsLong();
    }
    public long calculate(ArrayList<Long> numbers, ArrayList<Character> operators, char first, char second, char third) {
        ArrayList<Long> result = new ArrayList<>();
        ArrayList<Long> nums = new ArrayList<>();
        ArrayList<Character> ops = new ArrayList<>();

        for(int i = 0; i < numbers.size(); i++){
            nums.add(numbers.get(i));
        }
        for(int i = 0; i < operators.size(); i++){
            ops.add(operators.get(i));
        }
        
        for (int i = 0; i < ops.size(); i++) {
            if (ops.get(i) == first) {
                long value = cal(nums.get(i), nums.get(i+1), first);
                nums.remove(i);
                nums.remove(i);
                nums.add(i, value);
                ops.remove(i);
                i--;
            }
        }
        for (int i = 0; i < ops.size(); i++) {
            if (ops.get(i) == second) {
                long value = cal(nums.get(i), nums.get(i+1), second);
                nums.remove(i);
                nums.remove(i);
                nums.add(i, value);
                ops.remove(i);
                i--;
            }
        }
        for (int i = 0; i < ops.size(); i++) {
            if (ops.get(i) == third) {
                long value = cal(nums.get(i), nums.get(i+1), third);
                nums.remove(i);
                nums.remove(i);
                nums.add(i, value);
                ops.remove(i);
                i--;
            }
        }
        Long value = nums.get(0);
        return value;
    }
    
    public long cal(long a, long b, char op){
        if(op == '+')
            return a + b;
        else if(op == '-')
            return a - b;
        else
            return a * b;
    }
}
```
