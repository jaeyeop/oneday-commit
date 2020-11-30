# 2020.11.30

## Chapter2. Interface & Class

### # 2.1 Intro.
- 인터페이스의 문제점
- 인터페이스의 진화
- default Method
- 다중 상속

### # 2.2 인터페이스 사용 시 문제점  
- 인터페이스는 여러 개의 구현체를 통일화된 명세서로 정의하기 위해 사용.
- 구현 방법에 상관 없이 자신이 원하는 메서드를 호출함으로써 목적을 이룰 수 있음. / 다형성, 캡슐화 등

> Collection - List / Collections.
> - Collection Interafce에 Method를 추가하게 되면 영향도가 엄청나다.
> - Collection Framework를 처리할 Utility Class를 제공하기로 하였고 그것이 Collections(List_sort 등 구현)
> - Static Class 구현


### # 2.3 인터페이스의 진화
> Interface ver 1.1
> - 상수 선언 / final
> - 메서드는 구현체가 아니라 명세만 정의
> - 인터페이스를 구현한 클래스는 인터페이스에서 정의한 메서드를 구현하지 않았다면 반드시 추상 클래스로 선언
> - 인터페이스 상수, 메서드는 public

> Interface ver 1.2
> - 중첩(Nested) 클래스 선언, 선언은 Inner 클래스 같아 보이지만 실제로는 중첩 클래스로 인식함.
> - 중첩 클래스, 인터페이스는 모두 public + static
> ```java
> //중첩클래스.
> public Interface Outer {
>   public static Class NestedStaticClass {
>       //public + static.
>   } 
> }
> //중첩인터페이스.
> public Class Outer {
>   public Interface NestedInterface {
>       //public + static.
>   }
> }
> ```

> Interface ver 1.5
> - 솔직히 모르겠다......... 질문!
> - 제네릭, 열거형, 어노테이션이 인터페이스에 영향을 주었다.
> - 인터페이스에 선언할 수 있는 것이 4 -> 6개로 증가함.
> - Nested Enum 선언
> - Nested Anotation 선언
> - public + static

> Interface ver 1.8
> - static 메서드를 선언할 수 있다.
> - default 메서드를 선언할 수 있다.
> - 구현이 완성된 method.
> - 이렇게 정의한 메서드는 인터페이스를 구현할 때 클래스에서 정의할 필요가 없다.

```java
public interface List<E> extends Collection<E> {

    //중략........
    default void replaceAll(UnaryOperator<E> operator) {
        Objects.requireNonNull(operator);
        ListIterator li = this.listIterator();

        while(li.hasNext()) {
            li.set(operator.apply(li.next()));
        }

    }

    default void sort(Comparator<? super E> c) {
        Object[] a = this.toArray();
        Arrays.sort(a, c);
        ListIterator<E> i = this.listIterator();
        Object[] var4 = a;
        int var5 = a.length;

        for(int var6 = 0; var6 < var5; ++var6) {
            Object e = var4[var6];
            i.next();
            i.set(e);
        }
    }
}
```

> Interface ver 1.9
> - 질문!!!!
> - private 메서드를 선언할 수 있다.

> 인터페이스 선언
> - 상수, 추상 메서드, 중첩클래스, 중첩인터페이스, 중첩 열거형, 중첩 어노테이션, static 메서드, private 메서드.

