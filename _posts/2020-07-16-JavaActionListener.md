---

layout : posts

title : "자바 URL에 연결해서 이미지 얻어오기"

date : 2020-07-14

categoris : java

---


자바 프로젝트를 하면서 가장 많이 쓰는 기능 중 하나인 `ActionListener`에 대해서 설명을 해보겠습니다.

**ActionListener**
: ActionListener는 어떤 이벤트가 일어났을 때 캐치할 수 있도록 도와주는 것입니다.

그러면 바로 코드를 보여드리고 설명을 하겠습니다

```java
 class Action extends JPanel implements ActionListener{
   JButton a = new JButton();
   setLayout(null);

   ad.setBounds(0,0,50,50); //0, 0부터 50의 크기씩 가지겠다.

   a.addActionListener(this);

   add(a);

   public void actionPerformed(ActionEvent e){
     if(e.getSource.equals(a)){ //얻은 정보가 버튼 a와 같으면
       a.setText("버튼이 눌려짐");
     }
   }
 }
```

ActionListener를 사용하기 위해서는 implements로 가져와야 합니다.

**상속(extends)** 은 하나만 가지고 올수 있지만, **인터페이스( implements)** 는 여러개를 상속 받아 올수 있기 때문에 `ActionListener` 뿐만 아니라 `ListSelectionListener` 같은 것도 같이 가져올수 있습니다. 

그리고 JButton을 눌려졌을때 액션을 받아와야 하기 때문에 꼭!! **addActionListener** 를 적어주셔야 합니다.

적지 않으면 아무일도 일어나지 않습니다.

implements를 하는 순간 Action(class 이름)에서 오류가 날것입니다.
그때 `Add unimplements methods` 를 클릭해 `actionPerformed`를 생성해주시고
그안에 원하는 기능을 넣으시면 됩니다.

어떤 버튼과 눌려졌는지 비교하고 싶을땐 `e.getSource`를 이용해 위의 코드와 똑같이 적어주시면 됩니다.

<hr>

<h3>요약</h3>

```java
class a extends JPanel implements ActionListener{
  JButton b = new JButton();
  b.addActionListener(this);

  public void actionPerformed(ActionEvent e){

  }
}
```
