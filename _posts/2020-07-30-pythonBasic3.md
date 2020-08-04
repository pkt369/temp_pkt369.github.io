---

layout : posts

title : "파이썬 기본 문법3(조건문, 반복문)"

date : 2020-07-30

categoris : Python

---

파이썬 기본문법 시리즈 3편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편 (변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편 (튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)

<h4>조건문</h4>

- 자바와 거의 똑같으며 조건문을 통해 원하는 코드 실행합니다.

```python
print('요일(월~일)을 입력하세요: ')
dow = input()

if dow == '월':
    print('Monday')
elif dow == '화':
    print('Tuesday')
elif dow == '수':
    print('Wednesday')
elif dow == '목':
    print('Thursday')
elif dow == '금':
    print('Friday')
elif dow == '토':
    print('Saturday')
elif dow == '일':
    print('Sunday')
else:
    print('잘못 입력된 요일입니다.')
```

해설) `print()`는 출력을 담당하는 메소드이고, 입력으로 받는 메소드는 `input()` 입니다.  
자바와 다른점은 괄호들이 없고 대신에 **:** 와 **들여쓰기** 로 구분하고 있습니다.  
자바에서는 `else if`로 쓰는 것은 파이썬에서는 `elif`로 쓰고 있습니다.

<hr>

<h4>반복문(while, for)</h4>

```python
print('몇 번 반복할까요? : ')

num = int(input())
count = 0

while count < num:
    count = count+1
    print("{0}회 반복".format(count))

print('반복 종료')
```

해석) while문은 조건에 따라서 반복한다.  
따라서 num의 숫자에 따라 횟수가 정해지고, {0}는 .format(count)를 통해 안의 숫자가 바뀌게 된다.  
만약 2를 입력했을때 : 1회반복 2회반복 반복종료

<br>



```Python
for i in (10, 20, 30):
    print(i) --> 10, 20, 30
```


해석) ()안에 값을 넣었기 때문에 튜플이고, 10부터 순서대로 i에 들어가면서 실행된다.

<br>

```python
for s in '더조은 컴퓨터 아카데미':
  print(s) --> 더조은 컴퓨터 아카데미
```

해석) 문자는 한글자씩 s에 들어가 실행되게 된다.

<br>

```python
for i in range(0, 5, 1):
    print(i) --> 0, 1, 2, 3, 4
```

해석) range는 가장 많이 쓰이는 것중하나인데, 0부터 인데스 5까지(0 ~ 4) 간격은 1만큼 보여달라는 뜻이다.  
간격이 1일때는 생략가능하다.

<br>

**별모양 만들기**
```python
for i in range(1,6):
    for j in range(i):
        print("*", end=" ") #이스케이프 스퀀스도 가능
    print() # 줄바꿈
    #*
    #* *
    #* * *
    #* * * *
    #* * * * *
```

위의 range를 제대로 이해하면 쉽게 이해했을거라고 생각합니다.  
end는 print했을때 맨끝에 문자를 붙여주는 기능입니다.

**딕셔너리를 이용해 반복문 만들기**

```python
dic = {'애플':'www.apple.com', '파이썬':'www.python.org', '네이버':'www.naver.com'}

for k, v in dic.items():
    print("{0}:{1}".format(k, v))
```

items()는 키와 값을 둘다 반환하는 메소드이다. 따라서 포문에서 k, v 두개의 변수를 생성했고, .format을 통해서 값들을 받아오게했다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편 (변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편 (튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
