## JAVA DATA TYPE

### Primitive Data Type

     숫자형 
     - 정수형(byte[1], short[2], int[4], long[8])
     - 실수형(float[4], double[8])

     문자형 
     - char[2byte]

     논리형 
     - boolean[1bit]
     
**자료형의 크기비교**

* 정수형 < 실수형(sign bit, 지수부 bit, 가수부 bit) 
*  1  10 ^ 8 -> 이렇게 효율적으로 관리할 수 있다. 
* (1, 10, 8만 기억하면 가능)
* float(1, 8, 23) < double(1, 11, 52) 
      
### Reference Data Type(=Non-Primitive Type)
- 실제 따라가서 참조하는 크기는 다르겠지만 해시된 주소값이니까 참조타입 상관없이 4바이트 할당



## JVM 
    메모리 영역 
    -  METHOD, HEAP, STACK

    METHOD 영역
    - 적재되면 계속 유지하는 성격이 강한 애들이 올라감
    - Byte code, Literal
 
    HEAP 영역
    - 생성된 객체 관리
 
    STACK 영역
    - 각 메소드 실행되는 것들이 쌓임
    - 스택이 여러개가 될 수 있음, 각 쓰레드마다 독자적인 스택 
    
```ex) int i = 10; String s = new String("hi");```

- STACK에 i = 10. s = 0x11111... HEAP에 스트링 객체가 들어가 있고 거기를 참조하는 레퍼런스값



## TYPE CASTING 형변환

### 1. 순서

*  byte < char, short < int < long < float < double 
* boolean은 어떠한 타입과도 호환 x
 
### 2. 묵시적 형변환(작->큰, up casting)

- 자동으로 수행
- long + float -> float + float 

### 3. 명시적 형변환(큰->작, down casting) 
- 직접 형변환을 명시
- 데이터 손실 우려때문에 자동으로 x, 형변환 연산자 필요
- long + float -> long + (long) float = long + long
- 객체간의 형변환
   - 상속관계를 통해 크고 작음을 따짐. 관계가 성립되는 계층구조에 따라 형변환 가능



## 조건 분기문
#### 1. if문 								 
- 조건식이 true/false 결과, 조건 성립이 빈번한 것부터 배치

### 2. switch문
- 값의 동등비교에 다중분기
- 해당케이스로 바로 건너뛰므로 동작시 더 빠르다고함(string 가능)



## 반복문
### 1. for문 (선조건 후수행)	
    for(초기치;조건식;증감치){ 반복내용; }
### 2. while문 (선조건 후수행) 
    횟수가 명확하지 않을 때
    초기치; while(조건식) { 반복내용; 증감치; }
### 3. do while문  (선수행 후조건 후수행)
    초기화; do{ 반복내용; } while(조건식);
       
### 4. 제어 키워드 
>* label  
탈출 또는 건너뛸 위치를 제어

>* break       	   
반복문을 끝내고 탈출

>* continue     
   다음 반복으로 건너뛰기 - 무한루프 조심(증감치 고려) 
   while(++i<=10) 이런식으로 처리하는게 나을 수도 있다!
   
   
   
## 배열 

### 동형 집합, 참조타입 -> object!
  
### 배열의 목적 
> 집합으로 만들어 관리하는 것 

> 일괄처리, 집합으로써의 표현, 공간의 효율적인 사용..)

> index가 zero base인 이유 
   
> address = address + offset * dataTypeSize

> 배열 안에 객체가 있으면, 그 객체가 참조하는 부분이 있고, 그 참조하는 부분에서 참조하는... 다차원 배열의 느낌 = 참조타입
   
### 배열 안에 있는 데이터에 따른 형태
1. Primitive Type Array

2. Reference Type Array
    
### 배열 생성하기
* DATA_TYPE[] arr = new DATA_TYPE[ARRAY_SIZE]

 - 가상으로 객체를 가리킬 수 있는 인위적인 값인 **reference**가 반환
 - reference != address (가비지 컬렉션이랑 관련있다고 함)

