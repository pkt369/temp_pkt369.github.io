---
layout : posts

title : "자료구조 LinkedList"

date : 2021-07-25

categories : java

comments : true
---



프로그래머라면 꼭 알아야하는 자료구조 시리즈를 연재할 생각이다.

오늘은 List 중 하나인 LinkedList를 알아보자.

<br>

List란 값을 여러개 담을 수 있는 배열을 의미한다. 그리고 값을 담는 공간을 노드라고 표현한다.

LinkedList 같은 경우 노드에는 값과 양옆으로 어떤 데이터를 가지고 있는지 주소값을 가리키고 있다.

![linkedlist](https://user-images.githubusercontent.com/66049273/126770992-1064bef9-5990-4621-b703-cacde2fb70ea.png)

참고 : https://psychoria.tistory.com/767

<br>

좀 더 쉽게 내부적으로 어떻게 표현되고 있는지 코드로 알아보자

밑의 코드는 이해하기 쉽게 필자가 쉽게 작성한 코드이다.

```java
class LinkedNode {
	LinkedNode next;
    LinkedNode prev;
    int val;
    public LinkedNode(LinkedNode prev, val) {
        this.prev = prev;
        prev.next = this;
        this.val = val;
    }
    
    public LinkedNode(val) {
        this.val = val;
    }
}
```

각 노드는 이전과 다음을 저장할수 있는 변수가 있고 값을 가질 수 있는 변수로 이루어져 있다.

생성자를 통해서 값만 초기화 시켜주거나 이전과 값을 함께 초기화 시켜줄 수 있다.

<br>

### 장점

LinkedList 의 장점은 ArrayList의 반대인 삭제와 삽입이 자유롭다는 것이다.

다음 포스팅에서 설명할 것이지만 ArrayList 같은 경우는 중간에 삭제나 삽입을 하게되면 다음 원소들을 다음 또는 이전으로 이동시켜줘야하기 때문에 많은 cost가 든다.

LinkedList 같은 경우는 next와 prev 값만 변경해주면 되기 때문에 **삽입, 삭제에 대한 비용이 적다**이다.

<br>

### 단점

단점 또한 ArrayList의 반대이다.

ArrayList 같은 경우 검색이 매우 빠르다는 장점이 있지만, LinkedList 같은 경우 **검색이 느리다**. 최악의 경우 O(n)의 성능을 가지게 된다. 즉, 하나씩 검색하게 된다는 뜻이다.

<br>

### LinkedList 사용법

LinkedList 같은 경우 먼저 `import java.util.LinkedList`를 먼저 해줘야 사용이 가능하다.

```java
List<String> list1 = new LinkedList<>();          
LinkdedList<String> list2 = new LinkedList<>();
LinkdedList<String> list2 = new LinkedList<>(arr);
```

어느 객체들과 같이 new LinkedList를 같이해야 생성이 되며 제네릭으로 이루어져 있다.

<br>

#### 추가

LinkedList는 add 함수로 추가할 수 있다.

```java
List<Integer> list = new LinkedList<>();
list.add(1);
list.add(2);
list.add(1, 3); // 인덱스, 값
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i)); // 1 3 2
}
```

함수는 오버로딩으로 이루어져있으며, 하나만 입력할시 마지막에 추가가 된다.

만약 두개의 인덱스가 있다면 첫번째 인덱스에는 몇번째 인덱스에 추가할지 변수를 넣게 된다.

참고로 맨 마지막에 넣을때 last라는 변수가 마지막을 가리키고 있어서 순차적으로 찾아서 넣지 않고 바로 넣게 된다.

<br>

#### 삭제

삭제는 remove로 값을 삭제할 수 있다.

remove(인덱스)이며, 전체를 삭제하고 싶으면 clear()를 하면 된다.

```java
List<Integer> list = new LinkedList<>();
list.add(1);
list.add(2);
list.add(3);
list.remove(1); //1 3
list.clear(); //empty
```

remove 같은 경우는 삭제하고 나서 삭제된 값을 리턴해준다.

<br>

#### 존재 유무

존재 유무는 contains 와 indexOf로 이용하여 알수 있다.

contains 같은 경우는 boolean 값으로 리턴하여 주며, indexOf 같은 경우 인덱스가 있으면 인덱스 값으로 없으면 -1을 리턴한다.

```java
List<Integer> list = new LinkedList<>();
list.add(1);
list.add(2);
list.add(3);
list.indexOf(2); // 1
list.contains(4); //false
```

<br>

#### 얻기

사실 위에서 이미 get을 써서 알고 있으리라 생각한다.

ArrayList와 같이 원하는 인덱스의 값을 얻고 싶으면 get(인덱스)를 적으면 된다.

```java
List<Integer> list = new LinkedList<>();
list.add(1);
list.add(2);
list.add(3);
list.get(0); // 1
```

<br>

<br>

#### Reference

https://psychoria.tistory.com/767

https://opentutorials.org/module/1335/8821
