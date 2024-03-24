Company Financial Management System
import java.util.ArrayList;
import java.util.Scanner;

class Transaction {
    private String description;
    private double amount;

    public Transaction(String description, double amount) {
        this.description = description;
        this.amount = amount;
    }

    public String getDescription() {
        return description;
    }

    public double getAmount() {
        return amount;
    }
}

class FinanceManager {
    private ArrayList<Transaction> transactions;

    public FinanceManager() {
        this.transactions = new ArrayList<>();
    }

    public void recordIncome(String description, double amount) {
        transactions.add(new Transaction(description, amount));
    }

    public void recordExpense(String description, double amount) {
        transactions.add(new Transaction(description, -amount));
    }

    public double getTotalIncome() {
        double totalIncome = 0;
        for (Transaction transaction : transactions) {
            if (transaction.getAmount() > 0) {
                totalIncome += transaction.getAmount();
            }
        }
        return totalIncome;
    }

    public double getTotalExpense() {
        double totalExpense = 0;
        for (Transaction transaction : transactions) {
            if (transaction.getAmount() < 0) {
                totalExpense += Math.abs(transaction.getAmount());
            }
        }
        return totalExpense;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        FinanceManager financeManager = new FinanceManager();

        System.out.println("Company Financial Management System");
        System.out.println("1. Record Income");
        System.out.println("2. Record Expense");
        System.out.println("3. Display Total Income");
        System.out.println("4. Display Total Expense");
        System.out.println("5. Exit");

        int choice;
        do {
            System.out.print("\nEnter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // consume the newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter income description: ");
                    String incomeDescription = scanner.nextLine();
                    System.out.print("Enter income amount: ");
                    double incomeAmount = scanner.nextDouble();
                    scanner.nextLine(); // consume the newline character
                    financeManager.recordIncome(incomeDescription, incomeAmount);
                    System.out.println("Income recorded successfully.");
                    break;
                case 2:
                    System.out.print("Enter expense description: ");
                    String expenseDescription = scanner.nextLine();
                    System.out.print("Enter expense amount: ");
                    double expenseAmount = scanner.nextDouble();
                    scanner.nextLine(); // consume the newline character
                    financeManager.recordExpense(expenseDescription, expenseAmount);
                    System.out.println("Expense recorded successfully.");
                    break;
                case 3:
                    System.out.println("Total Income: $" + financeManager.getTotalIncome());
                    break;
                case 4:
                    System.out.println("Total Expense: $" + financeManager.getTotalExpense());
                    break;
                case 5:
                    System.out.println("Exiting the program.");
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a valid option.");
            }
        } while (choice != 5);

        scanner.close();
    }
}
