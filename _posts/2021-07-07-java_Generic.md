---
layout : posts

title : "제네릭(Generic)"

date : 2021-07-07

categories : java

comments : true
---



제네릭은 자바하면 들어봤을 용어이다. 

필자도 제네릭을 자세히 알지 못했고 이번에 공부하면서 좀더 자세히 알게되었다.

알게된 내용을 공유해드릴려고 한다.

<br>

<br>

<H3>제네릭(Generic)</H3>

제네릭(Generic)은 하나의 데이터 타입이 아니라 여러 데이터 타입들을 가질 수 있다는 뜻이다.

```java
List<Integer> list1 = new ArrayList<>();
List<String> list2 = new ArrayList<>();
```

이렇게 제네릭은 **클래스 내부에서 지정하는 것이 아닌 외부에서 지정하는 것을 의미**한다.

<br>

그럼 제네릭은 왜 쓰는 걸까?

1. 코드의 재사용
2. 컴파일 단계에서 오류
3. 외부에서 타입을 지정하기 때문에 내부에서 타입을 관리할 필요가 없다.

<br>

<h5>코드의 재사용</h5>

만약 우리가 ArrayList를 구현한다고 가정해보자

```java
public class ArrayListInteger {
    int[] arr;
    public ArrayListInteger(int[] arr) {
        this.arr = arr;
    }
    
    public add(int n) {...}
}
```

int 형으로 배열을 하나 구현했다.

근데 만들다보니 String이 들어있는 배열도 필요할것같다.

<br>

```java
public class ArrayListString {
    String[] arr;
    public ArrayListString (String[] arr) {
        this.arr = arr;
    }
    
    public add(String s) {...}
}
```

위 코드와 아래 코드를 보면 코드가 똑같다고 느껴지진 않는가?

개발자라고하면은 중복되는 코드를 없애는게 당연하다.

<br>

```java
public class ArrayListGeneric<T> {
    T[] arr;
    public ArrayListString (T[] arr) {
        this.arr = arr;
    }
    
    public add(T s) {...}
}

ArrayListGeneric<Integer> list1 = new ArrayListGeneric<Integer>();
ArrayListGeneric<String> list1 = new ArrayListGeneric<String>();
```

이렇게 사용할수 있을것이다.

<br>

여기서 짚고 넘어가야 할것이 있다.

처음만든건 기본형(Primitive)인 int로 만들었는데 위에 코드에서는 래퍼(Wrapper)인 Integer를 썼다.

제네릭은 타입 파라미터로 지정할 수 있는 것은 **참조타입(Reference)**이기 때문이다.

또한 우리가 만든 클래스 또한 올수 있다는 뜻이기도 하다.

<br>

<br>

<h5>컴파일 단계에서 오류</h5>

제네릭을 쓰기 않고 어떻게 사용 할수 있을까?

```java
public class CarCenter {
    private Object car;
    
    public void setCar(Object car) {
        this.car = car;
    }
    
    pulbic Object getCar() {
        return car;
    }
}
public class Tesla{}
public class Avante {}


public static void main(String[] args) {
    CarCenter center = new CarCenter();
    center.set(new Tesla());
    
    Tesla tesla = (Tesla) center.getCar();
    Avante avante = (Avante) center.getCar(); //java.lang.ClassCastException
}
```

여기서 타입이 변경이 될까?

실행을 시키면 실행까진 된다. 문제는 실행하고 나서 에러가 걸리는 것이다.

즉, 런타임 에러가 되는 것이다.

우리가 배우길 가장 좋은 에러는 런타임 에러가 아니라 컴파일 에러라고 배웠다.

<br>

그럼 제네릭은 언제 에러가 걸리게 될까?

```java
public class CarCenter<T> {
    private T car;
    
    public void setCar(T car) {
        this.car = car;
    }
    
    pulbic T getCar() {
        return car;
    }
}
public class Tesla{}
public class Avante {}


public static void main(String[] args) {
    CarCenter<Tesla> center = new CarCenter<Tesla>();
    center.set(new Tesla());
    
    Tesla tesla = center.getCar();
    Avante avante = center.getCar(); //error
}
```

코드와 같이 바로 컴파일 시점에서 오류를 잡아준다.

왜냐하면 미리 앞선 시점에서 선언을 해주었기 때문이다.

<br>

<br>

<h5>외부에서 타입을 지정하기 때문에 내부에서 타입을 관리할 필요가 없다.</h5>

이 이야기는 우리가 위에서 타입캐스팅을 해보면서 사실 미리 겪어 보았다.

```java
Tesla tesla = center.getCar();
Tesla tesla = (Tesla) center.getCar();
```

(Tesla)가 보이는가? 저걸 타입캐스팅이라고 한다.

우리는 앞선 시점에서 미리 선언을 해줌으로써 타입캐스팅을 할 필요도 없어지는 것이다.

즉, 관리하기가 편해진다는 것이다.

<br>

<br>

<h3>제네릭(Generic)이 사용 불가능한 경우</h3>

제네릭은 **static**일 경우 사용할 수 없다.

우리가 기존에 객체를 생성할 때 new 를 쓰던 것이 기억이 나는가?

```java
new Tesla();
new Avante();
new CarCenter<Tesla>();
```

이렇게 우리는 new 를 통해 객체를 생성하는데 new는 heap 영역에서 타입에 맞는 크기만큼 생성해준다.

제네릭도 타입을 적어 놓음으로써 크기를 알수가 있다.

 <br>

그럼 우리가 제네릭으로 선언한 클래스에 만약 static(정적)으로 되어 있으면 어떻게 될 것 같은가?

