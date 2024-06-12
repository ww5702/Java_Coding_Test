# Java_Coding_Test
[Java][프로그래머스] 알고리즘 풀이
```
반환형을 public int[] solution에서
publis List solution으로 바꿔도 된다는 사실
런타임 에러가 발생할 경우 -> 범위의 초과
따라서 for문 확인 혹은 int -> long으로 변환해보기
```
```
함수를 밑에서 또 선언할때
public static boolean visited[];
public int solution() {
        visited = new boolean[3];
        ~~~;
}
public static void ~~~() {
}
위와 같이 선언해줘야 변수를 쓸 수 있다.  
```
```
java에서의 구조체
class Point {
    int end;
    int cost;
    
    public Point(int end, int cost) {
        this.end = end;
        this.cost = cost;
    }
}
```
```
dfs에서 배열추가하여 재귀는 안되므로
dfs(int[] arr, int cnt) {
  if (cnt == k) { return; }
  for (int i = 0; i < n; i++) {
        arr[cnt] = i;
        dfs(arr, cnt+1);
  }
와 같이 하자
}
```
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
str.replaceAll("[^a-z0-9._-]","") a~z, 0~9, . _ - 빼고 다 
str.replaceAll("[.]{2,}","."); .이 2번이상 반복된것을 . 하나로


자르기
str.charAt(i)

시작하는가 끝나는가
str.startsWith(str2) true / false
str.endsWith(str2) true / false

string 비교
== 쓰면 안된다
str.equals("asdf") true / false

index찾기
abcdbe
str.indexOf("b") // 앞에서 b = 1
str.lastIndexOf("b") // 뒤에서 b = 4

<형변환>   
int와 double의 차이점은 Double은 64비트에 값을 저장하고, Int는 32비트에 값을 저장한다는 것이다.

[int -> double]
double b = (double) a;  // 55.0
double b = Double.valueOf(a);  // 55.0
[int -> string]
String s = Integer.toString(n);
String s = String.valueOf(n);
[int -> long]
Long l = new Long(num);
Long l = Long.valueOf(num);
[int -> int array]
import java.util.stream.*;
int[] digits = Stream.of(String.valueOf(num).split(""))
        .mapToInt(Integer::parseInt).toArray();

[double -> int]
int b = (int) a;
int b = b.intValue()
를 통해 변환시킬 수 있다.

[array -> list]
List<String> list = Arrays.asList(arr);
-> string은 되고 integer은 안됨
-> 단 위와 같이 리스트를 만들 경우 고정되어 있어 원소를 제거 할 수 없다.
List list = new ArrayList(Arrays.asList(arr));
List<Integer> answer = new ArrayList<>();
        for (int num : arr) {
            answer.add(num);
        }

[array -> string]
String.valueOf(arr);

[integer array -> int array]
int[] answer = Arrays.stream(arr).mapToInt(i -> i).toArray();

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
split(".")은 작동을 안하다.
. 은 무작위 한글자를 의미하므로
이스케이프 문자인\을 넣어야하고, String안에서 이스케이프 문자를 써주려면
\를 또 넣어줘야 한다.
따라서 split("\\.")이어야 한다.

str.chars(); 와 같이도 가능
s.chars().filter( e -> 'Y' == e).count();
와 같이 활용 가능

[string -> int]
Integer a = Integer.valueOf(str);
Integer a = Integer.parseInt(str);

[string -> long]
long num = Long.parseLong(str);

<소수점 올림, 반올림, 버림>
Math함수를 이용해 해결한다.
double pie = 3.141592;
Math.ceil(pie) // 4 올림
Math.round(pie) // 3 반올림
Math.floor(pie) // 3 버림

<max,min>
Math.max(a,b)
Math.min(a,b)

<세제곱근, 네제곱근>
Math.sqrt(4, 2.0) = 2이다.
하지만 세제곱근 네제곱근은 pow를 이용해야한다.
Math.pow(9, 1.0/num)

<대문자, 소문자, 앞뒤로 공백제거> - str
str.toUpperCase();
str.toLowerCase();
str.trim();
<대소문자> - char
Character.toUpperCase(char);
Character.toLowerCase(char);
대소문자인지 확인
Character.isUppcerCase(char);
Character.isLowerCase(char);

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
String word = String.join("", map); 로 띄어쓰기없이 합쳐서 출력 가능

배열 채우기 fill
Arrays.fill(arr, 0);         //0으로 배열 채우기

배열 출력
Arrays.toString(arr);

배열의 비교
배열의 비교 또한 == 연산자가 아닌
if (Arrays.equals(arr1, arr2)) {break;}
와 같이 사용해야 한다.
== 연산자는 해당 배열의 주소값을 가져오기에 같이라고 판단하지 않는다.

