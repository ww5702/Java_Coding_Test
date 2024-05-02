좀 복잡해졌지만 기지의 크기가 2억 이므로 1중반복문으로 처리해야한다.   
따라서 기지국이 이미 설치되어있는 장소에서 영향이 없는 부분에 따라   
기지국을 설치해준다는 의미이다.   
```
class Solution {
    public int solution(int n, int[] stations, int w) {
        int answer = 0;
        int end = 0, mod = (w*2)+1;
        for (int i = 0; i < stations.length; i++) {
            if (i == 0) {
                int start = stations[i] - w - 1;
                if (start < 0) start = 0;
                if (start != 0) {
                    if (start%mod == 0) {
                        answer += start/mod;
                    } else {
                        answer += (start/mod)+1;
                    }
                }
                end = stations[i] + w + 1;
                //System.out.println(start+" "+answer);
            } else {
                int start = stations[i] - w - 1;
                if (end <= start) {
                    if ((start-end+1)%mod == 0) {
                        answer += (start-end+1)/mod;
                    } else {
                        answer += ((start-end+1)/mod) + 1;
                    }
                }
                end = stations[i] + w + 1;
                //System.out.println(start+" "+answer);
            }
        }
        //System.out.println(end);
        if (end <= n) {
            if ((n-end+1)%mod == 0) {
                answer += (n-end+1)/mod;
            } else {
                answer += ((n-end+1)/mod) + 1;
            }
            
        }
        return answer;
    }
}
```
를 좀 더 가독성있는 코드로 변환시킨게 다음과 같다.   

```
import java.util.*;
class Solution {
    public static int solution(int n, int[] stations, int w)
    {
        int count = 0;
        int state = 0;
        int left = 1;
        int newleft = 0;

        while(true) {
            if(state<stations.length && left >= stations[state] - w) {
                left = stations[state]+w+1;
                state++;
            }
            else {
                newleft = left+w;
                if( (state <= stations.length-2) && (newleft >= stations[state+1]-w))
                    newleft = stations[state+1]-w-1;

                left=newleft+w+1;
                count++;
            }
            if(left > n)
                break;
        }

        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        // System.out.println("Hello Java");

        return count;
    }
}

```
