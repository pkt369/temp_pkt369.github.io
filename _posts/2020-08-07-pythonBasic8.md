---

layout : posts

title : "파이썬 기본 문법8(예외처리)"

date : 2020-08-07

categoris : Python

comments : true

---

파이썬 기본문법 시리즈 8편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)

<h3>예외처리</h3>

- 문법적으로 문제가 없는 코드를 실행하는 중에 발생하는 오류
- 예외처리 구문

**1.**

```python
try:
  #문제가 없을 경우 실행 할 코드
except:
  # 문제가 생겼을 때 실행 할 코드
```

**2.**

```python
try:
  # 문제가 없을 경우 실행 할 코드
except 예외형식1:
  # 문제가 생겼을 때 실행 할 코드
except 예외형식2:
  # 문제가 생겼을 때 실행 할 코드

my_list = [1, 2, 3]
try:
  print("첨자를 입력하세요:")
  index = int(input())
  print(my_list[index] / 0)
except ZeroDivisionError:
  print("0으로 나눌 수 없습니다.")
except IndexError:
  print("잘못된 첨자입니다.")
```

**3.**

```python
try:
  # 문제가 없을 경우 실행 할 코드
except 예외형식1 as e:
  # 문제가 생겼을 때 실행 할 코드
except 예외형식2 as e:
  # 문제가 생겼을 때 실행 할 코드

my_list = [1, 2, 3]  
try:
  print("첨자를 입력하세요:")
  index = int(input())
  print(my_list[index] / 0)
except ZeroDivisionError as e:
  print("0으로 나눌 수 없습니다. ({0})".format(e))
except IndexError as e:
  print("잘못된 첨자입니다. ({0})".format(e))
```

이 경우 오류 메세지의 내용까지 알고싶을때 사용하는 것이다. e에 오류값이 들어가서 같이 반환을 하게 된다.

**4.**

```python
try:
  # 실행할 코드 블록
except:
  # 예외 처리 코드 블록
else:
  # except절을 만나지 않았을 경우 실행하는 코드 블록

  my_list = [1, 2, 3]

try:
  print("첨자를 입력하세요:")
  index = int(input())
  print("my_list[{0}]: {1}".format(index, my_list[index]))
except Exception as err:
  print("예외가 발생했습니다 ({0})".format(err))
else:
  print("리스트의 요소 출력에 성공했습니다.")
```

try에서 코드를 실행해서 오류가 걸리면 except로 가고, 아니면 else로 간다.

**5.**

```python
# 반드시 실행되는 finally

try:
    # 코드 블록
except:
    # 코드 블록
else:
    # 코드 블록
finally:
    # 코드 블록

my_list = [1, 2, 3]

try:
  print("첨자를 입력하세요:")
  index = int(input())
  print("my_list[{0}]: {1}".format(index, my_list[index]))
except Exception as err:
  print("예외가 발생했습니다 ({0})".format(err))
finally:
  print("어떤 일이 있어도 마무리합니다.")

```

try문이 오류이던지 아니던지 finally는 무조건 실행이 되는 코드이다.

**6.** 예외 발생 시키기

```python
try:
    raise Exception("예외를 일으킵니다.")
except Exception as e:
    print("예외가 발생하였습니다. :{0}".format(e))

# 2.
try:
    # 예외 발생

except:
    raise

def some_function():
    print("1~10 사이의 수를 입력하세요:")
    num = int(input())
    if num < 1 or num > 10:
        raise Exception("유효하지 않은 숫자입니다.: {0}".format(num))
    else:
        print("입력한 수는 {0}입니다.".format(num))


def some_function_caller():
    try:
        some_function()
    except Exception as err:
        print("1) 예외가 발생했습니다. {0}".format(err))
        raise
```

위의 코드를 보면 raise를 통해 무조건 예외를 발생시키는 것을 알 수 있다.

**7.**
사용자 정의 예외 발생

```python
# 사용자 정의 예외 형식

class MyException(Exception):
    def __init__(self):
        super().__init__("MyException이 발생했습니다.")

if everything_is_fine == False:
    raise MyException()

```

위의 코드를 보면 Exception을 상속받아 오버라이딩을 하고 있는 것을 볼수 있다.








다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)
