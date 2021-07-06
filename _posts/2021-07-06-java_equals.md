---
layout : posts

title : "equals 와 == 차이"

date : 2021-07-06

categories : java

comments : true
---





보통 자바에서 비교할때 ==을 가지고 많이 비교를 한다.

필자도 잘모를땐 전부다 ==으로 비교하면 되는거 아니야? 라고 생각을 했었던 적이 있다.

그럼 본격적으로 == 과 equals를 비교해보자

<br>

<br>

<h3>==</h3>

자바에서 비교할때 == 는 어떨때 사용될까?

당연히 많은 독자께서 ==는 당연히 값을 비교할때 사용하지! 라고 대답을 할것이다.

맞다. 정답이다. 단 데이터타입이 기본형일때만이다.

<br>

데이터 타입에는 두가지 종류가 있다.

1. 기본형(Primitive Type)
2. 참조형(Reference Type)

<br>

기본형은 다들 생각하듯이 byte, short, int, long, float, double, char, boolean 이 있다.

<br>

참조형은 자바의 가장 기본적인 class인 **java.lang.Object**를 상속받으면 참조형이 된다.

쉽게 말해서 기본형이 아닌 경우는 참조형이 됩니다.

참조형의 경우는 class, interface, array 이 있습니다.

<br>

위에서 말했듯이 데이터타입이 기본형인 경우에만 == 으로 값이 비교가 가능하다.

그럼 누군가는 이렇게 말할것이다.

string 타입인 "name" == "name" 은 보기에 같아보이는대요?

```java
public class compare {
    public static void main(String[] args) {
        String name1 = "name";
        String name2 = "name";
        System.out.println(name1 == name2); //false
    }
}
```

그렇다 보기엔 같아보인다. 하지만 "name" == "name"을 실행시켜보면 false가 나온다.

도대체 왜그럴까?

<br>

참조형으로 생성된 객체는 Heap 영역에 생성이 된다. 

각 객체는 주소값을 가지게 되고 == 비교는 주소값을 가지고 비교를 하게 된다.

```java
public class Compare {
    public static void main(String[] args) {
        String name1 = "name"; //Compare@1b3s~
        String name2 = "name"; //Compare@1a2o~
        //Compare@1b3s == Compare@1a2o
        System.out.println(name1 == name2); //false
    }
}
```

여기서보면 이제 주소값이 다르니까 ==이 왜 틀린것을 알수 있다.

그러면 이제 ==은 주소값을 비교한다는 것을 알았다.

그럼 어떻게 참조형끼리 비교를 할수 있을까?

<br>

<br>

<h3>equals</h3>

참조형의 값을 가지고 비교할수 있는 것이 equals 메소드이다.

사용법은 .equals를 이용해 비교할수 있다.

```java
public class Compare {
    public static void main(String[] args) {
        String name1 = "name";
        String name2 = "name";
        System.out.println(name1 == name2); //false
        System.out.println(name1.equals(name2)); //true
    }
}
```

값을 찍어보면 true가 나오는 것을 알수있다.

<br>

앞에서 참조형을 가지고 서로 비교하는것이 equals라고 말했었다.

그럼 이 객체는 어떻게 비교할까?

```java
public class human {
    String name;
    int age;
    
    public human(name, age) {
        this.name = name;
        this.age = age;
    }
}
```

<br>

이것 또한 equals를 이용해 비교할수 있다.

 단, 먼저 equals를 먼저 오버라이드 한 후에 말이다.

```java
public class Human {
    String name;
    int age;
    
    public Human(name, age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public boolean equals(Human h) {
        if (h.name != this.name) {
            return 0;
        }
        if (h.age != this.age) {
            return 0;
        }
        return 1;
    }
}

public class Main {
    public static void main(String[] args) {
		Human human1 = new Human("name", 10);
        Human human2 = new Human("name", 10);
        Human human3 = new Human("name2", 10);
        Human human4 = new Human("name", 20);
        
        //1.
        System.out.println(human1.equals(human2));
        //2.
        System.out.println(human1.equals(human3));
        //3.
        System.out.println(human1.equals(human4));
    }
}
```

과연 여기서 어떤것들이  true 일까?

정답은 1번만 true 이다.

우리가 앞서서 equals 메서드를 오버라이딩하여 구현한 것을 보면 이름과 age 둘다 비교하여 사용하고 있기 때문이다.

<br>

<br>

<h3>마무리</h3>

자바를 처음배울때 주소라는 개념을 이해하기가 정말 어려웠던 기억이 있다.

그렇기때문에 equals도 그렇구나 하고 개념은 잘몰랐었다.

그렇기 때문에 좀더 열심히 서술(?)했다.

<br>

주소라는 개념을 이해하기 위해서는 힙영역, 스택영역에 대해 알아야 한다고생각한다.

다음 블로그 포스팅으로 힙 & 스택에 대해 서술해볼까 생각한다.























