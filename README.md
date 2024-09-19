import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.time.LocalDate;
import java.time.Period;
import java.time.format.DateTimeFormatter;

public class AgeCalculatorApp {
    public static void main(String[] args) {
        // Create a JFrame for the application window
        JFrame frame = new JFrame("Age Calculator");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 200);

        // Create a JPanel to hold the components
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(3, 2));

        // Add label and text field for birthdate input
        JLabel birthdateLabel = new JLabel("Enter your birthdate (yyyy-mm-dd): ");
        JTextField birthdateField = new JTextField();

        // Add button to calculate age
        JButton calculateButton = new JButton("Calculate Age");

        // Add a label to display the result (user's age)
        JLabel resultLabel = new JLabel("Your age is: ");

        // Add components to the panel
        panel.add(birthdateLabel);
        panel.add(birthdateField);
        panel.add(calculateButton);
        panel.add(resultLabel);

        // Add ActionListener to calculate the age when the button is clicked
        calculateButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String birthdateStr = birthdateField.getText();
                DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");

                try {
                    // Parse the input birthdate
                    LocalDate birthdate = LocalDate.parse(birthdateStr, formatter);
                    LocalDate currentDate = LocalDate.now();

                    // Calculate the age
                    Period age = Period.between(birthdate, currentDate);

                    // Display the age in the result label
                    resultLabel.setText("Your age is: " + age.getYears() + " years");
                } catch (Exception ex) {
                    resultLabel.setText("Invalid date format. Please use yyyy-mm-dd.");
                }
            }
        });

        // Add the panel to the frame and make it visible
        frame.add(panel);
        frame.setVisible(true);
    }
}