배열 firstindex
배열 그 자체로는 firstIndexOf를 사용할 수 없다.
int index = Arrays.asList(name).indexOf(p);
따라서 list로 변환후 사용이 가능하다.

<2차원 배열>
int[][] answer = {};
int[][] answer = new int[2][2];

출력
Arrays.deepToString(arr)

정렬
한가지만 비교
o1-o2 = 오름차순
o2-o1 = 내림차순
Arrays.sort(answer, (o1,o2) -> {
                return o1[1] - o2[1];
            });

Arrays.sort(failure, (o1, o2) -> {
            if(o1[1] == o2[1]) {
                return Double.compare(o1[0], o2[0]);
            } else {
                return Double.compare(o2[1], o1[1]);
            }
        });
만약 [1]값들이 같다면 [0]의 조건들로 오름차순, 아니라면[1]의 조건으로 오름차순

Arrays.sort(tickets, (o1,o2) -> {
            if (o1[0].equals(o2[0])) {
                return o1[1].compareTo(o2[1]);
            } else {
                return o1[0].compareTo(o2[0]);
            }
        });
string 2차원 배열이라면 equals로 사용하고, o1[1].compareTo(o2[1])
처럼 사용해야 한다.
o1[0] o2[0]이 같다면 [1]의 값을 기준으로 오름차순,
같지 않다면 [0]값을 기준으로 오름차순이다.

o2 - o1 = 내림차순
o1 - o2 = 오름차순
Arrays.sort(failure, (o1,o2) -> (o1[0] == o2[0] ? o1[1] - o2[1] : o1[0] - o2[0]));
람다식으로도 가능

복사
int[][] dp = land 와 같이 한다면 얕은복사가 되어
값이 변경되면 같이 변경된다 따라서 깊은 복사를 사용해야 한다.
int[][] dp = new int[land.length][land[0].length];
for (int i = 0; i < land.length; i++) {
        dp[i] = land[i].clone();
}


<리스트>
List<String> arrlist = new ArrayList<>();
List<int []> 2list = new ArrayList<>(); 2차원리스트
ArrayList<Point>[] listPoint = new ArrayList[N+1]; 구조체를 2차원리스트로 선언
List.of(1) 선언과 동시에 초기화

추가
arrList.add(str);
arrList.add(0,str);
2list.add(1차원배열);
listPoint.add(new Point(1,0)); 

변경
list.set(0, 3);

출력
list.get(0);

index
list.indexOf(2);                // firstIndex
list.lastIndexOf(2);            // lastIndex

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

출력
list.toString();

isEmpty
list.isEmpty();

contains
list.contains("a")



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
HashMap<String, Integer> map = new HashMap<>();
map.put("asdf", map.getOrDefault("asdf", 0) + 1);
-> asdf라는 string을 저장하는데 만약 없던 값이라면 0으로 초기화 후 +1하여 저장

출력
dict.get("aa");         // 1

contains
hashMap.containsKey("A");
hashMap.containsValue("BANANA")

삭제
testMap.remove("red");
testMap.clear(); 전체 삭제



전체 순환
map.forEach((key, value) -> {
            System.out.println(""+key+" "+value);
        });

2번째 방법
for ( Map.Entry<String, Integer> entry : map.entrySet()) {
            if (entry.getValue() != 0) {
                answer = entry.getKey();
                break;
            }
}
이 방법이 변수를 바꿔줄수도 break를 걸수도 있어 편하다.

정렬
list로 변환후 정렬할수도 있고 tree로도 정렬할 수 있다
stream또한 가능
List<String> keySet = new ArrayList<>(map.keySet());
List<Integer> valueSet = new ArrayList<>(map.values());
key값을 기준으로 오름차순, 내림차순
Collections.sort(keySet);
Collections.reverse(keyset);
value값을 기준으로 오름차순, 내림차순
keySet.sort((o1, o2) -> map.get(o1).compareTo(map.get(o2)));
keySet.sort((o1, o2) -> map.get(o2).compareTo(map.get(o1)));

합치기
map2를 map1에 각각 더해주기
map2.forEach((key, value) -> map1.merge(key, value, (v1,v2) -> v1 + v2));
map1에 map2의 값이 있다면 덮어씌우고 없다면 추가
map2.forEach((key, value) -> map1.merge(key, value, (v1, v2) -> v2));

<Set>
import java.util.*;
HashSet<Integer> set = new HashSet<Integer>();

추가
set.add(1);

형 변환
Integer[] arr = set.toArray(new Integer[0]);
Set<String>set = new HashSet<>(list);

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
List<String> distinct_id_list = Arrays.stream(report).distinct().collect(Collectors.toList());

