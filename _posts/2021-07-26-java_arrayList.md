---
layout : posts

title : "자료구조 ArrayList"

date : 2021-07-26

categories : java

comments : true
---



오늘은 List 중 하나인 ArrayList 를 알아보자.

저번 [LinkedList](https://pkt369.github.io/java/java_linkedList/) 와 비교해서 보여줄 예정이라 LinkedList를 잘모른다면 이전 포스팅을 보고 오길 바란다.

<br>

List란 값을 여러개 담을 수 있는 배열을 의미한다. 그리고 값을 담는 공간을 노드라고 표현한다.

ArrayList는 쉽게 말해서 배열과 같다. 다른점이라면 배열 같은 경우 사용할 배열의 길이를 미리 정해야한다면 ArrayList 같은 경우 크기가 가변적으로 변한다.

내부적으로는 ArrayList에 임시로 용량을 정해놓고 그 용량을 넘어서면 새롭게 더 큰 메모리를 할당한다.

<br>

#### 생성

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        List<Integer> list1 = new ArrayList<>();
        List<Integer> list2 = new ArrayList<Integer>();
        ArrayList<Integer> list3 = new ArrayList<>(10); //초기 사이즈 설정
        List<Integer> list4 = new ArrayList<>(new int[] {1, 2, 3});
        List<Integer> list5 = new ArrayList<>(Arrays.asList(1, 2, 3));
    }
}
```

생성할 땐 util 안에 있는 ArrayList를 import를 해야 사용할 수 있고, 생성자를 통해 ArrayList를 만들어 줄 수 있다.

제네릭이라서 타입 생략이 가능하고, 초기 사이즈나 값을 넣어줄 수도 있다.

<br>

#### 추가

add() 메서드로 추가가 가능하다.

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);
list.add(0, 0); //0번째 0을 넣겠다.

System.out.println(list); //0, 1, 2, 3
```

`list.add(0, 0);`을 하게 되면 0번째에 넣게 되면서 원래 있던 것들은 한칸씩 밀리게 된다.

<br>

#### 변경

set() 메서드로 변경이 가능하다.

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);
list.set(0, 0);

System.out.println(list); //0, 2, 3
```

원하는 인덱스의 값을 원하는 값으로 변경해 줄 수 있다.

<br>

#### 삭제

remove() 메서드로 삭제가 가능하다.

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);
list.remove(0);
list.remove(Integer.valueOf(2));

System.out.println(list); //3

list.clear();

System.out.println(list); //null
```

remove는 두가지의 기능이 있다. 하나는 인덱스의 값으로 삭제하는 것이고, 하나는 값을 바로 삭제하는 것이다.

인덱스의 경우에는 `remove(int)`이며, 값을 삭제하는 경우에는 `remove(Object)`이다.

만약 Integer로 되어 있을 경우 `remove(Integer.valueOf(2))`로 Integer 형으로 변환 시켜준 후 삭제 시켜줄 수 있다.

<br>

#### 값 확인

contains() 와 indexOf()로 확인할 수 있다.

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

boolean con = list.contains(1); // true
int idx = list.indexOf(4); // -1
```

contains 는 반환형이 boolean으로 존재여부를 반환해주고 있다.

indexOf 는 값이 있으면 index로 없으면 -1을 반환해주고 있다.

<br>

### ArrayList 와 LinkedList의 차이

|                 | ArrayList                                                    | LinkedList                                                  |
| --------------- | ------------------------------------------------------------ | ----------------------------------------------------------- |
| 검색            | O(1)의 성능으로 매우 빠름                                    | 최악의 경우 O(n)으로 ArrayList 보다 느림                    |
| 삭제, 중간 삽입 | 삭제 한 후 그다음 인덱스들을 한칸씩 땡겨와야 함으로 LinkedList보다 느림. | 이전과 다음의 주소값만 변경해주면 되기 때문에 삭제에 용이함 |

<br>

<br>

#### Reference

https://psychoria.tistory.com/765
