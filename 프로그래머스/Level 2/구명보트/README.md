보트에 탈 수 있는 사람은 최대 2명이라는 제한조건때문에 가능한 풀이방법이다.   

```
import java.util.Arrays;
class Solution {
    public int solution(int[] people, int limit) {
        int answer = 0;
        Arrays.sort(people);
        int index = 0;
        for (int i = people.length-1; i >= index; i--) {
            if (people[i] + people[index] <= limit) {
                answer += 1;
                index += 1;
            } else {
                answer += 1;
            }
        }
        return answer;
    }
}
```
