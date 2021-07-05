---

layout : posts

title : "자바 문자 나누기 & 합치기"

date : 2020-07-22

categoris : javaScript

---

자바에서 문자를 나누는 함수가 있습니다.

바로 `subString`과 `split`이 있습니다.

먼저 `subString`을 먼저 살펴봅시다.

<h4>subString</h4>

```java
String st = "Hello-Java-World"; //앞에서부터 0 ~이다.

st.subString(4); // Hello (0~4 인덱스를 불러온다)

st.subString(6,9) // Java (시작위치, 끝위치)
```

**subString은 (시작위치, 끝위치)를 매개변수로 받습니다.**

<hr>

<h4>split</h4>

`split`은 특정 문자를 기준으로 나누어서 배열로 저장해주는 편리한 함수입니다.

```java
String st = "Hello-Java-World"

st.split("-") //-를기준으로 단어들이 나뉘며 지금은 hello, java, World로 나뉜것이다.
```

<hr>

<h4>다시 문자 붙이기</h4>

`split`을 이용해 나눈 문자를 다시 붙이는 방법입니다.

생각보다 쉬우니 바로 코드를 보여드리겠습니다.

```java
String st = "Hello-Java-World";

String[] sp = st.split("-"); //hello, java, world로 나뉨
String result = "";

for(int i = 0; i < sp.length; i++){
  if(sp[i].equals("Java")){
    //만약 Java가 있다면 포문을 건너뛰어라(저장안되게한다는 뜻)
    continue;
  }
  result += (sp[i] + " "); //사이에 띄워쓰기 넣기
}

System.out.println(result); //Hello World
```

저도 함수를 찾다가 안보여서 제가 만들어서 썼습니다.
생각보다 간단하죠?
