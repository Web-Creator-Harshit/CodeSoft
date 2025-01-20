import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class Game extends JFrame
{
    JTextField guess, bestscore, totalguess;
    JButton giveupbutton,playagainbutton,guessbutton;
    ButtonListener buttonListener;
    ButtonListener2 buttonListener2;
    ButtonListener3 buttonListener3;
    JLabel inputlabel,guesslabel,trylabel,bestscorelabel,totalguesslabel;

    int rand=(int) (Math.random()*100);
    int count=0;
    public Game()
    {
        Container c = getContentPane();
        c.setLayout(null);
        c.setBackground(Color.CYAN);

        guesslabel = new JLabel("*******Guess the Number*******");
        guesslabel.setForeground(Color.PINK);
        guesslabel.setFont(new Font("times new roman",Font.BOLD,36));
        guesslabel.setBounds(450,0,600,100);


        inputlabel=new JLabel("Enter a number between 1-100");
        inputlabel.setFont(new Font("Comic Sans MS",Font.PLAIN,18));
        inputlabel.setBounds(600,80,400,100);

        trylabel = new JLabel("You Have To Try Atleast Once");
        trylabel.setFont(new Font("Comic Sans MS",Font.PLAIN,16));
        trylabel.setBounds(620,200,400,100);

        guess = new JTextField(10);
        guess.setBounds(650,160,100,60);
        guess.setBackground(Color.PINK);


        bestscore = new JTextField(10);
        bestscore.setBounds(800,160,50,25);

        bestscorelabel = new JLabel(" Your Score");
        bestscorelabel.setFont(new Font("Comic Sans MS",Font.PLAIN,14));
        bestscorelabel.setBounds(860,160,300,25);

        totalguess = new JTextField(10);
        totalguess.setBounds(800,190,50,25);


        totalguesslabel = new JLabel("Guesses Count");
        totalguesslabel .setFont(new Font("Comic Sans MS",Font.PLAIN,14));
        totalguesslabel.setBounds(860,190,300,25);

        guessbutton =new JButton("Check Your Guess");
        guessbutton.setBounds(630,280,200,50);
        guessbutton.setBackground(Color.LIGHT_GRAY);
        buttonListener = new ButtonListener();
        guessbutton.addActionListener(buttonListener);


        giveupbutton = new JButton("Give up!");
        giveupbutton.setBounds(510,360,200,50);
        giveupbutton.setBackground(Color.LIGHT_GRAY);
        buttonListener2 = new ButtonListener2();
        giveupbutton.addActionListener(buttonListener2);

        playagainbutton = new JButton("Play Again!");
        playagainbutton.setBounds(750,360,200,50);
        playagainbutton.setBackground(Color.LIGHT_GRAY);
        buttonListener3 = new ButtonListener3();
        playagainbutton.addActionListener(buttonListener3);


        c.add(guesslabel);
        c.add(inputlabel);
        c.add(trylabel);
        c.add(guess);
        c.add(bestscore);
        c.add(bestscorelabel);
        c.add(totalguess);
        c.add(totalguesslabel);
        c.add(guessbutton);
        c.add(giveupbutton);
        c.add(playagainbutton);

        
        bestscore.setEditable(false);
        totalguess.setEditable(false);
        setTitle("GUESS THE NUMBER");
        setSize(1600,1000);
        setVisible(true);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
    }
        class ButtonListener implements ActionListener
    {
        int bestScore=100;
        public void actionPerformed(ActionEvent e)
        { 
            int a = Integer.parseInt(guess.getText());
            count=count+1;
            if(a<rand)
            {
                JOptionPane.showMessageDialog(guessbutton,a+"\t \t"+": Number Is low, Try Again","Try Again",0);
            }
            else if(a>rand)
            {
                JOptionPane.showMessageDialog(guessbutton,a+"\t \t"+": Number Is High, Try Again","Try again",0);
            }
            else
            {
                JOptionPane.showMessageDialog(guessbutton,"Congratulations"+"\n"+"You Won"+"\n"+"Your Guess is Correct :"+"\t \t"+rand,"GAME OVER",0);
                if(count<bestScore)
                {
                    bestScore=count;
                    bestscore.setText(bestScore+"");
                }
                else {
                    bestscore.setText("" + bestScore);
                }
                guess.setEditable(false);
            }

            guess.requestFocus();
            guess.selectAll();
            totalguess.setText(count+"");
        }
    }
    class ButtonListener2 implements ActionListener
    {
        public void actionPerformed(ActionEvent e)
        {
            totalguess.setText("");
            JOptionPane.showMessageDialog(giveupbutton,"The correct answer is : "+rand+"!!","GAME OVER",0);
            guess.setText("");
            guess.setEditable(false);
        }
    }

    class ButtonListener3 implements ActionListener
    {
        public void actionPerformed(ActionEvent e)
        {
            rand=(int) (Math.random()*100);
            guess.setText("");
            totalguess.setText("");
            JOptionPane.showMessageDialog(playagainbutton,"*****RESTARTED*****","START",0);
            totalguess.setText("");
            count=0;
            guess.setEditable(true);
            guess.requestFocus();
        }
    }
    public static void main(String[] args)
    {
        new Game();
    }
}
