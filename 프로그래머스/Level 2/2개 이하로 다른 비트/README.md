예제 7보다는 큰 숫자이니 1을 증가시킨다 ++;   
증가된 숫자와 원래 숫자를 XOR 연산으로 비교한다 ^   
1이 둘중 하나라도 들어가 있으면 1을 반환한다.   
7 ^ 8 = 1111 이 나온다.   
2개 이하로 다른 비트이므로 오른쪽 쉬프트 연산자를 통해 이동한다 >>> 2    
0011을 증가시킨 숫자에 더해준다 8 + 3 = 11   
만약 3개 이하로 다른 비트면 >>>3을해주고 5개 이하라면 >>>5를 해준다.   
```
class Solution {
    public long[] solution(long[] numbers) {
        long[] answer = numbers.clone();
        for(int i = 0; i< answer.length; i++){
            answer[i]++;
            answer[i] += (answer[i]^numbers[i])>>>2;
        }
        return answer;
    }
}
```