int to string to [string] , sum
return Arrays.stream(String.valueOf(n).split(""))
    .mapToInt(Integer::parseInt)
    .sum();

string[] to int[]
return Arrays.stream(strArr)
        .mapToInt(Integer::parseInt)
        .toArray();

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

## 입출력 
```
// Scanner 클래스 불러오기
import java.util.Scanner;

// Scanner 클래스의 인스턴스 생성하기
Scanner scanner = new Scanner(System.in);
// nextLine() 메서드를 통해 입력 값 변수에 저장하기
String inputValue = scanner.nextLine();

nextLine() : 문자열을 입력받는 메서드
nextInt() : 정수형 데이터를 입력받는 메서드
netxFloat() : 실수형 데이터를 입력받는 메서드
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
sb.charAt(0);           // 5

sb.toString() -> string으로 출력
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

쉽게 생각하면 고정된 배열값을 list로 만들어주어 삭제할 수 없다는 오류가 나온것이다.
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
## 2진수 10진수 등등 진수변환
```
2진수, 8진수등을 다시 숫자로 변환
int num = Integer.parseInt(value,2);
int num = Integer.parseInt(value,8);


(String)숫자를 2진수로 8진수 등등 원하는 진수로 변환
"4" -> "110" 으로 string -> string
2 진수
String num = Integer.toBinaryString(value);
8 진수 Integer.toOctalString(i);
16진수 Integer.toHexString(i);
3 진수 String threeJin = Integer.toString(n,3);
위와 같이 3을 2,3,4,5,6 등으로 응용 가능

true 인 값을 찾을 수 있는 bitCount
int a = Integer.bitCount(num);
1101 -> 3

Integer.toBinaryString(arr1[i] | arr2[i])
11000
 0100
이 두개를 위의 문법으로 사용할 경우
11100으로 반환된다.   
```
## 스택
```
import java.util.Stack;

Stack<Integer> stackInt = new Stack<>();

push
stack.push(c);
stack.add(c);

pop
stack.pop();

peek = last!
stack.peek();
만약 비었을시 오류

isEmpty
stack.isEmpty();

search
스택에서 해당 위치를 반환한다. 이때 반환하는 index는 빠져나올 순서를 의미한다.
없다면 -1을 뽑아내고, 여러개라면 가장 먼저 빠져나올 인덱스가 나온다.
stack.search(num);

```
## 우선순위 큐
```
FIFO로 우선순위가 높은 데이터가 먼저 나간다.
import java.util.PriorityQueue;
//낮은 숫자가 우선 순위인 int 형 우선순위 큐 선언
PriorityQueue<Integer> priorityQueueLowest = new PriorityQueue<>();
//높은 숫자가 우선 순위인 int 형 우선순위 큐 선언
PriorityQueue<Integer> priorityQueueHighest = new PriorityQueue<>(Collections.reverseOrder());

  //2차원배여롤 이루어진 큐에서 [1]을 기준으로 오름차순
PriorityQueue<int[]> q = new PriorityQueue<>((a, b) -> a[1] - b[1]);

push
priorityQueue.add(1);
priorityQueue.offer(10);

pop
// 첫번째 값을 반환하고 제거 비어있다면 null
priorityQueue.poll();
// 첫번째 값 제거 비어있다면 예외 발생
priorityQueue.remove(2); -> pq를 탐색해서 첫번째 2제거
priorityQueue.removeEq(2); -> 2 전부 제거   

// 첫번째 값을 반환만 하고 제거 하지는 않는다.
// 큐가 비어있다면 null을 반환
priorityQueue.peek();
// 첫번째 값을 반환만 하고 제거 하지는 않는다.
// 큐가 비어있다면 예외 발생
priorityQueue.element();
// 초기화
priorityQueue.clear();      
```
## 큐
```
import java.util.LinkedList; //import
import java.util.Queue; //import
Queue<Integer> queue = new LinkedList<>(); //int형 queue 선언, linkedlist 이용
Queue<String> queue = new LinkedList<>(); //String형 queue 선언, linkedlist 이용

메서드들은 우선순위 큐와 같다. 
```
## 유클리드 호제법
```
최대공약수
public int gcd(int a, int b) {
        if (b == 0) { return a; }
        return gcd(b, a%b);
}
최소공배수
public int lcm(int a, int b) {
        return a * b / gcd(a,b);
}
```
## replaceAll 표현식
[참고 사이트](https://zhfvkq.tistory.com/5#:~:text=[JAVA]%20%EC%A0%95%EA%B7%9C%20%ED%91%9C%ED%98%84%EC%8B%9D(replaceAll)%20*%20%2D%20%EB%8C%80%EC%83%81%20%EB%AC%B8%EC%9E%90%EC%97%B4,:%20str.replaceAll(%22[%5E0%2D9]%22%2C%22%22);%20*%20%EC%88%AB%EC%9E%90%20%EC%A0%9C%EA%B1%B0%20:%20str.replaceAll(%22[0%2D9]%22%2C%22%22);)   
```

