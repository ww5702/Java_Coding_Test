구현 문제이다.   
처음에는 각도로 계산하려했으나 말이 안된다고 생각했다.   
분침이 한바퀴 도는동안 초침을 몇번만나고,   
시침이 한바퀴 도는동안 초침을 몇번 만나는지 계산한뒤,   
현재 시간에 울리는지를 파악하여 계산한다.   

```
class Solution {
    public int solution(int h1, int m1, int s1, int h2, int m2, int s2) {
        /*
        초침이 60번 가야 분이 1분 분이 60분 가야 시간이 1이니까
        초침이 1초 가면 분이 60분의1 움직이고 시간이 3600분의 1움직임
        */
        int answer = -1;
        int start = toSec(h1,m1,s1);
        int end = toSec(h2,m2,s2);
        
        // 끝나는 시간까지 몇번 울리는지 - 시작시간까지 몇번 울리는지 + 현재시간이 울리는지
        answer = cal(end) - cal(start);
        
        // 만약 시작시간이 초침과 겹친다면 -1
        if (start*59%3600 == 0 || start*719%43200 == 0) {
            answer += 1;
        }
        return answer;
        
    }
    public int cal(int time) {
        /*
        분침이 한 바퀴 도는동안 초침이랑 59번 겹친다
        3600번중 59번 울린다
        즉 현재시간 x 59 / 3600으로 몇번 울리는지 알 수 있다.
        */
        int mValue = time * 59 / 3600;
        /*
        시침은 한바퀴 도는동안 60x60x12 = 43200초가 걸린다.
        60초에 시침이 한번 겹치고 60분 12시 겹친다고 할 수 있다.
        60 x 12 이지만 시침이 한번 움직이므로 -1 = 719
        */
        int hValue = time * 719 / 43200;
        /*
        정각은 분침과 시침이 일치하므로 -1 씩 해줘야한다.
        43200이 넘는다면 2번 겹치고, 아니라면 1번 겹친다
        */
        int a = time >= 43200 ? 2 : 1;
        return mValue + hValue - a;
    }
    public int toSec(int h, int m, int s) {
        return h*3600 + m*60 + s;
    }
}
```
