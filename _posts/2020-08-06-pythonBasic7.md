---

layout : posts

title : "파이썬 기본 문법7(상속)"

date : 2020-08-06

categoris : Python

comments : true

---

파이썬 기본문법 시리즈 7편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)

<h3>상속</h3>

**정의**
- class 기반 클래스: #멤버 정의
- class 파생클래스(기반클래스):
  - 아무 멤버를 정의하지 않아도 기반 클래스의 모든 것을 물려받아 갖게 됨.
  - 단, private 멤버(__ 로 시작되는 이름을 갖는 멤버)는 제외.

```python
class Base:
  def __init__(self):
    print(self)
    self.message = "Hello, World"

  def print_message(self):
    print(self.message)

class Derived(Base):
  pass

if __name__ == '__main__':
  base = Base()
  base.print_message()

  a = Derived()
  a.print_message()
```

위의 코드를 보시면 `Derived(Base)`를 통해 상속을 받고 `main`에서 `pass`를 적었음에도 불구하고 `Base`의 함수를 쓰고 있는 것을 볼 수 있습니다.

<br>

**다형성**
- 여러가지 형태를 가질 수 있는 능력

```python
# 다형성(Polymorphism)
class ArmorSuite:
  def armor(self):
    print('armored.')

class IronMan(ArmorSuite):
  pass

def get_armored(suite):
  suite.armor()

if __name__ == '__main__':
  suite = ArmorSuite()
  get_armored(suite)

  iron_man = IronMan()
  get_armored(iron_man)
```

위의 코드를 보면 IronMan에서 상속을 받아서 다른 클래스지만 같은 결과값을 가져오는 것을 알수 있다.  

같은 모양의 코드가 다른 기능을 하는것이 다형성이다.

<br>

**super()**
- 부모클래스의 객체 역할을 하는 프록시(Proxy)를 반환하는 내장 함수.

```python
class A:
    def __init__(self):
        print("A.__init__()")
        self.message = "Hello"

class B(A):
    def __init__(self):
        super().__init__()      #A.__init__(self)
        print("B.__init__()")

        print("self.message is "+ self.message)

if __name__ =="__main__":
    obj = B()

    print(obj.message)
```

위의 코드를 보면 `self.message`가 생성자에 있는데 A 클래스를 생성하지않아서 B에서 생성을 해서 사용하는 것을 볼수 있다.

클래스가 생성되지 않으면 `self.message`가 생성이 되지 않는다는 것을 알 수 있다.

<br>

**다중 상속**
- 자식클래스 하나가 여러 부모 클래스로부터 상속받는 것.

```python
class A:
  pass

class B:
  pass

class C:
  pass

class D(A,B,C):
  pass
```

만약 A에 있는 함수가 B에도 똑같은 이름의 함수가 있다면 매개변수에서 앞에 있는 A의 함수를 사용하게 된다.

<br>

**오버라이딩**
- 부모클래스로 부터 상속받은 메서드를 다시 자식 클래스에 정의하는것

```python
class A:
  def message(self):
    print("A")

class B(A):
  def message(self):
    print("B")

if __name__=='__main__':
  B().message()
```

위의 코드의 답은 B가 나온다. 똑같은 이름의 message를 상속받지만 오버라이딩하면서 A의 기능에서 변경해서 사용했다.

<br>

**데코레이터**
- 함수를 꾸미는 객체
- `__call__()` 메서드를 구현하는 클래스
  - 객체를 함수 호출 방식으로 사용하게 만드는 메서드

```python
class Callable:
    def __call__(self):
        print("I am called")

if __name__ == '__main__':
    obj = Callable()
    obj()
```

위의 코드를 보면 obj()를 볼수 있는데 `obj()`를 부르면 call의 메서드를 부르게 된다.

응용)

```python
class MyDecorator:
    def __init__(self, f):
        print("Initializing MyDecorator...")
        self.func = f #MyDecorator의 func 데이터 속성이 print_hello를 받아둠.

    def __call__(self):
        print("Begin:{0}".format(self.func.__name__))

        self.func() # __call()__ 메서드가 호출되면 생성자에서 저장해둔 함수

        print("End:{0}".format(self.func.__name__))

def print_hello():
        print("Hello")

if __name__=='__main__':
    print_hello2 = MyDecorator(print_hello)

    print_hello2()
```

```python
class MyDecorator:
    def __init__(self, f):
        print("Initializing MyDecorator...")
        self.func= f

    def __call__(self):
        print("Begin:{0}".format(self.func.__name__))
        self.func()
        print("End:{0}".format(self.func.__name__))

@MyDecorator
def print_hello():
    print("hello!!!!")

if __name__ == '__main__':
    print_hello()
```

위 코드에서는 일반 코드이고 밑에 코드는 @데코레이션을 사용한 코드입니다. 보시면 간결해지신것을 보실수 있습니다.

두개다 같은
`Initializing MyDecorator...`  
`Begin:print_hello`  
`hello!!!!`  
`End:print_hello`  
가 나오게 됩니다.

<br>

**for문 순회 가능 객체 만들기**
예)
- list
```python
list = [1, 2, 3]
for e in list:
  print(e)
```  

- iterator()

```python
iterator = range(3).__iter__() print(iterator.__next__()) print(iterator.__next__()) print(iterator.__next__()) print(iterator.__next__()) # error
```

위의 코드를 보면 이터레이터는 없는 인덱스값을 찾으면 오류가 걸리는 것을 알수 있다.

- 제너레이터(Generator)

```python
def generator():
    yield 0 # __iterator__가 생성된다고 생각을 하면 된다.
    yield 1
    yield 2
    yield 3

iterator = generator()
print(iterator.__next__())
print(iterator.__next__())
print(iterator.__next__())
print(iterator.__next__())
```

위의 코드를 보면 `yield`가 이터레이터 인덱스 갯수를 하나 늘려준다고 생각을하면 된다.

그러면서 뒤에있는 숫자값을 넣어줘서 인데스0번은 0의 값을 가지게 된다.

<br>

**상속의 조건 : 추상 기반 클래스**
- 자식 클래스가 갖춰야 할 특징(메서드)을 강제하는 기능.
- 강제 조건 규약에 따르지 않으면 TypeError 예외 발생.
- metaclass = ABCMeta 클래스와 @abstractmethod 데코레이터를 이용

```python
from abc import ABCMeta
from abc import abstractmethod

class AbstractDuck(metaclass=ABCMeta):
    @abstractmethod
    def Quack(self):
        pass

class Duck(AbstractDuck):
    def Quack(self):
        print("[Duck] Quack")

if __name__=='__main__':
    duck = Duck()
    duck.Quack()
```

위의 코드를 보면 `AbstractDuck(metaclass=ABCMeta)`를 볼수 있다. metaclass=ABCMeta와 @abstractmethod를 이용하면 강제성을 지닐 수 있다.


다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)
