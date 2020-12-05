# 2020.12.05

## Chapter4. 람다와 함수형 인터페이스
<hr>

### # 4.1 들어가며
- 람다 표현식이 자바 혁신의 핵심.
- 람다 표현식이 공식적으로 추가됨으로써 함수형 인터페이스, 메서드 참조, 스트림 API가 탄생하여 컬렉션 기반의 기술을 편리하고 빠르게 처
> <h2>Chapter4 Goal </h2>
> 람다 표현식 : 익명 클래스를 람다 표현식으로 변경하는 과정 <br>
> 람다 표현식 주요 문법 : 람다 표현식에서 사용할 수 있는 주요 문법<br>
> 함수형 인터페이스 : 함수형 인터페이스란 무엇인지, 어떻게 사용하고 람다 표현식과 어떻게 연결되는지 알아본다. <br>
> 메서드 참조 : 메서드 참조 방법과 규칙, 그리고 사용 시 장점 <br>
<hr>

### # 4.2 람다 표현식이 필요한 이유
- 자바 프로그램이 비대해지며 프레임워크와 라이브러리가 추가되면서 유연성과 다양성을 확보하기 위해 인터페이스 기반으로 개발을 많이함.
- 프로그램의 명세(인터페이스)와 구현(클래스)을 분리하고 결과적으로 많은 클래스 파일이 생긴다.
- 이에 대응하기 위해 별도로 구현된 클래스를 만들기도 하고 간단한 코드라면 중첩 클래스나 익명 클래스 형태로 실제 내용을 구현함.
- 익명 클래스를 만들면 비즈니스로직의 구현보다 그것을 담기 위한 코드를 더 많이 작성하게 되고 중복되는 코드가 많아짐
- 반복적이고 비효율적인 구조를 개선 가능함
- 람다 표현식은 익명 클래스를 대체하는데 유용하다.
> Ex) 4.1 BaseballPlayer.java <br>
> Ex) 4.2 SortCollection.java <br>
> Ex) 4.3 JdbcTemplateExample.java <br>
> https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/core/RowMapper.html
>https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/core/JdbcTemplate.html

```java
//Lambda
list.sort(
    (BaseballPlayer object1, BaseballPlayer object2)
        -> object1.getPlayerName().compareTo(object2.getPlayerName())
)

//익명 Class
list.sort(new Comparator<BaseballPlayer> object2) {
    @Override
    public int compare(BaseballPlayer object1, BaseballPlayer object2) {
        return object1.getPlayerName().compareTo(object2.getPlayerName());
    }
}
```
> <h3>Lambda 장점</h3>
> - 이름 없는 함수를 선언할 수 있다. 메서드는 반드시 특정 클래스나 인터페이스 안에 포함되어야 하고 메서드의 이름이 있어야 하지만, 람다 표현식은 이러한 제약이 없다. <br>
> - 소스 코드의 분량을 획기적으로 줄일 수 있다. <br>
> - 코드를 파라미터로 전달할 수 있다. 외부에서 동작을 정의해서 메서드에 전달할 때 편리하게 사용할 수 있다.
<hr>

### # 4.3 람다 표현식이 필요한 이유
- 람다 표현식은 익명 클래스를 단순화하여 그 표현식을 메서드의 인수로 전달
- 인터페이스의 객체를 생성할 수 있는 기능을 제공
- 익명클래스정의 -> 람다표현식으로 변경.
> <h3>메서드를 구성하는 4가지 요소</h3>
> - 메서드의 이름
> - 메서드에 전달되는 파라미터 목록
> - 메서드를 구현한 본문
> - 메서드의 리턴 타입
> - 람다표현식은 이름과 리턴 타입을 생략하고 파라미터, 구현만 표현함
</br>

#### # 4.3.1 람다 표현식으로 전환
> 1단계 - 익명 클래스 선언 부분 제거 <br>
> 제거해야 할 부분은 인터페이스 이름이다. <br>
> 이미 Thread 생성자의 인수는 Runnable 인터페이스가 유일하며, 입력해야 할 Runnable 인터페이스 혹은 이를 구현한 클래스로 한정되기 때문에 인터페이스명을 다시 선언할 필요가 없다.
> ```java
> Thread thread = new Thread(new Runnable() {
>   @Override
>   public void run() {
>       System.out.println("Hello Thread!");       
>   }
> });
> ```
> <br>
> 2단계 - 메서드 선언 부분 제거<br>
>
> ```java
> Thread thread = new Thread(
>   @Override
>   public void run() {
>       System.out.println("Hello Thread!");       
>   }
> );
> ```

> <br>
> 3단계 - 람다 문법으로 정리<br>
> 메서드명과 리턴타입을 제거한다.<br>
> 리턴이 없으면 void / 리턴이 있으면 리턴타입이 이미정해져있음<br>
>
> ```java
> Thread thread = new Thread(
>   () {
>       System.out.println("Hello Thread!");       
>   }
> );
> ```
> <br>

> 4단계 - 최종 결과<br>
> 람다에서는 파라미터 목록을 메서드의 본문으로 전달한다는 의미로 '->'기호를 사용한다.<br>
> Runnable 인터페이스의 run 메서드의 경우 입력 파라미터가 없지만 람다 표현식에서는 이 경우에도 파라미터 목록을 남겨놔야한다.<br>
>
> ```java
> Thread thread = new Thread(
>   () -> System.out.println("Hello Thread!"));
> ```

- 파라미터 목록 : 메서드의 파라미터 목록을 정의
- 화살표 : 파라미터와 코드의 구현 부분을 구분
- 메서드 본문 : 파라미터를 받아서 처리하고 결과를 리턴하는 코드 영역이다.
- 만일 메서드를 구현한 것이 한 줄이라면 별도의 구분 없이 한 줄만 코드를 작성하면 되고, 여러 줄에 걸쳐서 작성되어 있다면 중괄호(||)를 이용해서 묶어주면 된다.

> #. 람다 특징
> - 이름이 없다.
> - 종속되지 않는다.
> - 값의 특징을 갖는다?????
> - 간단하다.
> - 새로운 것이 아니다.

#### # 4.3.3 람다 표현식과 변수
- 람다 표현식에서 사용한 변수들은 내부에서 선언한 것만을 사용하였다. 하지만 람다 표현식 밖에서 생성한 변수도 참조해서 사용가능.
- 람다 표현식에서 외부 변수를 참조하기 위해서는 반드시 final이거나 final과 유사한 조건이여야 한다.
```java
int threadNumber = 100;
//Stream.class - void forEach(Consumer<? super T> var1);
list.stream().forEach((String s) -> System.out.println(s + ", " + threadNumber));
```
<hr>

### # 4.3 람다 표현식이 필요한 이유
- 비록 인터페이스에 default, static, private 메소드가 포함되어 있더라도 오직 하나의 추상 메서드만이 존재하면 함수형 인터페이스이며 해당 추상 메서드를 함수형 메서드로 인식한다.
- @FunctionInterface 자바 제공 함수형 기본 인터페이스
- Consumer / Function / Predicate / Supplier