* 객체는 생성위치 무관하게 HEAP에올라감 

 - HEAP에서 항상 객체 생성시 default 초기화가 이뤄짐(0,0.0,false,'')

 - 내가 갖고 있는 레퍼런스가 실제 주소가 아니므로 찾아가는 과정을 하다보니 많이 참조 또는 반복 시 성능이 떨어질 수 있음(오버헤드)
   => 응집도를 높여야함 (타객체 참조 최소화)

 - JVM안에 HEAP에는 GC가 청소해버림. 버리면 안되는 것만 모아두고 싹 치우는 방식임




### HEAP 영역
 * | young 1 | young 2 | old |

     1. Heap이 다 차면 지워지면 안되는 사용중인 객체만 young2로 복사
     2. swap 위해 한쪽을 비움. young끼리 이동하는 것이 마이너 GC
     3. 기준을 주고(일정 카운팅), 어차피 안버리는 애는 old에 넣어둠  
     4. old에 있는 애들도 날려버리는 것이 메이저 GC

   
### 다차원 배열
 * 2차원 배열은 reference를 원소로 갖고 있는 것
   
  - int[][] arr= new int[2][4] 배열을 원소로 갖는 배열
  - 레퍼런스를 주고 받는 것
  
 * 자바에서 배열은 length라는 상수가 있기때문에 크기정보를 따로 줄 필요가 없음
  - 객체 배열 사이즈는 고정. Collection으로 하면 크기가 가변적으로 되지만, 배열은 아님
  - 자바는 객체가 런타임시간에 만들어지므로 배열 크기를 변수로 줘도 됨


### for each 구문
      배열 원소 각각에 대해서 반복문을 처리할 수 있도록 함
      for(배열타입 원소 : 배열) 
      iterable을 만족하고 있으면 for each 전부 쓸 수 있음
      
      
      
      
## 레퍼런스 배열 정렬 

* 내부의 어떤 것을 순서로 해야하는지 알 수 없기 때문에, 비교기능을 객체들이 갖고 있어야함.

 - 2가지 방식
   comparable interface 구현하고 있어야함  compareTo(-1,0,1로 결과값 반환) 메소드 재정의해야함 
   Comparator class 구현


### Comparable(스스로 비교)
  * 원소들이 구현 (동일한 타입의 다른녀석과 자기 자신을 비교할 기준을 스스로 구현하고 있음)
     
     
### Comparator(남이 비교해줌)
 ``` 별도로 비교 판단 해주는 비교자
  Student 클래스가  Comparable을 구현했다면 compareTo 메소드를 작성한 것이고, (한가지로 밖에 정렬할 수 없음) int compareTo(Student s)
  상황에 따라서 이름으로, 또는 나이로, 학번으로 비교하고 싶다면  Comparator를 따로 만들어서 같이 전달해서 compareTo말고 다른 거를 비교하도록 비교자에게 물어보게함
  => Arrays.sort()를 내림차순으로 바꾸려면 사용 가능
  => 객체형 배열은 비교 정렬 시 comparable || comparator 둘 중에 하나 반드시 필요
  두 개의 객체를 비교할 때 equals / hashcode가 같다고 하면 똑같은 객체임을 알 수 있음(compare) 
```



### 입출력방법
* Scanner보다 BufferReader로 하는게 길어질수록 효율이 높음
      
      데이터가 흘러다니는 통로의 유형(Stream의 유형) [입력스트림(읽기만 가능), 출력스트림]
      자바는 단방향 통로로, 우리입장에선 받아들이는 스트림 input, 내보내는 스트림 out
      JVM 구동시 System.in(입력) / System.out(출력) / System.err 이 자동으로 실행


* 데이터 입력스트림		

      input stream (System.in) 	-  byte 단위로 처리 (byte 하나 읽거나, byte[] 읽거나) 
      reader				-  char 단위로 처리(2byte)
      Scanner가 스트림을 읽어다가 처리해줌
      stream이 제공하는 내용을 파싱하고 컨버팅하는 작업을 해야하는데 Scanner를 쓰면 입력에 대한 처리를 신경안쓰고, 데이터 타입에만 포커싱해도 되는 것, 대신 내부적으로 거치는 일들이 많다보니 속도가 떨어짐
      그래서 BufferedReader 이용해서 직접 필터링해서 입출력하면 시간 세이브가 됨. 입력시간 개선은 분명히 영향이 있다는 것. 
    
---



