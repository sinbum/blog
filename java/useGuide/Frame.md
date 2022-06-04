# 프레임

프레임을 이용하기 위해서는 Frame 클래스 상속 받아야합니다.

자바와 gui의 관련된 개념에 대한 설명은 다음링크를 참조하시기 바랍니다.  

[참고링크 : 너굴너굴 조재연의 프로그래밍](https://raccoonjy.tistory.com/16)

```java
public class MyWindow1 extends Frame
```

## 해당 클래스에 부품 나열  
```java
Button button1;  
Button button2;  
Panel panel;  
```

## 기본적인 설정은 생성자에서 설정  
- 부품 생성, 부품 설정, 부품 조립(add),이벤트 처리(리스너 등록)  
- 부품 생성 : button1=new Button();  
- 부품 설정 : button1.setLabel("버튼1");  
- 부품 조립(add) : panel.add(button1);  
- 이벤트 처리(리스너 등록) :button1.addActionListener(여기에 처리할 위치가 있음);  

## 리스너 등록하는 방법 (3가지)

1. 자기자신의 클래스 이용(this)  
button1.addActionListener(this);  
자기자신 클래스에 리스너를 implements해야함  
public class MyWindow1 extends Frame implements WindowListener  

2. 새로운 클래스를 만들어 이용(new ActionLinst())  
ActionListenProc ap=new ActionListenProc(button1,button2);  
button1.addActionListener(ap);  
새로운 클래스는 리스너를 implements해야함

4. 익명함수 이용  
  ```java
  button1.addActionListener(new ActionListener() {  
    public void actionPerformed(ActionEvent e) {
      System.out.println(e.getSource());
    }
  }); 
  ```

## 레이아웃의 설정
setLayout(layout유형);
layout유형은 다음의 유형들과 같습니다.  

- new FlowLayout()
- new BorderLayout()
- new CardLayout()
- new GridLayout()

> SungjukFrame.java - 기본사항 코딩

```
package StudentManagerProject;

import java.awt.Button;
import java.awt.Color;
import java.awt.Frame;
import java.awt.GridLayout;
import java.awt.Label;
import java.awt.Panel;
import java.awt.TextField;
import java.awt.event.WindowEvent;
import java.awt.event.WindowListener;

public class SungjukFrame extends Frame implements WindowListener{

Label idLabel,nameLabel,hpLabel;
TextField idTextField,nameTextField,hpTextField;
Button confirmButton;
Panel infoInputPanel;

public SungjukFrame() {
	idLabel=new Label("학번");
	nameLabel=new Label("이름");
	hpLabel=new Label("전화번호");

	idTextField=new TextField(10);
	nameTextField=new TextField(10);
	hpTextField=new TextField(10);

	confirmButton=new Button("확인");
	infoInputPanel=new Panel();

	infoInputPanel.setLayout(new GridLayout(4,2,10,10));
	infoInputPanel.add(idLabel);
	infoInputPanel.add(idTextField);
	infoInputPanel.add(nameLabel);
	infoInputPanel.add(nameTextField);
	infoInputPanel.add(hpLabel);
	infoInputPanel.add(hpTextField);
	infoInputPanel.add(confirmButton);

	add(infoInputPanel);

	idLabel.setAlignment(Label.CENTER);
	nameLabel.setAlignment(Label.CENTER);
	hpLabel.setAlignment(Label.CENTER);

	infoInputPanel.setBackground(Color.yellow);

	setBounds(100,100,500,200);
	setVisible(true);

	//리스너 등록
	addWindowListener(this);

}

@Override
public void windowOpened(WindowEvent e) {
	// TODO Auto-generated method stub

}

@Override
public void windowClosing(WindowEvent e) {
	System.exit(0);

}

@Override
public void windowClosed(WindowEvent e) {
	// TODO Auto-generated method stub

}

@Override
public void windowIconified(WindowEvent e) {
	// TODO Auto-generated method stub

}

@Override
public void windowDeiconified(WindowEvent e) {
	// TODO Auto-generated method stub

}

@Override
public void windowActivated(WindowEvent e) {
	// TODO Auto-generated method stub

}

@Override
public void windowDeactivated(WindowEvent e) {
	// TODO Auto-generated method stub

}


}
```
