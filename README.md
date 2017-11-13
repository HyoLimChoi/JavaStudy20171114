package Question01;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Container;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.ItemEvent;
import java.awt.event.ItemListener;

import javax.swing.ButtonGroup;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JRadioButton;
import javax.swing.JTextField;

public class OrderPizza extends JFrame {

	
	JLabel welcom = new JLabel("자바 피자에 오신것을 환영합니다.");
	JLabel line = new JLabel("****************************************************************");
	
	JLabel type=new JLabel("종류");
	JLabel topping=new JLabel("추가토핑");
	JLabel pizzasize=new JLabel("크기");
	
	JRadioButton[] orderBy1 = new JRadioButton[3] ;
	JRadioButton[] orderBy2 = new JRadioButton[4] ;
	JRadioButton[] orderBy3 = new JRadioButton[3] ;
	
	String[] orderBy1text={"콤보 100원","포테이토 200원","불고기 300원"};
	String[] orderBy2text={"피망 400원","치즈 500원","페페로니 600원","베이컨 700원"};
	String[] orderBy3text={"Small 1000원","Medium 5000원","Large 10000원"};
	
	JButton calc = new JButton("계산");
	JButton cancel = new JButton("취소");	
	JTextField moneyResult = new JTextField("                ");
	
	int result=0;
	public OrderPizza() {
		
		super("피자 주문");
		setVisible(true);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setSize(380, 300);
		setLayout(new BorderLayout(5,5));
		
		/*상단 타이틀 부분*/
		add(new Title(),BorderLayout.NORTH);		
		
		/*중간 선택 부분*/
		add(new Type(),BorderLayout.WEST);
		add(new AddTopping(),BorderLayout.CENTER);
		add(new Size(),BorderLayout.EAST);   
		
		/*하단 결과 부분*/
		add(new resultCalc(),BorderLayout.SOUTH);
	}

	
	class Title extends JPanel{
		public Title() {			
			setLayout(new GridLayout(2, 0,0,5));
			welcom.setFont(new Font("고딕체", Font.BOLD,20));
			welcom.setHorizontalAlignment(JLabel.CENTER);
			add(welcom);
			
			line.setHorizontalAlignment(JLabel.CENTER);
			add(line);

		}
	}//end of Title
	
	
	class Type extends JPanel{
		public Type() {		
			
			setLayout(new GridLayout(4, 0));
		
			type.setForeground(Color.RED);
			type.setFont(new Font("굴림체", Font.BOLD,12));
			add(type);
			
			
			ButtonGroup g = new ButtonGroup();
			for(int i=0;i<orderBy1.length;i++) {
				orderBy1[i]=new JRadioButton(orderBy1text[i]);
				g.add(orderBy1[i]);
				add(orderBy1[i]);
				orderBy1[i].addItemListener(new ItemListener() {	
					public void itemStateChanged(ItemEvent e) {
						if(e.getStateChange() == 
								ItemEvent.DESELECTED)
								return;
							if(orderBy1[0].isSelected()) 
								result+=100;
							else if(orderBy1[1].isSelected()) 
								result+=200;
							else
								result+=300;						
					}
				});
			}
		}
		
	}//end of Type
	
	class AddTopping extends JPanel{
		public AddTopping() {
			
			setLayout(new GridLayout(5, 0));
		
			topping.setForeground(Color.RED);
			topping.setFont(new Font("굴림체", Font.BOLD,12));
			add(topping);
			
			
			ButtonGroup g = new ButtonGroup();
			for(int i=0;i<orderBy2.length;i++) {
				orderBy2[i]=new JRadioButton(orderBy2text[i]);
				g.add(orderBy2[i]);
				add(orderBy2[i]);
				orderBy2[i].addItemListener(new ItemListener() {	
					public void itemStateChanged(ItemEvent e) {
						if(e.getStateChange() == 
								ItemEvent.DESELECTED)
								return;
							if(orderBy2[0].isSelected()) 
								result+=400;
							else if(orderBy2[1].isSelected()) 
								result+=500;
							else if(orderBy2[2].isSelected()) 
								result+=600;	
							else
								result+=700;	
					}
				});
			}
		}
	}//end of AddTopping
	
	class Size extends JPanel{
		public Size() {
			setLayout(new GridLayout(5, 0));		
			pizzasize.setForeground(Color.RED);
			pizzasize.setFont(new Font("굴림체", Font.BOLD,12));
			add(pizzasize);
			
			
			ButtonGroup g = new ButtonGroup();
			for(int i=0;i<orderBy3.length;i++) {
				orderBy3[i]=new JRadioButton(orderBy3text[i]);
				g.add(orderBy3[i]);
				add(orderBy3[i]);
				orderBy3[i].addItemListener(new ItemListener() {	
					public void itemStateChanged(ItemEvent e) {
						if(e.getStateChange() == 
								ItemEvent.DESELECTED)
								return;
							if(orderBy3[0].isSelected()) 
								result+=1000;
							else if(orderBy3[1].isSelected()) 
								result+=5000;
							else 
								result+=10000;	
				
					}
				});
			}
		}
	}//end of Size
	
	
	class resultCalc extends JPanel{
		public resultCalc() {
		
			add(calc);			
			calc.addActionListener(new ActionListener() {				
				@Override
				public void actionPerformed(ActionEvent e) {
					moneyResult.setText(Integer.toString(result));
					
				}
			});
			
			cancel.addActionListener(new ActionListener() {				
				@Override
				public void actionPerformed(ActionEvent e) {
					result=0;
					moneyResult.setText(" ");
					
					for(int i=0;i<3;i++)
					{
						
						orderBy1[i].setSelected(false);
						orderBy2[i].setSelected(false);
						orderBy3[i].setSelected(false);
					}
				}
			});
			add(cancel);
			
			
			moneyResult.setEnabled(false); //피자가격 직접입력 불가
			add(moneyResult);
		}
	}//end of resultCalc
	
	
	public static void main(String[] args) {
		new OrderPizza();	
	}//end of main

	
}//end of OrderPizza
