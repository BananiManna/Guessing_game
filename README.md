/*It is a number guessing game the system involves following-
1. The system generates a random number from a given range, say 1 to 100.
2. The user is prompted to enter their given number in a displayed dialogue box.
3. The computer then tells if the entered number matches the guesses number or it is
 higher/lower than the generated number.
4. The game continues under the user guessing the number.
 */
//CBTCIP
import javax.swing.*;
import java.util.Random;
public class NumberGuessingGame {
    public static void main(String[] args) {
        Random random = new Random();
        int lowerBound = 1;
        int upperBound = 100;
        int generatedNumber = random.nextInt(upperBound - lowerBound + 1) + lowerBound;
        int maxAttempts = 10;
        int attempts = 0;
        int score = 100;
        JOptionPane.showMessageDialog(null, "Welcome to the Number Guessing Game!\nI've selected a random number between " + lowerBound + " and " + upperBound + ". Try to guess it.");
        while (attempts < maxAttempts) {
            String userGuessString = JOptionPane.showInputDialog("Enter your guess:");
            // Handle cancel or empty input
            if (userGuessString == null || userGuessString.trim().isEmpty()) {
                JOptionPane.showMessageDialog(null, "Invalid input. Please enter a number.");
                continue;
            }
            try {
                int userGuess = Integer.parseInt(userGuessString);
                attempts++;
                if (userGuess == generatedNumber) {
                    JOptionPane.showMessageDialog(null, "Congratulations! You guessed the correct number in " + attempts + " attempts.\nYour score is: " + score);
                    break;
                } else {
                    String message = "Incorrect guess.\n";
                    if (userGuess < generatedNumber) {
                        message += "Try a higher number.";
                    } else {
                        message += "Try a lower number.";
                    }
                    int difference = Math.abs(generatedNumber - userGuess);
                    score -= (difference * 50 + attempts * 50);
                    message += "\nAttempts left: " + (maxAttempts - attempts);
                    JOptionPane.showMessageDialog(null, message);
                }
            } catch (NumberFormatException e) {
                JOptionPane.showMessageDialog(null, "Invalid input. Please enter a valid number.");
            }
        }
        if (attempts == maxAttempts) {
            JOptionPane.showMessageDialog(null, "Sorry, you've run out of attempts. Better luck next time!! The correct number was: " + generatedNumber + "\nYour final score is: " + score);
        }
    }
}
