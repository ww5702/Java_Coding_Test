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

replaceAll //asdf
str.replaceAll("asdf,"22"); // 22
여러개 지울때
str.replaceAll("[aeiou]","") //sdf
역도 가능 str.replaceAll("[^a-b]","") a~b빼고 다

자르기
str.charAt(i)

시작하는가 끝나는가
str.startsWith(str2) true / false
str.endsWith(str2) true / false

string 비교
== 쓰면 안된다
str.equals("asdf") true / false

index찾기
abcde
str.indexOf("b") // 1

<형변환>   
int와 double의 차이점은 Double은 64비트에 값을 저장하고, Int는 32비트에 값을 저장한다는 것이다.

[int -> double]
double b = (double) a;  // 55.0
double b = Double.valueOf(a);  // 55.0
[int -> string]
String s = Integer.toString(n);
String s = String.valueOf(n);
[int -> int array]
int[] digits = Stream.of(String.valueOf(num).split(""))
        .mapToInt(Integer::parseInt).toArray();

[double -> int]
int b = (int) a;
int b = b.intValue()
를 통해 변환시킬 수 있다.

[array -> list]
List<String> list = Arrays.asList(arr);
List list = new ArrayList(Arrays.asList(arr));
List<Integer> answer = new ArrayList<>();
        for (int num : arr) {
            answer.add(num);
        }

[array -> string]
String.valueOf(arr);

[list -> array]
Integer[] arr = list.toArray(new Integer[list.size()]);

[list -> int array]
int[] answer = list.stream().mapToInt(i -> i).toArray();

[ch -> string]
String.valueOf(ch);
str.toCharArray();

[ch -> int]
(int)c = ascii코드로 인해 48 과 같은 숫자가 되어서 여기에 - 48을 해주거나
Character.getNumericValue(c); -> 1,2,3 과 같이 반환된다.

[string -> array]
char[] arr = str.toCharArray();
string str = "happy birthday!"
System.out.println(str.split(""));
\s 는 공백을 의미 \s+ 는 공백 여러개를 의미
my_string.split("\\s+"); \ \s+ 를 붙여서 사용

[string -> int]
Integer a = Integer.valueOf(str);
Integer a = Integer.parseInt(str);

<소수점 올림, 반올림, 버림>
Math함수를 이용해 해결한다.
double pie = 3.141592;
Math.ceil(pie) // 4 올림
Math.round(pie) // 3 반올림
Math.floor(pie) // 3 버림

<대문자, 소문자, 앞뒤로 공백제거>
str.toUpperCase();
str.toLowerCase();
str.trim();

<배열>
java의 배열은 크기를 정해줘야 한다.
int[] answer = new int[arr.length]; 와 같이
int[] answer = {1,2,3};
int[] answer = IntStream.rangeClosed(0,n).toArray();

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

배열 contains
바로 contains를 사용할수는 없고 list로 변환 후 사용 가능하다.
Arrays.asList(arr).contains(n);

배열 subarr
잘라내는것이 아닌 복사
Arrays.copyOfRange(arr, 1, 5);

배열 복사 System.arraycopy
System.arraycopy(num_list, 0, newarr, 0, num_list.length);

배열 join
swift joined 처럼 String.joined("",arr); 로 합쳐서 string으로
출력해줄 수 있다.

<2차원 배열>
int[][] answer = {};
int[][] answer = new int[2][2];

<리스트>
List<String> arrlist = new ArrayList<>();

추가
arrList.add(str);
arrList.add(0,str);

정렬
Collections.sort(list);
Collections.sort(list, Collections.reverseOrder());
// 대소문자 구분없이 오름차순, 내림차순 a A B c 이렇게
Collections.sort(list, String.CASE_INSENSITIVE_ORDER);
Collections.sort(list, Collections.reverseOrder(String.CASE_INSENSITIVE_ORDER));

제거
list.remove(1);        //index1 제거
list.remove(Integer.valueOf(1));        // 값이 1인 첫번째값 제거
list.removeAll(Arrays.asList(Integer.valueOf(1)) // 1전부 제거

<mapping>
java의 map
mapToInt(Integer::parseInt)

<asciiCode>
char 값을 (int)c로 그저 출력해주면 그만
다시 돌아가는것 또한 (char)c 이다.
a = 97  A = 65
z = 122 Z = 90
0~9 = 48~57

<index 구하기>
list.indexOf(i);


<Dictionary>
import java.util.HashMap;
HashMap<String, String> dict = new HashMap<String,String>();
dict.put("aa","1");

출력
dict.get("aa");         // 1

```
## int vs integer
```
배열은 int형으로 사용하고 리스트에서는 Integer형으로 알맞게 사용해야한다.
int는 Primitive 자료형이다 즉 변수의 타입이다.
integer는 매개변수로 객체가 필요할때, 기본형 값이 아닌 객체로 저장해야할때 사용한다.
즉 int는 산술연상 가능, integer는 데이터를 wrapper할 경우에 사용

```

## 스트림에서 제공하는 기본 함수
```
스트림이란 자바 8 API에서 새로 추가된 기능이다.
쉽게 생각하면 데이터 컬렉션 반복을 멋지게 처리하는 기능이라고 생각하자.
filter, map, reduce, find, match, sort등 고차함수들을
컬렉션, 배열, I/O 자원

Arrays.stream -> import java.util.Arrays;
IntStream.rangeClosed() -> import java.util.stream.*;
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

배열에서 원하는 값 출력
return IntStream.rangeClosed(0, n)
    .filter(value -> value % 2 == 1)
    .toArray();

배열에서 조건에 따라 mapping하여 출력
return Arrays.stream(arr)
    .map(i -> k % 2 == 0 ? i + k : i * k)
    .toArray();

복잡하지만 삼항조건을 넣으면서까지도 가능하기도 하다
i가 50보다 크거나 같으면서 짝수라면 /2 를
i가 50보다 작거나 홀수라면 * 2를 하라.
return Arrays.stream(arr)
            .map(i -> i >= 50&&i%2 == 0 ?
                i / 2 : i < 50&&i%2 != 0 ? i * 2 : i)
            .toArray();

음수를 처음 발견하면 해당 index return, 없다면 -1
return IntStream.range(0, numList.length)
      .filter(i -> numList[i] < 0)
      .findFirst()
      .orElse(-1);

곱셈을 return
return Arrays.stream(intlist)
    .reduce((acc, i) -> acc * i)
    .getAsInt();

짝수인 수들만 제곱해서 더하여 return
return Arrays.stream(arr)
    .filter(i -> i%2 != 0)
    .map(i -> i * i)
    .sum();

x를 기준으로 string을 나눠 o의 갯수만큼 배열 return
return Arrays.stream(myString.split("x", myString.length()))
            .mapToInt(x -> x.length())
            .toArray();;
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
sb.reverse();           // 5a
 
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
