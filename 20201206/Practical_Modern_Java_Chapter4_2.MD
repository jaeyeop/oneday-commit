# 2020.12.05

## Chapter4. 람다와 함수형 인터페이스
<hr>

## # 4.6 메서드 참조
- 람다 표현식을 사용하는 방법 OK
- 함수를 메서드에 파라미터로 전달하는 것을 메서드 참조(method reference)라고 부른다.
- 메서드 참조의 장점은 람다 표현식과는 달리 여러 곳에서 재사용 가능하고 자바의 기본 제공 메스드뿐만 아니라 직접 개발한 메서드도 사용할 수 있다.
> <h3>메서드의 참조 종류</h3>
> - 메서드의 파라미터로 전달하는 메서드 참조
> - 생성자의 파라미터로 전달하는 생성자 참조
<hr>

### # 4.6.1 메서드 참조란
- 람다표현식은 (String name) -> System.out.println(name)
- 메서드참조는 System.out::println
```java
List<String> list = new ArrayList<>();
for(String entity : list) {
    System.out.println(entity);
}
```
- 람다 표현식 변경
```java
list.stream().forEach((String entity) -> System.out.println(entity));
```
- 메서드 참조 변경
- 난 너무 축약인거 같은데........(갠적 생각임)
```java
list.stream().forEach(System.out::println);
```
- Ex 4.13) MethodReferenceExample.java
- executeMethod안에 여러 가지 복잡한 기능을 추가하고, 이를 스트림의 forEach 메서드에 참조로 전달하여 코드의 재사용성과 가독성을 높임.
- 메서드를 참조하는 모든 구문들을 한번에 변경시킬 수 있다.
- 클래스명::메서드명 / 객체 변수명::메서드명
- Class::Method / System.out::println
```java
public class MethodReferenceExample {
    public static MethodReferenceExample of() {
        return new MethodReferenceExample();
    }

    // Data 처리 Logic.
    public static void executeMethod(String entity) {
        if(entity != null && !"".equals(entity)) {
            System.out.println("Contents : " + entity);
            System.out.println("Length : " + entity.length());
        }
    }

    // 대문자로 변경하는 코드
    public void toUpperCase(String entity) {
        System.out.println(entity.toUpperCase());
    }

    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("a");
        list.add("b");
        list.add("c");

        // 정적 메서드 참조
        list.stream().forEach(MethodReferenceExample::executeMethod);

        // 한정적 메서드 참조
        list.stream().forEach(MethodReferenceExample.of()::toUpperCase);

        // 비한정적 메서드 참조
        list.stream().map(String::toUpperCase).forEach(System.out::println);
        /*
        list.stream().map(new Function<String, String>() {
            @Override
            public String apply(String s) {
                return s.toUpperCase();
            }
        });
        */

        list.stream().forEach(System.out::println);
    }
}
```
> <h3>#. 정적메서드 참조</h3>
> - static 메서드는 호출할 때 객체를 생성하지 않기 때문에 정적 메서드 참조일 때도 코드가 명확해 보임. <br>
> - Integer에 정의되어 있는 static 메서드인 parseInt를 참조 <br>
> - Integer::parseInt <br>
> - (String s) -> Integer.parseInt(s) <br>
<br>

> <h3>#. 비한정적 메서드 참조</h3>
> - static 메서드를 참조하는 것과 유사하게 작성한다. <br>
> - 비한정적이라는 표현은 작성하는 구문 자체가 특정한 객체를 참조하기 위한 변수를 지정하지 않는다는 의미이다. <br>
> - 용어가 더럽게 마음에 들지 않는다. <br>
> - String::toUpperCase <br>
> - (String s) -> s.toUpperCaes() <br>
> - s::toUpperCase는 안되니깐.. 이렇게 쓴다고한다. 별루임, <br>
> - 람다 표현식 내부에서 생성한 객체의 메서드를 참조할 때 사용. <br>
<br>

> <h3>#. 한정적 메서드 참조</h3>
> - Calendar.getInstance()::getTime <br>
> - 자바8 이후 객체를 인스턴스화하는 대신 of와 같은 메서드를 이용해서 생성하는 경향이 많다. <br>
> - Calendar cal = Calendar.getInstance(); () -> cal.getTime(); <br>
> - Calendar cal = Calendar.getInstance(); cal::getTime <br>
> - 외부에서 생성한 변수를 람다 표현식에서 활용한다. <br>
> - 메서드 참조 수식에서 of 메서드나 getInstance 등의 메서드로 생성할 필요 없이 이미 생성되어 있는 객체를 참조한다. <br>
> - 외부에서 정의한 객체의 메서드를 참조. <br>
<br>

> <h3>#. 저자님 의견 추천</h3>
> - 한 라인으로 작성 가능한 람다 표현식은 그냥 람다 표현식으로. 여러 라인으로 작성해야 한다면 메서드로 분리한 후 메서드 참조 <br>
> - 비록 한 라인으로 작성할 수 있어도 다른 곳에서 재활용할 가능성이 높으면 메서드 참조를 이용 <br>
> - 너무나 익숙하고 자주 사용하는 메서드(Integer.parseInt(s)) 이러한 경우에는 람다 표현식보다는 메서드 참조 사용.

### # 4.6.2 생성자 참조란
- 자바 언어에서는 생성자와 메서드는 엄격히 구분되어 있다.
- 클래스명::new
- 생성자 참조는 메서드 참조와 달리 메서드명을 기술하지 않고 new 키워드를 지정
- 새로운 객체를 생성해서 리턴해야 하는 경우에 많이 씀.
- 이러한 경우에 생성자 참조를 유용하게 사용할 수 있다.
- 많은 클래스들이 여러 개의 생성자를 내부에 정의해 놓았는데 생성자 참조는 단순히 new 키워드만을 사용하기 때문에 명확하게 어떤 생성자를 호출하는지 혼동스러울 수 있다. 잘 사용해야 한다.
```java
// 람다 표현식
list.stream().map((String name) -> new ConstructorReferenceExample(name))
    .forEach((ConstructorReferenceExample data) -> System.out.println(data));
// 생성자 참조로 변환
list.stream().map(ConstructorReferenceExample::new)
    .forEach((ConstructorReferenceExample data) -> System.out.println(data));
// 생성자 참조, 메서드 참조로 변환
list.stream().map(ConstructorReferenceExample::new)
    .forEach(System.out::println);
```
<hr>

## # 4.7 람다 표현식 조합
### # 4.7.1 Consumer 조합
```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T var1);

    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (t) -> {
            this.accept(t);
            after.accept(t);
        };
    }
}
```

### # 4.7.2 Predicate 조합
```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T var1);

    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> {
            return this.test(t) && other.test(t);
        };
    }

    default Predicate<T> negate() {
        return (t) -> {
            return !this.test(t);
        };
    }

    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> {
            return this.test(t) || other.test(t);
        };
    }

    static <T> Predicate<T> isEqual(Object targetRef) {
        return null == targetRef ? Objects::isNull : (object) -> {
            return targetRef.equals(object);
        };
    }

    static <T> Predicate<T> not(Predicate<? super T> target) {
        Objects.requireNonNull(target);
        return target.negate();
    }
}
```

### # 4.7.3 Function 조합
```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T var1);

    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (v) -> {
            return this.apply(before.apply(v));
        };
    }

    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (t) -> {
            return after.apply(this.apply(t));
        };
    }

    static <T> Function<T, T> identity() {
        return (t) -> {
            return t;
        };
    }
}
```