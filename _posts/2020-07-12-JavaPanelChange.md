---

layout : posts

title : "자바 스윙 패널을 통한 화면전환" 

date : 2020-07-12

categoris : Blog

--- 

학원에서 일주일 프로젝트를 하게되었을때 화면전환에 대해 많은 고민을 한적이 있다.  
  

그때 썼던 코드는` dispose()`를 통해 화면을 닫고 새로여는 방식이였는데   
지금 개인 프로젝트를 하면서 더 좋은 것을 알게 되었다.  
그것은 바로 **panel을 통한 화면전환 방식** 이다.  
바로 코드부터 보여드릴려고 한다.  
```java
public class ControlTower extends JFrame{
	public String panelName = null;
	
	//화면들
	FirstUI firstUi;
	TicketingUI ticketUi;
	
	ControlTower(){
		list = admini.selectMovie();
		thList = thAdmini.selectTheater();

	}
	
	public void changePanel(String panelName) {
		if(panelName == "firstUi") {
			getContentPane().removeAll();
			getContentPane().add(firstUi);
			revalidate();
			repaint();
		}else if(panelName == "ticketUi"){
			getContentPane().removeAll();
			getContentPane().add(ticketUi);
			revalidate();
			repaint();
		}
	}
}

```

하나의 컨트롤 타워를 만들고 컨트롤타워에서 패널들을 만들어준다.  
  
new는 main에서 생성을해서 관리하도록하고 컨트롤타워는 모든 클래스에서 사용할 수있도록 메인에서 뿌려준다.  
  
다른 클래스에서 사용할땐 panelName = firstUi 이런식으로 바꿔주게 되면 화면이 전환되게 되는 것이다.  
  
그럼 바로 메인코드로 가보자.  


```java	
public static void main(String[] args) {
		ControlTower ct = new ControlTower();
		ct.firstUi = new FirstUI(ct);
		ct.ticketUi = new TicketingUI(ct);
		
		ct.add(ct.ticketUi);
		
		ct.setTitle("영화예매");
		ct.setSize(1200, 900);
		ct.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		ct.setVisible(true);
		ct.setLocationRelativeTo(null);
	}

```
  
메인에서는 new를 통해 주소값을 생성하고 컨트롤타워(패널변경)의 권한을 넘겨준다.  
  
`ct.add`는 첫화면에서 보여줄것을 넣는것이다.  
  
조금 더 보충설명을 위해 다음코드도 적어본다.  


```java
class FirstUI extends JPanel implements ActionListener{
	ControlTower ct;
	JButton ticketing;

	FirstUI(ControlTower ct){
		this.ct = ct;
		setLayout(null);
		JLabel ad = new JLabel(new ImageIcon("./images/ad.jpg")); //광고
		ad.setBounds(50, 30, 1100, 400);
		
		ticketing = new JButton("예매하기");
		ticketing.setBounds(50, 450, 550, 350);
		
		JButton checking = new JButton();
		checking.setBounds(600, 450, 550, 350);

		add(ad);
		add(checking);
		add(ticketing);
		
		ticketing.addActionListener(this);

	}

	@Override
	public void actionPerformed(ActionEvent e) {
		if(e.getSource().equals(ticketing)) {
			ct.changePanel("ticketUi");
		}
	}
}
```

액션리스너를 통해 `actionPerformed`에 들어오게 되면 `e.getSource`로 어떤 액션에서 받아왔는지 확인하고 
  
그확인한것이 `equal`을 통해 ticketing과 비교해서 맞으면 if문 안으로 들어와 ct(컨트롤타워)에 있는 `panelName`의 이름을 바꿔주는 것이다.  
   
참고로 changePanel은 패널을 바꾸기위한 내가 만든 메서드이다.