static 을 붙이면 먼저 메모리에 올려 놓는데 어떤 타입인지 알수가 없기 때문에 크기를 알 수가 없다.

그렇기 때문에 제네릭은 static을 사용할 수 없다.

<br>

<br>

<h3>제네릭 메소드</h3>

사실 제네릭은 클래스만 있는 것이 아니다. 제네릭은 메소드 또한 존재한다.

우리가 위에서 배웠던 개념과 비슷하지만 클래스와 다르다.

어떤 점이 다를까?

1. 선언하는 위치
2. static 사용 가능 여부
3. 클래스가 가진 타입과 메소드가 가진 타입

<br>

<h5>선언하는 위치</h5>

클래스같은 경우는 클래스 이름 옆에 <E>를 붙여 사용을 했다.

하지만 메소드 같은 경우는 반환 타입 전에 선언을 하여 사용 한다.

```java
public <E> e genericMethod(E a) {
    //...
}
```

<br>

<br>

<h5>static 사용 가능 여부</h5>

클래스 같은 경우 static이 사용 불가능했다.

하지만 메소드 같은 경우는 사용이 가능하다.

그 이유는 별도로 타입을 지정하여 사용하기 때문이다.

```java
class CarCenter<E> {
    private E car;
    void setCar(E car) {
        this.car = car;
    }
    E getCar() {
        return car;
    }
    static <E> E genericMethod(E a) {
        return a;
    }
}

public class Main {
    public static void main(String[] args) {
        CarCenter.<Avante>genericMethod(new Avante());
        //CarCenter.genericMethod(new Avante());
    }
}
```

여기서 우리가 눈여겨 봐야할 것은 CarCenter를 선언하지 않고 static 메소드를 사용했다는 점이다.

우리가 Avante 를 넣어줌으로써 타입이 정해졌기 때문에 사용이 가능하다.

<br>

두번째로 봐야할 것은 class 와 같은 E(타입) 를 사용 한다는 것이다.

클래스와 메소드의 E는 같은 타입이 아니다.

 CarCenter에서 Tesla를 넣고 메소드에서는 Avante를 넣을수 있다는 얘기이다.

즉, 메소드는 클래스와 독립적인 존재이다.

<br>

세번째로 <Avante>는 생략이 가능하다. 그 이유는 인자의 타입이 Avante인 것을 보고 추론을 할 수 있기 때문이다.

<br>

<br>

<h3>와일드 카드와 제한된 제네릭</h3>

우리가 앞서서 적었던 E에는 어떤 것이든 다 들어갈 수가 있다.

하지만 보통은 우리가 원하는 타입만 넣기를 원할 것이다.

이때 사용하는 것이 **extends**, **super** 그리고 **?(와일드 카드)**이다.

```java
<E extends T> //T와 T의 자손 타입만 가능(E의 타입으로 지정됨)
<E super T>   //T와 T의 부모 타입만 가능(E의 타입으로 지정됨)
    
<? extends T> //T와 T의 자손 타입만 가능
<? super T>   //T와 T의 부모 타입만 가능
<?>           //모든 타입 가능 <? extends Object>랑 같은 의미
```

**extends T : 상한 경계**

**super T : 하한 경계**

**<?> : 와일드 카드**

<br>

좀더 이해하기 쉽게 코드로 설명해보겠다.

```java
public class Num<K extends Number> {
    ...
}

public class Main {
    public static void main(String[] args) {
        Num<Integer> n = new Num<>();
        Num<String> s = new Num<>(); //ERROR
    }
}
```

Number를 상속받는 타입만 쓸수 있다. 따라서 String은 Number 가 아니므로 에러를 낸다.

<br>

```java
public class Num(K super Integer) {
    ...
}

public class Main {
    public static void main(String[] args) {
        Num<Integer> n = new Num<>();
        Num<Number> n = new Num<>();
        Num<String> s = new Num<>(); //ERROR
    }
}
```

Integer 이랑 같거나 높은 타입만 가능하다. Number는 상속해주는 부모 타입이므로 성공적으로 넘어가나 String 타입은 다르므로 에러를 낸다.

<br>

여기서 제네릭과 ?(와일드카드) 차이점은 무엇일까?

```java
public static <E extends Number> void TypeCheck(List<E> list1, List<E> list2) {
    ...
}

public static void main (String[] args) {
    List<Integer> list1 = new ArrayList<>();
    List<Double> list2 = new ArrayList<>();
    TypeCheck(list1, list2); //ERRIR
}
```

여기서 봤을 때 typecheck 메소드에서 에러가 난다.

이유는 같은 제네릭 타입을 받아야하는데 하나는 Integer, 하나는 Double을 받았기 때문이다.

<br>

그럼 와일드 카드를 사용하면 어떻게 될까?

```java
public static void TypeCheck(List<? extends Number> list1, List<? extends Number> list2) {
    ...
}

public static void main (String[] args) {
    List<Integer> list1 = new ArrayList<>();
    List<Double> list2 = new ArrayList<>();
    TypeCheck(list1, list2); //success
}
```

여기서보면 정상적으로 작동하는 것을 알수 있다.

그리고 자세히보면 메소드 옆에 있던 제네릭타입이 파라미터로 옮겨간 것을 알수 있다.

<br>

이처럼 제네릭은 다중 제한(Multiple Bounds)이고 와일드 카드는 아니다.

그럼 어떨때 사용하면 좋을까?

위의 예제와 같이 특정 메서드 인자와 반환값을 모두 사용할때 제네릭을 사용하면 좋고, 와일드 카드는 제한적인 상황보다 어떤 타입이든 상관없을때 좀 더 폭넓게 사용할때 좋다.