```
## Iterator 
```
자바 컬렉션에 저장되어 있는 요소들을 순회하는 인터페이스이다.
컬렉션 프레임워크에 공통으로 사용이 가능하고 사용법이 간단하기에 사용한다.
Iterator<T> iterator = Collection.iterator();
사용가능한 메서드는
hasNext(), next(), remove()가 끝이다.
ex)
Iterator<Integer> it = list.values().iterator();
while(it.hasNext()) {
        answer *= it.next();
}
```
## Pattern 클래스
자바의 정규 표현식이 컴파일된 클래스이다.   
```
import java.util.regex.*;
Pattern p = Pattern.compile("a...b");
일정한 패턴의 조건에 일치하는 문자열을 찾는 것이다.

Pattern pat = Pattern.compile("정규식") -> 패턴을 정의한 후
Matcher match = pat.matcher("여기에 조사할 문자열") -> 정의된 패턴에 매치 되는 값을 저장한다
match.find() -> 매치된 값이 있다면true, 아니라면 false 이다
match.group() -> 매치된 값을 반환한다.

Pattern p = Pattern.compile("([a-z\\s.-]+)([0-9]{1,5})");
라고 했을때 위는
a~z까지와 - , . 이 포함된 그룹하나
0~9까지 1~5번 포함된 그룹둘 이라는 뜻이다.
img250 이 있을때
Matcher m = p.matcher("img250".toLowerCase());
m.find();
System.out.println(m.group(2));
이라면 m.find()가 true이고, group2인 250이 반환된다.   
```
## 비트 연산자
```
| (OR 연산자)
& (AND 연산자)
^ (XOR 연산자) -> 둘다 0이거나 1일경우 0 하나라도 다르다면 1   
~ (비트 전환 연산자)
<< >> (쉬프트 연산자)
```
## 그래프 인접리스트 구현
```
swift에서 사용하던 튜플식으로 구현하는법
선언 후 초기화까지 해야 한다.
ArrayList<Integer>[] list = new ArrayList[n+1];
for (int i = 0; i <= n; i++) {
        list[i] = new ArrayList<>();
}
for(int[] edge : edges) {
        list[edge[0]].add(edge[1]);
        list[edge[1]].add(edge[0]);
}


더 쉽게도 가능한데
int[][] matrix = new int[n + 1][n + 1];
for(int[] edge : edges) {
        matrix[edge[0]][edge[1]] = 1;
        matrix[edge[1]][edge[0]] = 1;
}
연결된 부분은 1로 2차원배열로도 표현이 가능하다
단점은 공간 복잡도가 O(n^2)이다
```
## union-find
만약 최단거리를 묻거나 그런 문제일때   
bfs사용도 있지만 union-find가 가능한지 확인해보는것도   
좋은 방법이다.   
```
static int[] parent;
public static void union(int a, int b) {
        a = find(a);
        b = find(b);
        if(a != b)
                parent[b] = a;
        }
public static int find(int x) {
        if(parent[x] == x) return x;
        return find(parent[x]);
}
main에서 선언 후 초기화까지 진행
parent = new int[n];
for (int i = 0; i < parent.length; i++) parent[i] = i; 
```
## 깊은 복사 vs 얕은 복사   
```
ArrayList<String> list = new ArrayList<>();
list.add("a");
ArrayList<String> newList = list;
newList.add("b");
System.out.println(list.toString()) // a b
System.out.println(newList.toString()) // a b

따라서 깊은 복사를 해야 따로 저장이 가능
ArrayList<String> newList = new ArrayList<>(list);

배열의 깊은복사
int[] A = {1,2,3,4,5};
int[] B = A.clone();

위와 같이 사용 가능 하지만 2차원배열은 불가
int[][] A = {{1,2,3,4,5}, {6,7,8,9,10}};
int[][] B = new int[A.length][A[0].length]; // B 선언

for(int i = 0; i < A.length; i++){ // 2중 반복문
        for(int j = 0 ; j < A[0].length; j++){
                B[i][j] = A[i][j];
        }
}

위와 같이 깡으로 복사 혹은
int[][] C = new int[A.length][A[0].length]; // C 선언,

for(int i = 0; i < A.length; i++){ // 반복문 + ArrayCopy
        System.arraycopy(A[i], 0, C[i], 0, C[i].length);
}
arraycopy 사용

```

