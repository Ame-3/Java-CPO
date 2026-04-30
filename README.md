import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
public class Calculator {
    JFrame frame;
    JTextField textField;
    double num1, num2, result;
    char operator;
    public Calculator() {
        frame = new JFrame("Calculator");
        frame.setSize(300, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());
        textField = new JTextField();
        textField.setFont(new Font("Arial", Font.BOLD, 20));
        frame.add(textField, BorderLayout.NORTH);
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(4, 4));
        String[] buttons = {
            "1","2","3","+",
            "4","5","6","-",
            "7","8","9","*",
            "C","0","=","/"
        };
        for (String text : buttons) {
            JButton btn = new JButton(text);
            panel.add(btn);
            btn.addActionListener(e -> {
                String value = btn.getText();
                if (value.matches("[0-9]")) {
                    textField.setText(textField.getText() + value);
                } else if (value.equals("C")) {
                    textField.setText("");
                } else if (value.equals("=")) {
                    num2 = Double.parseDouble(textField.getText());
                    switch (operator) {
                        case '+': result = num1 + num2; break;
                        case '-': result = num1 - num2; break;
                        case '*': result = num1 * num2; break;
                        case '/': result = num1 / num2; break;
                    }
                    textField.setText(String.valueOf(result));
                } else {
                    num1 = Double.parseDouble(textField.getText());
                    operator = value.charAt(0);
                    textField.setText("");
                }
            });
        }
        frame.add(panel, BorderLayout.CENTER);
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        new Calculator();
    }
}
