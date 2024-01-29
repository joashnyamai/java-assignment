import java.util.Scanner;
import java.io.Console;

public class LoginSystem {

    public static void main(String[] args) {
        // Initialize Scanner and Console classes
        Scanner scanner = new Scanner(System.in);
        Console console = System.console();
        int attempts = 0; // Counter for the number of login attempts

        // Hardcoded correct username and password for validation
        final String CORRECT_USERNAME = "user"; // Replace with actual username
        final String CORRECT_PASSWORD = "pass"; // Replace with actual password

        // Loop allows up to 3 attempts for user login
        while (attempts < 3) {
            System.out.print("Enter Username: ");
            String username = scanner.nextLine(); // Read username input

            // Read password input, masking if Console is available (terminal)
            // Otherwise, password will not be masked (IDE console)
            char[] passwordArray = console == null ? new char[0] : console.readPassword("Enter Password: ");
            String password = new String(passwordArray);

            // Validate username and password
            if (login(username, password, CORRECT_USERNAME, CORRECT_PASSWORD)) {
                System.out.println("Login successful!");
                break; // Exit loop on successful login
            } else {
                System.out.println("Incorrect username or password.");
                attempts++; // Increment attempt counter
            }

            // Check if maximum attempts reached
            if (attempts == 3) {
                System.out.println("Login failed. No more attempts allowed.");
            }
        }

        scanner.close(); // Close Scanner to prevent resource leak
    }

    /**
     * Method to check if the provided credentials match the correct ones.
     *
     * @param username The entered username
     * @param password The entered password
     * @param correctUsername The correct username
     * @param correctPassword The correct password
     * @return true if credentials are correct, false otherwise
     */
    private static boolean login(String username, String password, String correctUsername, String correctPassword) {
        return username.equals(correctUsername) && password.equals(correctPassword);
    }
}
