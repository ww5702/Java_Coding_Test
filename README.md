# Java_Coding_Test
[Java][프로그래머스] 알고리즘 풀이

```
<형변환>   
int와 double의 차이점은 Double은 64비트에 값을 저장하고, Int는 32비트에 값을 저장한다는 것이다.
int a = 55;
double b = (double) a;  // 55.0
이렇게도 되지만
double b = Double.valueOf(a);  // 55.0
이 방법도 직접적이고 반복저긍로 구현하기 쉽다.

<소수점 올림, 반올림, 버림>
Math함수를 이용해 해결한다.
double pie = 3.141592;
Math.ceil(pie) // 4 올림
Math.round(pie) // 3 반올림
Math.floor(pie) // 3 버림
```
