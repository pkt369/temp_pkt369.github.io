---

layout : posts

title : "자바 ListSelectionListener 사용법"

date : 2020-07-17

categoris : java

---

자바에서 List를 선택할땐 앞에서 [포스팅](https://pkt369.github.io/JavaActionListener/)했던 ActionListener로 선택되지 않는다.

list로 값을 받아와 액션을 하는 방법을 알려드리겠습니다.

먼저 코드를 먼저 보여드리고 설명을 하겠습니다.

```java
class listExample extends JPanel implements ListSelectionListener{
  setLayout(null);
  String[] st = {"하나" , "둘", "셋"};
  JList<String> jl;
  JScrollPane jp;

  listExample(){
    jl = new JList<String>(st);
    jp = new JScrollPane(jl);

    jp.setBounds(0, 0, 50, 50);
    jl.addListSelectionListener(this);
    add(jp);
  }

  public void valueChanged(ListSelectionEvent e){
    if(!e.getValueIsAdjusting()){ //마우스를 땔때 한번만 실행
      System.out.println(jl.getSelectedValue()); // 선택한것을 보여줌.
    }
  }
}
```

String을 JList에 넣어주고, JList를 JScrollPane에 넣어주면 기본 사용할 준비가 된다.

먼저 `implements ListSelectionListener`를 먼저 선언을 해주면 그다음 class이름에 오류가 뜰 것이다.
`Add unimplements methods`를 클릭해서 `valueChanged`를 오버라이딩 해준다.

그리고 `jl.addListSelectionListener(this)`를 선언을해서 사용가능하게 해준다.

**!e.getValueIsAdjusting()** 는 !는 부정, getValueIsAdjusting은 선택했을때 바로 true값을 리턴해줘서 바로 실행되는 것인데 부정 + 바로실행 = 마우스를 땔때 실행이 되는 것이다.

그리고 안에서 선택된 값을 가져오는 메서드는 `getSelectedValue()` 이다.

<hr>

<h3>요약(조금더 간단한 버전)</h3>

```java
class a extends JPanel implements ListSelectionListener{
  JList a = new JList();
  JScrollPane b = new JScrollPane(a);

  a.addListSelectionListener(this);

  public void valueChanged(ListSelectionEvent e){
    if(!e.getValueIsAdjusting()){
      string st = a.getSelectedValue();
    }
  }
}
```
