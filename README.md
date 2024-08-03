# techwithclan
For my techwithclan cohort 2 backend development track assignments
class BankAccount:
    def __init__(self, account_number, initial_balance=0):
        self.account_number = account_number
        self.balance = initial_balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Deposited {amount:.2f} into account {self.account_number}. New balance: {self.balance:.2f}")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if amount > 0 and amount <= self.balance:
            self.balance -= amount
            print(f"Withdrew {amount:.2f} from account {self.account_number}. New balance: {self.balance:.2f}")
        else:
            print("Insufficient funds or invalid withdrawal amount.")

    def transfer(self, recipient_account, amount):
        if amount > 0 and amount <= self.balance:
            self.balance -= amount
            recipient_account.balance += amount
            print(f"Transferred {amount:.2f} from account {self.account_number} to account {recipient_account.account_number}")
        else:
            print("Insufficient funds or invalid transfer amount.")

    def check_balance(self):
        print(f"Account {self.account_number} balance: {self.balance:.2f}")

def main():
    accounts = {}  # Dictionary to store accounts

    while True:
        print("\nUSSD Banking Menu:")
        print("1. Deposit")
        print("2. Transfer")
        print("3. Withdraw")
        print("4. Check Balance")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            account_number = input("Enter your account number: ")
            amount = float(input("Enter deposit amount: "))
            if account_number in accounts:
                accounts[account_number].deposit(amount)
            else:
                print("Account not found.")
        elif choice == "2":
            sender_account = input("Enter your account number: ")
            recipient_account = input("Enter recipient's account number: ")
            amount = float(input("Enter transfer amount: "))
            if sender_account in accounts and recipient_account in accounts:
                accounts[sender_account].transfer(accounts[recipient_account], amount)
            else:
                print("Invalid account numbers.")
        elif choice == "3":
            account_number = input("Enter your account number: ")
            amount = float(input("Enter withdrawal amount: "))
            if account_number in accounts:
                accounts[account_number].withdraw(amount)
            else:
                print("Account not found.")
        elif choice == "4":
            account_number = input("Enter your account number: ")
            if account_number in accounts:
                accounts[account_number].check_balance()
            else:
                print("Account not found.")
        elif choice == "5":
            print("Thank you for using the USSD banking service.")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
    
