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
똑같이 double -> int 또한
int b = (int) a;
int b = b.intValue()
를 통해 변환시킬 수 있다.

<소수점 올림, 반올림, 버림>
Math함수를 이용해 해결한다.
double pie = 3.141592;
Math.ceil(pie) // 4 올림
Math.round(pie) // 3 반올림
Math.floor(pie) // 3 버림

str 배열로 바꾸기
string str = "happy birthday!"
System.out.println(str.split("");  // h a p p y 띄어쓰기 b i r t h d a y !

<배열>
java의 배열은 크기를 정해줘야 한다.
int[] answer = new int[arr.length]; 와 같이

배열 순환
for (int i: arr) {
  System.out.println(i);
}


```

## 스트림에서 제공하는 기본 함수
```
import java.util.Arrays;
public static void main (String [I args) {
  int [] intArr = {1, 2, 3, 4, 5};

  long count = Arrays.stream(intArr)
    .filter (n -> n%2 == 0)
    .count () ;

  long sum = Arrays. stream(intArr)
    .filter (n -> n$2 == 0)
    .sum ();

  double avg = Arrays. stream(intArr)
    .filter (n -> n%2 == 0)
    .average ( )
    .getAsDouble();

  int max = Arravs.stream (intArr)
    .filter (n -> n%2 == 0)
    .max ( )
    .getAsInt ();

int min = Arravs.stream (intArr)
    .filter (n -> n%2 == 0)
    .min ()  
    .getAsInt ();

int first = Arrays.stream (intArr)
    .filter (n -> n%2 == 0)
    .findFirst()
    .getAsInt ();

int[] result = Arrays.stream(numbers)
    .map(i -> i*2)
    .toArray();

```

## length, length(), size() 차이점
```
length
arrays 즉 배열의 길이를 알고자 할때 사용
length()
문자열의 길이를 알고자 할때 사용
size()
arrayList, set etc,,, 등 컬렉션프레임워크 타입의 길이를 알고자 할때 사용
```

## StringBuilder?
```
많은 문자열을 연결하면 중간 문자열 객체가 생성되어 비효율적인 코드가 생성된다.
StringBuilder는 변경 가능한 문자열을 만들어주기 때문에
String을 합치는 작업 시 하나의 대안이 될 수 있다.

StringBuilder sb = new StringBuilder();
sb.append("aaa");        // aaa
sb.insert(2, "ccc");     // aaccca
sb.replace(2,4, "5");    // aa5ca (index 2~3까지를 "5"로 교체
sb.substring(3);         // ca
sb.substring(1,2);       // a5
sb.deleteCharAt(1);      // a5ca
sb.delete(2, sb.length())// a5
sb.toString();           // a5
sb.reversed();           // 5a
 
```
