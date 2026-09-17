# canteen.java
import java.util.Scanner;

public class Canteen {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Menu items and prices
        String[] menuItems = {"Burger", "Pizza", "Pasta", "Sandwich", "Milk Tea"};
        double[] prices = {80.00, 120.00, 100.00, 70.00, 90.00};

        int totalQuantity = 0;
        double totalBeforeDiscount = 0.0;
        double totalDiscount = 0.0;

        char orderAgain = 'Y';

        while (orderAgain == 'Y' || orderAgain == 'y') {
            // Display Menu
            System.out.println("===== MENU =====");
            for (int i = 0; i < menuItems.length; i++) {
                System.out.printf("%d. %-10s $%.2f%n", (i + 1), menuItems[i], prices[i]);
            }
            System.out.println();

            // Prompt item number
            System.out.print("Enter item number: ");
            if (!scanner.hasNextInt()) {
                System.out.println("Invalid order! Please enter a valid item and quantity.\n");
                scanner.next(); // Clear invalid input
                System.out.print("Do you want to order again? (Y/N): ");
                orderAgain = scanner.next().charAt(0);
                System.out.println();
                continue;
            }
            int itemNum = scanner.nextInt();

            // Prompt quantity
            System.out.print("Enter quantity: ");
            if (!scanner.hasNextInt()) {
                System.out.println("Invalid order! Please enter a valid item and quantity.\n");
                scanner.next(); // Clear invalid input
                System.out.print("Do you want to order again? (Y/N): ");
                orderAgain = scanner.next().charAt(0);
                System.out.println();
                continue;
            }
            int quantity = scanner.nextInt();

            // Validate item selection and quantity
            if (itemNum < 1 || itemNum > 5 || quantity < 1 || quantity > 10) {
                System.out.println("Invalid order! Please enter a valid item and quantity.");
                System.out.print("Do you want to order again? (Y/N): ");
                orderAgain = scanner.next().charAt(0);
                System.out.println();
                continue;
            }

            // Prompt student status
            System.out.print("Are you a student? (Y/N): ");
            char studentChar = scanner.next().charAt(0);
            boolean isStudent = (studentChar == 'Y' || studentChar == 'y');

            // Calculation for current order
            double itemPrice = prices[itemNum - 1];
            double subtotal = itemPrice * quantity;

            // Determine discount rate
            double discountRate = 0.0;
            if (isStudent && subtotal >= 500.0) {
                discountRate = 0.15;
            } else if (isStudent) {
                discountRate = 0.10;
            } else if (subtotal >= 500.0) {
                discountRate = 0.05;
            }

            double discountAmount = subtotal * discountRate;
            double orderTotal = subtotal - discountAmount;

            // Display current order details
            System.out.printf("Subtotal: $%.2f%n", subtotal);
            System.out.printf("Discount: $%.2f%n", discountAmount);
            System.out.printf("Order total: $%.2f%n", orderTotal);

            // Accumulate totals
            totalQuantity += quantity;
            totalBeforeDiscount += subtotal;
            totalDiscount += discountAmount;

            // Prompt to order again
            System.out.print("Do you want to order again? (Y/N): ");
            orderAgain = scanner.next().charAt(0);
            System.out.println();
        }

        // Display Final Order Summary
        System.out.println("===== ORDER SUMMARY =====");
        System.out.println("Total items: " + totalQuantity);
        System.out.printf("Total before discount: $%.2f%n", totalBeforeDiscount);
        System.out.printf("Total discount: $%.2f%n", totalDiscount);
        System.out.printf("Final amount: $%.2f%n", (totalBeforeDiscount - totalDiscount));
        System.out.println("Thank you for ordering!");

        scanner.close();
    }
}
