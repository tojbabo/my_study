# DAY 10.
---
### 인터페이스 주요 용도 2가지
1. 하위클래스의 특정 method 강제
2. class 간의 의존성 감소(loose coupling)
<pre>
- tight coupling [일반적인 경우]
TestMain ---------> DBService --------->| MySQLDAO ---------> DB(MySQL)
                                        |OracleDAO ---------> DB(Oracle)

    * 각각의 DAO가 수정되어도 Service 부분에는 변함이 없다.
    * 그러나 각각의 DAO를 따로 구현해야 한다.
  
- loose coupling [인터페이스 활용하면]
TestMain ---------> DBService ---------> DBDAO(interface) |DB(MySQL)    
                                                          |DB(Oracle)

    * 일관된 구현, 및 사용으로 코드가 간결해짐

</pre>
---
### 중첩클래스 (Inner Class)
종류
1. member inner class
   outter 클래스의 멤버 변수 처럼 정의

2. local inner class
   outter 클래스의 로컬 변수처럼 정의

3. static inner class
   
4. 익명 클래스

#### 익명클래스 (Anonymous class)
- 이름이 없는 클래스
- 인터페이스를 사용할 때 주로 활용
- lambda 식과 연결됨

<pre>
    public interface A{
        public abstract void func();
    }

    # normal calss
    public class normal implements A{
        @Override
        public void func(){}
    }

    # anonymous class
    A a = new A(){  // 클래스 이름은 없이 바로 정의 들어간다
        @Override
        public void func(){

        }
    }
</pre>

*lambda 표현식*
익명 클래스의 또 다른 표현 방법으로,
Java 에서 class 단위로 구현하는 것이 단순 method를 하나 구현하기 위해 class를 만드는 것은 매우 비효율적.
이를 해결하기 위해 lambda를 활용하는 것

추상 메서드 단 하나만 가진 경우 람다식 사용 가능
@FunctionalInterface 어노테이션을 사용

<pre>
    @FunctionalInterface
    public interface A{
        public abstract void func(); // 이거 하나만 선언 가능
        // default method 는 여러개 추가할 수 있다.
    }



    ** 람다식으로 표현해보자면
    A a = ()->{system.out.println("good")};
    A a = (n)->{n++}; // 사실 파라미터가 한개면 소괄호는 없어도 됨
    A a = (a,b)->{return b-a};



</pre>
---
#### final
*마지막을 의미*
final 변수 >> 값 변경 불가 - 상수
final method >> 재정의 불가
final class >> 상속 불가

---
### Utility Class

> #### String
> new String("hello"); :같은 문자열도 new 할때마다 다른 인스턴스가 생성됨.
> 한번 생성되면 변경이 안된다는 사실
> StringTokenizer : str.split()와 같은 역할. 근데 좀더 간편함
> new StringTokenizer(word, ":/,") 이러면 문자열에 있는 모든 단어를 사용해서 나눈다

> #### String Builder
> new StringBuilder(); 
> sb.toString()으로 최종적으로 사용할땐 String으로 사용함

> #### Date, Calender
> Date는 오래된 애 Calender는 비교적 최근 애
> new Date() // Calender.getInstance() : Calender는 싱글톤 패턴이 적용되어있다.
> > LocalDate 라이브러리를 쓰도록하자. 채신기술*

> #### Wrapper클래스
> 기본형을 클래스로 전환.
> why? class 안에 정의된 메서드 및 상수를 활용하기 위해
> 예) Short.MIN_VALUE / short.MAX_VALUE를 사용하면 해당 자료형의 최소 최대 값을 알 수 있다.
>
> int n = 10;
> Integer nn = new Integer(10);
> 
> Integer n2 = n; <= 오토 박싱
> int n3 = nn; <= 오토 언박싱 
---

### Try-catch
*예외클래스(Exception)는 당연히 다형성이 있다*
따라서 최상위 예외클래스(Exception)는 가장 하위에서 써줘야한다
안그러면 최상위 클래스에서 걸린다

