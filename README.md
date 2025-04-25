import javax.swing.*;
import java.awt.*;
import java.text.SimpleDateFormat;
import java.util.Date;

public class MultiFormatClock extends JFrame {
    private JLabel clockLabel;
    private JButton format24Button, format12Button, oClockButton, dateButton;
    private String currentFormat = "HH:mm:ss"; // Default: 24-hour

    public MultiFormatClock() {
        setTitle("Multi-Format Digital Clock");
        setSize(400, 200);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(new BorderLayout());

        // Clock Label
        clockLabel = new JLabel();
        clockLabel.setFont(new Font("Consolas", Font.BOLD, 32));
        clockLabel.setHorizontalAlignment(SwingConstants.CENTER);
        clockLabel.setForeground(Color.CYAN);
        clockLabel.setBackground(Color.BLACK);
        clockLabel.setOpaque(true);
        add(clockLabel, BorderLayout.CENTER);

        // Buttons Panel
        JPanel buttonPanel = new JPanel(new FlowLayout());
        format24Button = new JButton("24-Hour");
        format12Button = new JButton("12-Hour");
        oClockButton = new JButton("O'Clock");
        dateButton = new JButton("Date");

        buttonPanel.add(format24Button);
        buttonPanel.add(format12Button);
        buttonPanel.add(oClockButton);
        buttonPanel.add(dateButton);
        add(buttonPanel, BorderLayout.SOUTH);

        // Button Actions
        format24Button.addActionListener(e -> currentFormat = "HH:mm:ss");
        format12Button.addActionListener(e -> currentFormat = "hh:mm:ss a");
        oClockButton.addActionListener(e -> currentFormat = "h 'O''Clock'");
        dateButton.addActionListener(e -> currentFormat = "EEE, dd MMM yyyy");

        // Start Clock
        runClock();
        setVisible(true);
    }

    private void runClock() {
        Timer timer = new Timer(1000, e -> {
            SimpleDateFormat formatter = new SimpleDateFormat(currentFormat);
            String time = formatter.format(new Date());
            clockLabel.setText(time);
        });
        timer.start();
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(MultiFormatClock::new);
    }
}
