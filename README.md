#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to represent a bank account
struct BankAccount {
    char name[50];
    int accountNumber;
    float balance;
};

// Function to create a new bank account
struct BankAccount createAccount() {
    struct BankAccount account;
    printf("Enter account holder's name: ");
    scanf("%s", account.name);
    printf("Enter account number: ");
    scanf("%d", &account.accountNumber);
    account.balance = 0.0;
    return account;
}

// Function to deposit money into an account
void deposit(struct BankAccount *account, float amount) {
    account->balance += amount;
    printf("Deposited %.2f into account %d.\n", amount, account->accountNumber);
}

// Function to withdraw money from an account
void withdraw(struct BankAccount *account, float amount) {
    if (amount <= account->balance) {
        account->balance -= amount;
        printf("Withdrawn %.2f from account %d.\n", amount, account->accountNumber);
    } else {
        printf("Insufficient balance in account %d.\n", account->accountNumber);
    }
}

// Function to display account details
void displayAccount(struct BankAccount account) {
    printf("Account Holder: %s\n", account.name);
    printf("Account Number: %d\n", account.accountNumber);
    printf("Balance: %.2f\n", account.balance);
}

int main() {
    int choice;
    struct BankAccount accounts[100]; // Assume a maximum of 100 accounts

    int numAccounts = 0; // Current number of accounts

    while (1) {
        printf("\nBank Management System\n");
        printf("1. Create Account\n");
        printf("2. Deposit\n");
        printf("3. Withdraw\n");
        printf("4. Display Account Details\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                accounts[numAccounts++] = createAccount();
                break;
            case 2:
                if (numAccounts > 0) {
                    int accNum;
                    printf("Enter account number: ");
                    scanf("%d", &accNum);
                    float amount;
                    printf("Enter amount to deposit: ");
                    scanf("%f", &amount);
                    for (int i = 0; i < numAccounts; i++) {
                        if (accounts[i].accountNumber == accNum) {
                            deposit(&accounts[i], amount);
                            break;
                        }
                    }
                } else {
                    printf("No accounts created yet.\n");
                }
                break;
            case 3:
                if (numAccounts > 0) {
                    int accNum;
                    printf("Enter account number: ");
                    scanf("%d", &accNum);
                    float amount;
                    printf("Enter amount to withdraw: ");
                    scanf("%f", &amount);
                    for (int i = 0; i < numAccounts; i++) {
                        if (accounts[i].accountNumber == accNum) {
                            withdraw(&accounts[i], amount);
                            break;
                        }
                    }
                } else {
                    printf("No accounts created yet.\n");
                }
                break;
            case 4:
                if (numAccounts > 0) {
                    int accNum;
                    printf("Enter account number: ");
                    scanf("%d", &accNum);
                    for (int i = 0; i < numAccounts; i++) {
                        if (accounts[i].accountNumber == accNum) {
                            displayAccount(accounts[i]);
                            break;
                        }
                    }
                } else {
                    printf("No accounts created yet.\n");
                }
                break;
            case 5:
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}
