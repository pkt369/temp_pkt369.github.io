---

layout : posts

title : "파이썬 기본 문법1(변수, 문자열)"

date : 2020-07-24

categoris : Python

---

파이썬의 기본문법 시리즈 1편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편 (튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편 (조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)
- [파이썬 9편 (파일 입출력, 데이터베이스)](https://pkt369.github.io/pythonBasic9/)

파이썬은 다른 언어들과 비슷하면서도 가장 쉽다고 알려진 언어중 하나입니다.

바로 문법 공부를 시작해 봅시다!!

**변수명 규칙** :
- 문자, 숫자, _ 가능. 단, 숫자로 시작할 수 없음.
- 대/소문자 구별
- 예약어 사용 불가능

**수치형** : `int, float, double, complex`(복소수)

**연산자** : +,-,* ,/,//,%, * (거듭제곱)
**/** : 소숫점을 포함한 몫, **//** : 소숫점이 없는 몫

**math를 이용한 계산** : `import math`
- `math.pi` : 원주율
- `math.3`  : 자연상수
- `abs`     : 절댓값
- `round` : 반올림(내장함수)
- `math.trunc` : 버림함수
- `math.pow(x, y)` : x * (y의 갯수만큼 곱하기) x -> 3,3 : 3 * 3 * 3
- `math.sqrt(81)` : 제곱근 계산 -> 9
- `27 ** (1/3)` : 세제곱근 계산 -> 3

<hr>

<h4>문자열</h4>

**문자열함수(+, *)**
```python
print("Py"+"thon") -->Python
print("Py","thon") -->Py thon
print("Py""thon") -->Python
```

쉼표는 스페이스바를 하나 넣는것이고, 나머지는 그냥 붙여지는것이다.  
**주의)** String과 int형 붙여도 자바와 다르게 자동형변환을 하지않아 오류가 걸린다.

`print('python ' * 3)` --> python python python : 문자를 곱하면 문자가 곱한만큼 나온다.

<br>

```python
s = 'Good Morning'
print(s[0:6]) --> Good M
print(s[5:12]) --> Morning
```
인덱스 번호로도 찾을 수 있다.

```python
print('M' in s) --> true
print('m' in s) --> false

print('Good' in s) --> true
print('morning' in s) -->false
```

존재 유뮤를 확인할땐 `in 키워드`를 써서 확인을 할수 있다.

**길이확인** : `len(s)` --> 길이를 알수있는 함수이다.

<hr>

<h4>비교연산자</h4>

너무간단하다.
 - AND : 비교 대상의 두개다 충족
 - OR : 둘중 하나만 맞아도 충족
 - NOT : 조건의 반대가 맞을 때 충족

<hr>

<h4>List</h4>

- 데이터의 목록을 다루는 자료형
- 리스트를 만들때 [ ] (대괄호) 사용

**특징**
 - 슬라이싱이 가능 :
 ```python
 x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
 print(x[0:5]) --> [1, 2, 3, 4, 5]
 print(x[5:]) --> [6, 7, 8, 9, 10]
 print(x[:3]) --> [1, 2, 3]
 ```

- '+' 연산자를 통한 리스트간의 결합 기능
```python
a = [1, 2, 3, 4, 5]
b = [6, 7, 8, 9, 10]
print(a + b)
```
- 특정 위치에 있는 데이터를 변경
 ```python
a = [1, 2, 3, 4, 5]
a[2] = 30
print(a) --> [1, 2, 30, 4, 5]
print(len(a)) --> 5
```

**List 제공 메소드**
- append() : 리스트의 끝에 새로운 요소 추가
```Python
a = [1, 3, 5]
a.append(7)
print(a) --> [1, 3, 5, 7]
```

- extend() : 기존 리스트에 다른 리스트를 이어 붙임(+ 연산자와 같은 기능)
```python
b = [9, 11, 13]
a.extend(b)
print(a) --> [1, 3, 5, 7, 9, 11, 13]
```

- insert(인덱스, 데이터) : 인덱스로 명시한 리스트 내의 위치에 새 요소를 삽입
```python
a.insert(1, 2) # 1번째 위치에 2를 삽입(인덱스번호는 1이 2번째이다.)
print(a) --> [1, 2, 3, 5, 7, 9, 11, 13]
```

- remove() : 매개변수를 입력한 데이터를 리스트에서 찾아 발견 첫번째 요소를 삭제
```python
a.remove(11)  # 삭제 값 지정
print(a) --> [1, 2, 3, 5, 7, 9, 13]
```

- pop() : 리스트의 마지막 요소를 뽑아 리스트에서 제거.
```python
a.pop()
print(a) --> [1, 2, 3, 5, 7, 9]

a.pop(1) # 인덱스 지정
print(a) --> [1, 3, 5, 7, 9]
```

- index() : 리스트 내에서 찾은 데이터 중 첫번째 요소를 반환, 없으면 오류 발생
```python
a = ['abc', 'def', 'ghi']
print(a.index('ghi')) --> 2
```

- count() : 입력한 매개변수와 같은 갯수를 반환
```Python
a = [1, 100, 2, 200, 3, 300]
print(a.count(100)) --> 1
```

- sort() : 리스트 내의 요소 정렬, Default는 오름차순, reserve=True입력시 내림차순
Tip) 키워드 매개변수 : reserve=True와 같이 이름을 명시하여 사용하는 매개변수
```Python
a = [7, 5, 9, 4, 2]
a.sort()
print(a) --> [2, 4, 5, 7, 9]

a.sort(reverse=True)
print(a) --> [9, 7, 5, 4, 2]
```

- reserve() : 리스트 내 요소를 반대로 뒤집는다.
```Python
a = [7, 5, 9, 4, 2]
a.reverse()
print(a) --> [2, 4, 9, 5, 7]
```

다른 파이썬 기본문법 시리즈는
- [파이썬 1편 (튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편 (조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)
- [파이썬 9편 (파일 입출력, 데이터베이스)](https://pkt369.github.io/pythonBasic9/)
