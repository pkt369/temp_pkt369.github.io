---

layout : posts

title : "파이썬 기본 문법2(튜플, 딕셔너리)"

date : 2020-07-29

categoris : python

---

파이썬 기본문법 시리즈 2편입니다

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)



<h4>튜플(Tuple)</h4>

- 기본적인 문법 : ()를 통해서 생성
- 새로운 요소를 추가하거나 삽입할수 없고, 기존 요소를 삭제할 수 없다.
- 소프트웨어 향상에 도움

##### 요소가 하나뿐인 튜플 정의하기 #####

```python
e = (1,)
type(e) --> tuple
f = 1,
type(f) --> tuple
```

**슬라이싱이 가능**
```python
x = (1, 2, 3, 4, 5, 6)
print(x[4:6]) --> (5, 6)
print(x[:2]) --> (1, 2)
print(x[4:]) --> (5, 6)
```

**+연산자를 통한 튜플간 결합도 가능**
```python
m = (1, 2, 3)
n = (4, 5, 6)

concat = m + n
concat --> (1, 2, 3, 4, 5, 6)
```

**튜플 메소드**
- index() : 매개변수와 같은 데이터를 찾아서 인덱스 반환, 없으면 오류

```python
a = ('abc', 'def', 'ghi')
print(a.index('ghi') --> 2
```

- count() : 매개변수로 입력한 데이터 일치하는 요소의 갯수를 반환

```python
b = (1, 100, 2, 200, 3, 300)
print(b.count(100)) --> 1
print(b.count(3)) --> 1
```

- 튜플 패킹(tuple packing) : 여러 가지 데이터를 튜플로 묶는 것.

```python
a = 1, 2, 3 # 괄호가 없어도 튜플로 묶어줌
print(a) --> (1, 2, 3)
```

- 튜플 언패킹(tuple Unpacking) : 각 요소를 여러 개의 변수에 할당하는 것.

```python
data = 'Seoul', 37.541, 126.986  # 지역 / 경도 / 위도

city, latitude, longitude = data

print(city) --> Seoul
print(latitude) --> 37.541
print(longitude) --> 126.986
```

<h4>딕셔너리(Dictionary)</h4>

- 기본적인용법: { } 를이용해서생성.
- 리스트처럼첨자를이용해서요소에접근하고, 변경할수있음.
- 요소에접근할때0부터시작하는수첨자뿐아니라, 문자열과숫자를비롯해서변경이불가능한형식이면어떤자료형이든사용가능.
- 첨자는키(key)라하고, 이키가가리키는슬롯에저장되는데이터를일컬어값(value)라함.
- 딕셔너리는키-값의쌍으로구성.
- 탐색속도가빠르고, 사용하기도편함.
- 새로운키-값을입력하거나딕셔너리안에있는요소를참조할때는리스트와튜플에서처럼대괄호[ ]를이용.


**사용 예**

`dic = {}` : 딕셔너리 생성
`dic['파이썬'] = "www.python.org"` : 동적으로 입력, 번호대신 문자로 키값 가능  
`dic['애플'] = 'www.apple.com'`  
`dic['파이썬']` : 'www.python.org'를 반환  
`dic` : { 'www.python.org', 'www.apple.com' }  

**딕서녀리 메소드**

- keys() : 키의 목록 출력
`print(dic.keys())` : dict_keys(['애플', '네이버', '파이썬'])

- values() : 값의 목록 출력
`print(dic.values())` : dict_values(['www.apple.com', 'www.naver.com', 'www.python.org'])

- items() :키와 값의 쌍으로 이루어진 전체 목록 반환
`print(dic.items())` : dict_items([('애플', 'www.apple.com'), ('네이버', 'www.naver.com'), ('파이썬', 'www.python.org')])

- in : 안에 키 또는 내용이 있는지 확인
`print('애플' in dic.keys())` or `print('www.apple.com' in dic.value())` : True값 반

- pop() : 받은 인덱스값 제거
`print(dic.pop('애플'))` : 키가 '애플'인 값 제거

- clear() : 딕셔너리 데이터 삭제
`print(dic)` : {} 반환

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