예외정보 가져오기
* e.getMessage();   
* e.printStackStrace(); // 디버깅용

**상속관계의 thorws**
public void a() thorws 예외클래스{}
public void a() // 자식에서는 부모가 thorws한 예외클래스와 같거나 계층적으로 하위클래스만 지정 가능하다

*부모 클래스의 오버로딩할 함수에 예외 클래스에 대해서 하위 클래스로 지정! 있는걸 없다고 해도 되지만 없는걸 있다곤 못해!*
RuntimeExcept로 thorws된 함수를 Exception(최사위 예외클래스)로 thorws 시키지는 못한다!


##### 런타임계열 vs 비런타임 계열
* 런타임계열
  > RumtimeException
  >> ArithmeticException
  ArryIndexOutofBoundException
  NullPointerException

    *실행시 예외가 발생됨*
  * try - cache 또는 thorws 방법으로 예외처리를 안함. 
  * *조건문으로 예외 발생을 방지할 수 있음* 
  * 이 에러가 발생 시 조건 처리를 안한것으로 개발자 잘못이다


* 비런타임계열
  > IOException
  > SQLException
  * 반드시 try - catch또는thorws 방법으로 예외처리를 해야됨
   안하면 컴파일 시 예외가 발생함


---
## 제네릭스(Generics)
다양한 타입을 다루는 메서드 및 클래스에서
**컴파일 시점**에 타입체크를 해서 예외를 미리 알 수 있도록 지원

* 저장하는 데이터 타입 안정성 확보 (저장하는 데이터형을 제한 가능)
* 형변환 불필요

<pre>
    &lt;T&gt;   : Reference Type,
            &lt;String&gt; 
            &lt;int&gt; (X) | &lt;Integer&gt; (O)
    &lt;E&gt;   : Element
    &lt;T,R&gt; : Return Type 
            &lt;String, Integer&gt; String으로 들어가서 Integer로 나온다
    &lt;K,V&gt; : Key - Value type
</pre>

* &lt;T&gt;가 컴파일 시점에 지정된 타입으로 치환됨
* 클래스, 인터페이스, 메서드 파라미터에 사용 가능
* static 사용은 불가, 객체 생성도 불가

## 컬렉션 API
JAVA의 데이터 저장 - 변수 / 배열 / **컬렉션**

* 자유로운 크기 변경
* 서로 다른 자료형의 데이터 저장 (제너릭을 통해 자료형 제한 가능)
* 자체적으로 지원되는 다양한 메서드

**종류**
<pre>
        Collectino<>  -------------------- (인터페이스)
    Set<> group     | List<> group -------------- (인터페이스)
    HashSet<>       | ArrayList<>

  
가. Set 계열
    - 저장되는 데이터 순서가 없음
    - 중복저장 불가

나. List 계열
    - 저장되는 데이터 순서가 있음
    - 중복저장 가능

다. Map 계열
    - Set과 List는 데이터, Map 계열은 데이터
</pre>



---
### 가변인자 파라미터
*public void a(int ... b){}*
a(1);
a(2,3,4);

예) system.out.printf("%d %d", 1, 2);

---
## StreamAPI
* collection api는 기본적인 기능(저장 삭제 추가 제거 조회 등)들만 포함하는 method만 지원
* 추가적으로 통계 기능(합계, 평균, 최대, 최소)등의 기능이 추가된 것
* 어떤 컬렉션에 스트림(파이프)를 넣어서 중간처리(중복제거, 정렬, 필터링) 및 최종처리(합계, 평균)등의 기능이 추가되는 것

Stream 과정에서 여러 기능을 활용하기 위해 함수적 인터페이스를 활용해야 한다.
1. Consumer : 파라미터는 있고, 리턴은 없는 경우 < T > , 두개 < T, U >
2. Supplier : 파라미터는 없고, 리턴은 있는 경우 < T >
3. function : 파라미터와 리턴 모두 있는 경우 < T, R >, < T, U, R >
4. Operator : Function을 상속받는 APi