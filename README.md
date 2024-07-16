# TaskJ1
import java.util.ArrayList;
import java.util.Scanner;

public class ATM {
    private String accountNumber;
    private String pin;
    private double balance;
    private ArrayList<String> transactionHistory;

    public ATM(String accountNumber, String pin, double initialBalance) {
        this.accountNumber = accountNumber;
        this.pin = pin;
        this.balance = initialBalance;
        this.transactionHistory = new ArrayList<>();
    }

    public void displayMenu() {
        Scanner scanner = new Scanner(System.in);
        int choice;
        do {
            System.out.println("\nATM Menu:");
            System.out.println("1. Account Balance Inquiry");
            System.out.println("2. Cash Withdrawal");
            System.out.println("3. Cash Deposit");
            System.out.println("4. Change PIN");
            System.out.println("5. Transaction History");
            System.out.println("6. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine();
            switch (choice) {
                case 1:
                    checkBalance();
                    break;
                case 2:
                    withdrawCash(scanner);
                    break;
                case 3:
                    depositCash(scanner);
                    break;
                case 4:
                    changePIN(scanner);
                    break;
                case 5:
                    showTransactionHistory();
                    break;
                case 6:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a number between 1 and 6.");
                    break;
            }
        } while (choice != 6);
        scanner.close();
    }

    private void checkBalance() {
        System.out.printf("Your current balance is $%.2f\n", balance);
        transactionHistory.add("Balance inquiry: $" + balance);
    }

    private void withdrawCash(Scanner scanner) {
        System.out.print("Enter the amount to withdraw: ");
        double amount = scanner.nextDouble();
        if (amount > balance) {
            System.out.println("Insufficient balance. Withdrawal cancelled.");
        } else {
            balance -= amount;
            System.out.printf("Withdrawal successful. Remaining balance is $%.2f\n", balance);
            transactionHistory.add("Withdrawal: $" + amount);
        }
    }

    private void depositCash(Scanner scanner) {
        System.out.print("Enter the amount to deposit: ");
        double amount = scanner.nextDouble();
        balance += amount;
        System.out.printf("Deposit successful. Updated balance is $%.2f\n", balance);
        transactionHistory.add("Deposit: $" + amount);
    }

    private void changePIN(Scanner scanner) {
        System.out.print("Enter your current PIN: ");
        String currentPIN = scanner.nextLine();
        if (!currentPIN.equals(pin)) {
            System.out.println("Incorrect PIN. PIN change cancelled.");
            return;
        }
        System.out.print("Enter your new PIN: ");
        String newPIN = scanner.nextLine();
        pin = newPIN;
        System.out.println("PIN changed successfully.");
    }

    private void showTransactionHistory() {
        System.out.println("Transaction History:");
        for (String transaction : transactionHistory) {
            System.out.println(transaction);
        }
    }

    public static void main(String[] args) {
        ATM atm = new ATM("123456789", "1234", 1000.0);
        atm.displayMenu();
    }
}
