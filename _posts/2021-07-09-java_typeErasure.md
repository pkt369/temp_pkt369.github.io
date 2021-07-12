---
layout : posts

title : "자바 type Erasure"

date : 2021-07-09

categories : java

comments : true
---



필자가 제네릭을 적으면서 다음편으로 type erasure을 꼭 적어야겠다고 생각을 했다.

왜냐하면 [제네릭](https://pkt369.github.io/java/java_Generic/)을 이해하기 위해서는 필수적으로 알아야하는 사항이기 때문이다.

<br>

<h3>구체화 vs 비구체화</h3>

타입 이레이저를 설명하기 전에 구체화와 비구체화에 먼저 설명할려고한다.

**구체화 타입(reifiable type)** : 자신의 타입을 런타임에도 알고 있는 타입 

ex ) int[], string[], ...

<br>

**비구체화 타입(non-reifiable type)** : 런타임에 소거(type erasure)되어 자신의 정보를 모르는 타입

- 제네릭 타입이 비구체화 타입에 해당한다.
- 제네릭은 컴파일 타임에 미리 타입 체크를 한 뒤에 런타임 시점에 타입을 지워서 사용한다.

<br>

그럼 이제 제네릭이 비구체화 타입인 것을 알았으니 소거(type erasure)에 대해 자세히 알아보자.

<br>

<br>

<h3>소거(Type Erasure)</h3>

제네릭을 구현하기위해 자바 컴파일러는 **타입 이레이저(type Erasure)**를 사용한다.

한국말로 **소거**라고 한다. 소거란 타입을 **컴파일에만 검사하고 런타임에는 해당 타입 정보를 알 수 없는 것**이다.

즉, 컴파일 타임에만 제약 조건을 적용하고, 런타임에는 타입에 대한 정보를 소거하는 것이다.

말로만 들으면 조금 어렵지 않은가?? 다음 규칙을 보면서 좀더 이해해보자.

<br>

<h3>자바 소거 규칙</h3>

자바 컴파일러는 타입소거를 위해 다음과 같이 적용하고 있다.

1. 제네릭 타입에서는 해당하는 **타입파라미터**나 **Object**로 변경해준다.

   만약 Object로 변경하는 경우는 타입이 지정되지 않는(unbounded) 된 경우를 의미하며, `<E extends Number>`와 같이 타입을 지정(bound)을 한 경우 타입(Number)으로 변경한다.

   소거 규칙은 제네릭을 적용할 수 있는 일반 클래스, 인터페이스, 메서드에만 해당한다.

2. 타입 안정성 보존을 위해 필요하다면 type casting을 넣어준다.

3. 확장된 제네릭 타입에서 다형성을 보존하기 위해 bridge method를 생성한다.

<br>

<br>

<h5>제네릭 타입에서 해당하는 타입파라미터나 Object로 변경해준다.</h5>

```java
public <E> int contains(E[] arr, E e) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i].equals(e)) {
            return i;
        }
    }
    return -1;
}
```

<br>

컴파일 이후 코드는 이렇게 변경이 된다.

```java
public int contains(Object[] arr, Object e) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i].equals(e)) {
            return i;
        }
    }
    return -1;
}
```

제네릭 타입이 모두 사라지고 Object로 변경되었다. 즉 타입이 소거가 된것이다.

컴파일 단계에서 미리 확인했기 때문에 런타임에서 에러가 나지 않는 것이다.

<br>

두번째로 범위가 제한적일 경우는 특정 타입을 변환된다.

```java
public int contains(Number[] arr, Number e) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i].equals(e)) {
            return i;
        }
    }
    return -1;
}
```

이런 경우는 제한적인 타입으로 변환하여 사용하게 된다.

<br>

<h5>타입 안정성 보존을 위해 필요하다면 type casting을 넣어준다.</h5>

```java
public <E> int contains(E[] arr, E e) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i].equals(e)) {
            return i;
        }
    }
    return -1;
}
```

위코드에서 우리가 E에 Integer를 넣었다면 타입 안정성 보존을 위해 (Integer) e로 변경할 수 있다. 

<br>

<h5>확장된 제네릭 타입에서 다형성을 보존하기 위해 bridge method를 생성한다.</h5>

먼저 설명을 듣기전에 추천 드리는 사이트가 있다. 물론 자바 공식 홈페이지라서 영어로 되어 있다.

oracle : [bridgeMethod](https://docs.oracle.com/javase/tutorial/java/generics/bridgeMethods.html)

여기에 나와있는 예제로 설명을 드리자면 

```java
public class Node<T> {
    public T data;
    public Node(T data) { this.data = data; }

    public void setData(T data) {
        this.data = data;
    }
}

public class MyNode extends Node<Integer> {
    public MyNode(Integer data) { super(data); }

    public void setData(Integer data) {
        super.setData(data);
    }
}


public static void main(String[] args) {
    MyNode mn = new MyNode(5);
	Node n = mn;            // Raw type - unchecked warning
	n.setData("Hello");     // ClassCastException(ERROR)
	Integer x = mn.data;    
}
```

이 코드에서 type erasure가 일어나면

<br>

```java
public static void main(String[] args) {
    MyNode mn = new MyNode(5);
	Node n = (MyNode)mn; // A raw type - compiler throws an unchecked warning
	n.setData("Hello");  // Causes a ClassCastException to be thrown.
	Integer x = (String)mn.data;    
}
```

이렇게 된다. 왜 setData("Hello")에서 에러가 날까?

<br>

사실 우리는 `setData(Object data)`라서 모든 것을 받을 수 있을줄 알았는데 컴파일 에러가 뜬다.

내부적으로 어떤 일이 일어난걸까?

<br>

Node의 setData는 `setData(Object data)`이다.

 그럼 String 객체도 Object 의 자손이므로 되야 하나 우리는 다형성을 유지하면서 Integer만 받길 원한다.

<br>

그렇기 때문에 자바 컴파일러는 다음과 같이 코드를 추가한다.

```java
class MyNode extends Node {
    public void setData(Object data) {
        setData((Integer) data);
    }

    public void setData(Integer data) {
        super.setData(data);
    }

}
```

이렇게 코드를 추가한 것을 **브릿지 메소드(Bridge Method)**라고 한다.

이렇게 추가되기때문에 String은 Integer로 캐스팅이 될수 없기 때문에 ClassCastException 가 터지는 것이다.





<h3>제네릭은 배열대신 리스트</h3>

추가적으로 제네릭에서는 배열 대신 리스트를 사용해야한다.

앞서 말했던 배열은 구체화 타입이라고 말했던 것을 기억 하는가? 

이부분은 코드로 설명하겠다.

```java
public <T> List<T> getList(T list) {
    return Arrays.asList(list);
}

public <T> T[] getArr(T... list) {
    return list;
}

public static void main(String[] args) {
    List<String> list = getList("리스트");
    String[] arr = getArr("배열"); //ERROR
}
```

여기서 List는 아무 이상없는 것에 반해 배열은 문제가 터지는 것을 볼수 있다.

그 이유는 제네릭은 소거를 하기 때문이다. 

만약 소거를 했을 경우 getArr은 이렇게 된다.

```java
public Object[] getArr(Object... list) {
    return list;
}
```

리턴 타입이 보이는가? 우리가 원했던 타입은 String이지만 실제로는 Object를 받는다.

즉, 컴파일 타임에 추론하는 List(list도 제네릭)를 통해 타입을 같이 확인할 수 있는 것이다.
