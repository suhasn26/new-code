import java.util.HashMap;
import java.util.Map;

public class BankService {

    private final Map<Integer, BankAccount> accounts = new HashMap<>();

    public void createAccount(int accountNumber, double initialBalance) {
        accounts.put(accountNumber, new BankAccount(accountNumber, initialBalance));
    }

    public void deposit(int accountNumber, double amount) {
        BankAccount account = accounts.get(accountNumber);
        account.deposit(amount);
        TransactionLogger.log("Deposited " + amount + " to account " + accountNumber);
    }

    public void withdraw(int accountNumber, double amount) {
        BankAccount account = accounts.get(accountNumber);
        try {
            account.withdraw(amount);
            TransactionLogger.log("Withdrawn " + amount + " from account " + accountNumber);
        } catch (InsufficientBalanceException e) {
            TransactionLogger.log("Failed withdrawal from account " + accountNumber);
            System.out.println(e.getMessage());
        }
    }

    public void displayBalance(int accountNumber) {
        System.out.println("Balance: " + accounts.get(accountNumber).getBalance());
    }
}
