이분 탐색처럼 start, end를 운영하여 더 작으면 더하는 숫자를 늘리고   
더 커지면 밑에서부터 빼주는 형식을 반복해주었다.   

```
class Solution {
    public int solution(int n) {
        int answer = 0;
        int start = 1;
        int end = 1;
        int sum = 0;
        while (start <= n+1) {
            //System.out.println(start+" "+end+" "+sum);
            if (sum < n) {
                sum += start;
                start += 1;
            } else if (sum > n) {
                sum -= end;
                end += 1;
            } else if (sum == n) {
                answer += 1;
                sum += start;
                start += 1;
                //System.out.println(answer);
            }
        }
        return answer;
    }
}
```
