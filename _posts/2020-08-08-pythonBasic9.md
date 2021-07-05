---

layout : posts

title : "파이썬 기본 문법9(파일 입출력, 데이터베이스)"

date : 2020-08-08

categoris : python

comments : true

---

파이썬 기본문법 시리즈 마지막편인 9편입니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)

<h3>파일입출력</h3>

파일 처리 파이썬 함수는 간단하게
![image](https://user-images.githubusercontent.com/66049273/89366135-3a415f00-d711-11ea-8e1f-4dc78d06fc6b.png)
이렇게 나뉜다.

**open(file, mode)**
- file : 실제 파일의 문자열 경로
- mode
![image](https://user-images.githubusercontent.com/66049273/89366230-71177500-d711-11ea-81c6-1d99e3747d7b.png)
- file에 write하기.

```python
file = open('test.txt', 'w') # a는 덧붙이기로 사용가능
file.write('hello')
file.close()
```

- file에 read하기.

```python
file = open.('test.txt', 'r')
str = file.read()
print(str)
file.close()
```

위의 코드들을 보면 close를 해줘야한다는 것을 알수 있다.

하지만 코드들을 짜다보면은 까먹는 경우가 있다. 그래서 처음부터 코드를 짤 때 이 코드를 쓴다.

**자원 누수 방지를 돕는 with ~ as**
- 구문 형식

```python
with open(파일이름) as 파일객체:
  #코드블록
  #이곳에서 읽거나
  #쓰기를 한 후
  #그냥 코드를 빠져나가면 됩니다.

with open('test.txt', 'rt') as file:
  str = file.read()
  print(str)
```

위코드를 보면 close하지 않아도 된다는 것을 알수 있다.

<br>
<br>

**텍스트 파일 쓰기**
- 문자열은 담은 리스트를 파일에 쓰는 `writelines()` 메서드.

```python
# ex1)
lines = ["we'll find a way we always have - Intersteller\n",
         "I'll find you and I'll kill you - Taken\n",
         "I'll be back - Terminator2\n"]

with open('movie_quotes.txt', 'w') as file:
    for line in lines:
        file.write(line)

# ex2)
with open('movie_quotes.txt', 'w') as file:
    file.writelines(lines)
```

위의 코드를 보면 write는 포문을 통해 한줄씩 넣어준다는 것을 알수 있고, writelines는 알아서 전체를 넣어준다는 것을 알수 있다.

**텍스트 파일 읽기**
- 줄 단위로 텍스트를 읽는 readline() & readlines() 메서드

```python
with  open('movie_quotes.txt', 'r') as file:
    line = file.readline()

    while line != '':
        print(line, end='')
        line = file.readline()
----------------------------------------------------

with open('movie_quotes.txt', 'r') as file:
    lines = file.readlines()
    line = ''
    for line in lines:
        print(line,end='')
```

위의 코드는 보면 readline이 보이는데 한줄을 읽어오는 코드이다.

while문을 통해 line의 모든 내용을 가져올때 까지 반복해준다는 것을 알수 있다.

readlines 함수는 파일의 모든 줄을 읽어서 리스트로 돌려준다.

lines는 리스트이며 line에 값을 넘겨줘서 모든줄을 다 읽어올때까지 반복한다.

<hr>

<h3>DataBase 연동</h3>

파이썬에서 database는 추가 설치없이 내장되어있는 패키지로 가능하다.

**연동하기**

```python
import sqlite3 #파이썬3에는 SQLite 라이브러리가 기본 탑재

conn = sqlite3.connect('test.db') # 1. 커넥션 열기
cursor = conn.cursor() # 커서 열기

cursor.execute() # 커서를 이용하여 데이터 추가/조회/수정/삭제하기

cursor.close() # 커서 닫기
conn.close() # 커넥션 닫기
```

위의 코드를 보면 자바에서 데이터베이스를 사용할때와 비슷하다.

**테이블 생성하기**

```python
import sqlite3

# test.db 파일 안에 phonebook 테이블 생성
conn = sqlite3.connect('test.db')
cursor = conn.cursor()

cursor.execute("""
create table phonebook (
    name char(32),
    phone char(32),
    email char(64) primary key)
""")

cursor.close()
conn.close()
```

**테이블에 정보 추가하기**

```python
import sqlite3

# test.db파일안에 phonebook 테이블 생성
conn = sqlite3.connect('test.db')
cursor = conn.cursor()

cursor.execute("""
insert into phonebook values(?, ?, ?)
""", ('홍길동', '010-5555-5555', 'hong@gildong.com'))

id = cursor.lastrowid
print(id)

conn.commit() # 데이터베이스는 트랜잭션을 해주고있어서 최종으로 커밋을해줘야 반영이 된다.

cursor.close()
conn.close()
```

**테이블 불러오기**

```python
import sqlite3

conn = sqlite3.connect('test.db')
cursor = conn.cursor()

cursor.execute("select * from phonebook")

rows = cursor.fetchall()

for row in rows:
    print("name:{0}, phone:{1}, email:{2}".format(row[0], row[1], row[2]))

cursor.close()
conn.close()
```

**테이블 변경하기**

```python
import sqlite3

conn = sqlite3.connect('test.db')
cursor = conn.cursor()

cursor.execute("""
update phonebook set phone=?, email=? where name=?
""", ('010-5555-5555', 'hong@hack.com','홍길동')
)

conn.commit()

cursor.close()
conn.close()
```

**데이터 삭제하기**

```python
import sqlite3

conn = sqlite3.connect('test.db')
cursor = conn.cursor()

cursor.execute("""
delete from phonebook where email=?
""", ('hongkd@hong.com',) # 튜플이라는 것을 증명하기 위해서 ,를 통해 오류를 없애줘야한다. (혼자일때만 사용)
)

conn.commit()

cursor.close()
conn.close()
```

코드중간중간에 설명을 해놓았습니다.

이것으로 파이썬 기초를 끝냅니다.

다른 파이썬 기본문법 시리즈는
- [파이썬 1편(변수, 문자열)](https://pkt369.github.io/pythonBasic1/)
- [파이썬 2편(튜플, 딕셔너리)](https://pkt369.github.io/pythonBasic2/)
- [파이썬 3편(조건문, 반복문)](https://pkt369.github.io/pythonBasic3/)
- [파이썬 4편 (함수)](https://pkt369.github.io/pythonBasic4/)
- [파이썬 5편 (모듈, 패키지)](https://pkt369.github.io/pythonBasic5/)
- [파이썬 6편 (클래스)](https://pkt369.github.io/pythonBasic6/)
- [파이썬 7편 (상속)](https://pkt369.github.io/pythonBasic7/)
- [파이썬 8편 (예외처리)](https://pkt369.github.io/pythonBasic8/)
