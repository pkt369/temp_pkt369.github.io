---

layout : posts

title : "파이썬 기본 문법4(함수)"

date : 2020-07-31

categoris : Python

comments : true

---

파이썬 기본문법 시리즈 4편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)

<h3>함수</h3>

**함수 정의**
- 기본 정의 문법

```python
def 함수이름(인자1, 인자2, ...):
  #코드블록
  return 반환값
```

- 키워드 매개 변수(Keyword Argument)

```python
def print_person(name, job='Programmer'):
  print('name: {0}'.format(name))
  print('position: {0}'.format(job))
```

이름은 필수로 적어줘야하고 job은 적지 않으면 기본값으로 Programmer가 된다.

두번째 매개변수를 적는다면 Programmer는 사라지게 되는 것이다.

- 가변 매개 변수(Arbitrary Argument List)

```python
def 함수이름(*매개변수):
  코드블록
  ...
```

`*매개변수`는  여러개의 인자를 받아오겠다는 소리이고 튜플 형태로 받아온다..

응용)

```python
def merge_string(*text_list) :
  result = ''
  for s in text_list:
    result += s

  return result

print(merge_string('아버지가', '방에', '들어가신다.'))
```
답은 아버지가방에들어가신다 가 나온다.


<br>
<hr>

<h4>** 매개변수</h4>

```python
def 함수이름(**매개변수):
  코드블록
  ...
```

** 매개변수는 파라미터 명을 같이 전달할 수 있고, 딕셔너리형태로 받아온다.

ex)

```python
def print_team(**players):
  for k in players.key() :
    print('{0} = {1}'.format(k, players[k]))

print_team(손흥민='축구', 서장훈 = '농구')
```

players 는 딕셔너리이고 손흥민=축구, 서장훈 = 농구를 반환한다.

**가변매개변수 사용시 주의점!**

```python
def print_args1(argc, *argv):
    for i in range(argc):
        print(argv[i])

print_args1(3, '홍길동', '이순신', '강감찬')
print_args1(argc = 3, '홍길동', '이순신', '강감찬') # 오류
print_args1('홍길동', '이순신', '강감찬', argc = 3) #오류
print_args1('홍길동', '이순신', '강감찬', 3) #오류
```

가변 매개변수가 두번째 인자로 있다면 오류가 아닌 첫번째 문장을 잘지켜서 적어서 사용해야한다.

두번째 주의점)

```python
def print_args2(*argv, argc):
    for i in range(argc):
        print(argv[i])

print_args2('홍길동', '이순신', '강감찬', argc = 3)
print_args2('홍길동', '이순신', '강감찬', 3) # 오류
```

가변인자가 앞에 올경우 `argc=`를 써줘야 오류가 나지 않는다.

<hr>

<h4>호출자에게 반환</h4>

<br>

**함수 즉시 종료/호출자에게 결과 전달**

return은 값을 전달하거나 함수를 종료 2가지 기능이 있다.

<h6>값전달</h6>

```python
def multiply(a, b):
  return a * b

print(multiply(3, 5)) # 15
```

<h6>함수 종료</h6>

```python
def abc(a):
  if a == 0:
    return
  else:
    print(a)
```

- 변수의 유효 범위

```python
def scope_test1():
    a = 1
    print('a:{0}'.format(a))

a = 0 # 함수 밖 변수 선언
scope_test1()
print('a:{0}'.format(a))
```

답은 1, 0 이렇게 나옵니다. 함수 안의 지역변수와 바깥에 선언된 전역변수이기 때문에 이렇게 값이 나옵니다.

그러면 함수내에서 쓴 지역변수를 바깥에서도 사용하고 싶으면 어떻게 해야할까요?  
그 답은 코딩을 통해 보여드리겠습니다.

```python
def scope_test2():
    global c # global 키워드 : 전역변수, 지역변수의 생성을 막는다.
    c = 1
    print('c:{0}'.format(c))

c = 0
print('c:{0}'.format(c))
scope_test2()
print('c:{0}'.format(c))
```

정답은 0, 1, 1 이 나온다. global을 통해 바깥에서도 사용을 할수 있게 만들었다.

- 함수를 변수에 담아 사용이 가능하다

```python
def print_a(a):
  print(a)

print_a("A") # A 반환
```

- 기능의 구현을 미루기

```python
# pass : 기능의 구현을 잠시 미루자

def empty_function():
    pass

empty_function() # pass가 없으면 오류가 걸린다.

#cf)
class empty_class:
    pass
```

pass 를 통해서 클래스나 함수를 비울수 있으나 사용을하면 오류가 걸린다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
