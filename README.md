# Java_Coding_Test
[Java][프로그래머스] 알고리즘 풀이

```
<str>
추가(append)
str += "a"

substring
str.substring(start,end);

contains
str1.contains(str2) -> true or false

repeat
answer += ("h".repeat(3)); // hhh


<형변환>   
int와 double의 차이점은 Double은 64비트에 값을 저장하고, Int는 32비트에 값을 저장한다는 것이다.

int -> double
double b = (double) a;  // 55.0
double b = Double.valueOf(a);  // 55.0
int -> string
String s = Integer.toString(n);
String s = String.valueOf(n);

double -> int
int b = (int) a;
int b = b.intValue()
를 통해 변환시킬 수 있다.

array -> list
List<String> list = Arrays.asList(arr);

ch -> string
String.valueOf(ch);
str.toCharArray();

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

배열 자르기
Arrays.copyOfRange(arr, start, end+1);

배열 정렬
Arrays.sort(arr);
Arrays.sort(arr, Collections.reverseOrder());
오류 발생시 아래 예외 확인


<mapping>
java의 map
mapToInt(Integer::parseInt)

```

## 스트림에서 제공하는 기본 함수
```
스트림이란 자바 8 API에서 새로 추가된 기능이다.
쉽게 생각하면 데이터 컬렉션 반복을 멋지게 처리하는 기능이라고 생각하자.
filter, map, reduce, find, match, sort등 고차함수들을
컬렉션, 배열, I/O 자원

import java.util.Arrays;
public static void main (String [I args) {
  int [] intArr = {1, 2, 3, 4, 5};

  long count = Arrays.stream(intArr)
    .filter (n -> n%2 == 0)
    .count ();

  long sum = Arrays. stream(intArr)
    .filter (n -> n$2 == 0)
    .sum ();

  double avg = Arrays. stream(intArr)
    .filter (n -> n%2 == 0)
    .average ()
    .getAsDouble();

  int max = Arrays.stream (intArr)
    .filter (n -> n%2 == 0)
    .max ()
    .getAsInt ();

int min = Arrays.stream (intArr)
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

중복제거
int[] result = Arrays.streama(numbers)
    .distinct()
    .toArray();

int to string to [string] , sum
return Arrays.stream(String.valueOf(n).split(""))
    .mapToInt(Integer::parseInt)
    .sum();

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

## Collection의 element를 제거할때 주의할점
```
List<String> list = Arrays.asList(s1);
Arrays.asList()를 통해 생성한 리스트의 인덱스를 삭제할때
Exception in thread "main" java.lang.UnsupportedOperationException: remove
와 같은 오류메세지를 확인할 수 있다.

하지만 
List<String> list = new ArrayList<>(Arrays.asList(s1));
java.util.ArrayList로 감쌀때
성공하는 모습을 확인할 수 있다.

Arrays.asList는 구현되어 있지 않아 상위객체인 AbstractList에서 throw Exception 처리를 한것이다. 
```
## int배열 내림차순 오류
```
[Error] no suitable method found for sort(int[],java.util.Comparator<java.lang.Object>)
와 같은 오류가 발생할 수도 있다

primitive타입에 대한 comparator가 없기 때문인데
원시타입인 int배열에는 사용할 수 없고, 객체(integer)배열에서만 사용이 가능하다.

따라서 int[]를 integer[]로 바꾸면 사용이 가능하다
Integer[] newArray = Arrays.stream(arr).boxed().toArray(Integer[]::new);
```
