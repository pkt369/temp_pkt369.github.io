---

layout : posts

title : "파이썬 기본 문법6(클래스)"

date : 2020-08-05

categoris : Python

comments : true

---

파이썬 기본문법 시리즈 6편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)
- [파이썬 9편 (파일 입출력, 데이터베이스)](https://pkt369.github.io/pythonBasic9/)

<br>

<h3>클래스</h3>

- 객체(object) = 속성(Attribute) + 기능(Method)
- 속성 : 유형/무형의 특징.
- 기능 : 유형/무형의 특징적인 동작
- 파이썬 : 속성 -> 변수, 기능 -> 함수(메서드)
- 클래스와 객체의 관계
  - 클래스 : 자료형
  - 객체 : 변수

exam)

```python
class Car:
  def __init__(self): # 생성자
    self.size = 11

  def forward(self): # 함수
    pass
```

<br>

**클래스 생성자 호출**
- 클래스의 생성자 호출 시 내부적으로 두 개의 메서드 호출
  - `__new__()` : 클래스의 인스턴스 생성(클래스 메서드)
  - `__init__()` : 인스턴스 변수의 초기화(인스턴스 메서드)
- Magic Method 혹은 Special Method라 불림.

<br>

**클래스 속성 / 인스턴스 속성**
- 클래스 속성
  - 데이터 속성을 초기화 메소드(`__init__()`)가 아닌 클래스에 직접 정의한다면 객체가 정의되기 이전에 존재.
  - 해당 클래스의 모든 인스턴스가 공유.

```python
class Car:
  text_list = [] # 클래스 멤버(인스턴스가 공유하는 멤버로 사용됨)

  def add(self, text):    # 인스턴스 멤버
    self.text_list.append(text)

  def print_list(self):   # 인스턴스 멤버
    print(self.text_list)
```

위에 코드를 보면 text_list가 클래스 속성인것을 볼수 있다.

- 인스턴스 속성
  - 인스턴스와 같은 시점에 정의되는 데이터 속성
  - 데이터 속성 정의는 `__init__()` 메서드 이용.

```python
class Car:
  def __init__(self):
    self.text_list = []

  def add(self, text):    # 인스턴스 멤버
    self.text_list.append(text)

  def print_list(self):   # 인스턴스 멤버
    print(self.text_list)
```

위의 코드를 보면 `__init__`을 볼수 있는데 이것은 생성자이다.  
`a = Car()`을 하게되면 `__init__`이 실행되는 것을 알수 있다.

<br>

**클래스 메서드에 사용되는 self**
- 메소드가 소속되어 있는 객체 자체 의미.
- 클래스 외부에서는 변수명으로 객체를 다룰 수 있지만 내부에서는 객체를 지칭할 이름이 없으므로 self를 사용.
- java의 객체 자신을 가리키는 this와 같다.

<br>

**정적 메서드(Static Method)**
- 클래스를 통해 호출 가능한 메서드
- `@staticmethod` 데코레이터로 수식.
- self 매개변수 없이 정의(self 매개변수를 전달받을 방법이 없음)
- 정의 형식
  - class 클래스이름:
    @staticmethod
    def 메서드이름(매개변수):
      pass

```python
class Calculator:
  @staticmethod # static 메서드
  def plus(a, b): # self 키워드 필요 없음
    return a + b

if __name__ == '__main__':
  print('{0} + {1} = {2}'.format(7, 4, Calculator.plus(7, 4)))
```

위의 코드를 보면 생성하지 않고 메소드를 불러낼수 있는 것을 볼 수 있다.

**Private Member**
- 클래스의 안에서만 접근이 가능한 멤버
- 작명법(Naming)으로 private/public 멤버 구분
- private 멤버의 명명 규칙
  - 두 개의 밑줄 __ 이 접두사여야 함. 예) `__number`
  - 접미사는 밑줄이 한 개까지만 허용 예) `__number_`
  - 접미사의 밑줄이 두 개 이상이면 public 멤버로 간주함. 예) `__number__`

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)
- [파이썬 9편 (파일 입출력, 데이터베이스)](https://pkt369.github.io/pythonBasic9/)
