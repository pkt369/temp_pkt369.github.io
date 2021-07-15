---
layout : posts

title : "Primitive type 과 Wrapper class 차이"

date : 2021-07-14

categories : java

comments : true
---



자바에는 기본형(Primitive type)과 참조형(Reference type)이 있다.

Wrapper class 는 참조타입의 기본형이다.

그럼 기본형과 Wrapper class 의 차이는 뭘까?

<br>

### Primitive type(기본형)

| Type    | Size    | Range                                                  |
| ------- | ------- | ------------------------------------------------------ |
| byte    | 1 byte  | -128 ~ 127                                             |
| short   | 2 bytes | -32, 768 ~ 32, 767                                     |
| int     | 4 bytes | -2,147,483,648 ~ 2,147483,647                          |
| long    | 8 bytes | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 |
| float   | 4 bytes | 1.4E-45 ~ 3.4028235E38                                 |
| double  | 8 bytes | 4.9E-324 ~ 1.7976931348623157E308                      |
| char    | 2 bytes | 0 ~ 65,536 (unsigned)                                  |
| boolean | 1 byte  | true, false                                            |

기본형은 총 8개가 있으며, `short, int, long, float, double, byte, char, boolean`이 있다.

<br>

### Reference type(참조형)

기본형을 제외한 모든 타입이 참조형 타입이며, null값을 가질 수 있다.

참조형은 주소값을 가지며, 그 주소값은 Heap영역에 저장이 된다.

기본형과 다르게 크기가 정해져 있지않으며 메모리에서 동적으로 할당한다.

참조하는 변수가 없으면 자바의 가비지 컬렉터(Garbage collector)가 제거하여 메모리를 관리한다.

<br>

### Wrapper class

Wrapper class 는 기본형을 **Boxing(박싱)**하여 원시타입(Primitive type)을 참조타입으로 변환 시킨 것을 말한다.

반대로 참조 타입을 원시타입으로 변환시키는 **Unboxing(언박싱)**도 있다.

ex) int -> Integer, char -> Character

<br>

### Wrapper class 와 Primitive type의 차이

1. Wrapper class는 참조타입이라 Heap에 저장되는 반면 Primitie는 Heap영역에 저장되지 않는다.
2. 기본형은 null이 들어갈수 없으나, Wrapper class 는 참조타입이라 null 이 들어갈 수 있다.
3. 기본형은 제네릭 타입에서 사용할수 없으나, Wrapper class 에서는 사용할수 있다.

<br>

### 왜 Wrapper class를 잘 쓰지 않는 걸까?

먼저 왜 기본형을 만들었는지에 대해 궁금증을 가져야 위의 문제에 대답할 수 있다.

일단 기본형은 Stack에 쌓인다. 힙에 저장하지않아 참조비용이 발생하지 않는다.

또한 접근속도도 힙에서 참조하지 않아서 빠르다.

![primitive-wrapper](https://user-images.githubusercontent.com/66049273/125546089-d6f68fb2-d192-47f1-86b7-fc4469ed24cd.gif)

참조 : https://www.baeldung.com/java-primitives-vs-objects

<br>

또한 참조 타입이 사용하는 메모리의 양이 압도적으로 높으므로 메모리적으로도 효율적이다.

(64비트 컴퓨터 기준)

|              | Primitive type 의 사용 메모리 | Reference type 의 사용 메모리 |
| ------------ | ----------------------------- | ----------------------------- |
| boolean      | 1bit                          | 128 bits                      |
| byte         | 8bits                         | 128 bits                      |
| short, char  | 16 bits                       | 128 bits                      |
| int, float   | 32 bits                       | 128bits                       |
| long, double | 64 bits                       | 192 bits                      |

<br>

### 마무리

성능상 이점이 있는 기본형을 먼저 써야하고, 제네릭 타입같이 필요한 경우에만 Wrapper class로 변환하여 사용해야 한다.

