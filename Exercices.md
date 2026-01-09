# Exercices
## Exercise 1 (Repo 1): Discover the Code & Rough Size

###  Bank
```bash
    java -jar ckjm_ext.jar target/classes/bankAccountApp/Bank.class
```
- **LOC :** 413
- **NOM :** 14
- **Short description of responsibility :** Handle bank operations (create, update, delete accounts, etc...).

###  BankAccount
```bash
    java -jar ckjm_ext.jar target/classes/bankAccountApp/BankAccount.class
```
- **LOC :** 462
- **NOM :** 20
- **Short description of responsibility :** Handle account operations (get balance, set limit, withdraw money, etc...).

![exo1](img/capture1.png)

###  Person
```bash
    java -jar ckjm_ext.jar target/classes/bankAccountApp/Person.class
```
- **LOC :** 325
- **NOM :** 23
- **Short description of responsibility :** Handle client data (name, email, etc...)

###  BankAccountApp
```bash
    java -jar ckjm_ext.jar target/classes/bankAccountApp/BankAccountApp.class
```
- **LOC :** 491
- **NOM :** 2
- **Short description of responsibility :** App base.

BankAccountApp's size seems way too big for the number of methods it contains.
![exo1](img/capture2.png)


## Exercise 2 (Repo 1): Cyclomatic Complexity on a Key 

###  BankAccount
```bash
    java -jar ckjm_ext.jar target/classes/bankAccountApp/BankAccount.class
```
#### Weighted Methods per Class
20
#### Cyclomatic Complexity per method
![exo1](img/capture3.png)
The total Cyclomatic Complexity of the file is 33.
#### Method choosen : withdrawMoney
##### Tasks
1) 
**Cyclomatic Complexity value :** 5
```java
	public boolean withdrawMoney(double withdrawAmount) { 
		if (withdrawAmount >= 0 && balance >= withdrawAmount && withdrawAmount < withdrawLimit
				&& withdrawAmount + amountWithdrawn <= withdrawLimit) {   // decision point 1 (if)
			balance = balance - withdrawAmount;
			success = true;
			amountWithdrawn += withdrawAmount;
		} else { // decision point 2 (else)
			success = false;
		}
		return success;
	}
```
2) 
To reduce complexity, I would starts by removing the **else** block. I would then removed  the **success** variable to simply return true or false.
Finally, I would create a helper function **checkAccountBalance** to simplify the **if**.

3) Bonus
```java
	public boolean withdrawMoney(double withdrawAmount) { 
		if (checkAccountBalance(withdrawAmount)) {   // decision point 1 (if)
			balance = balance - withdrawAmount;
			amountWithdrawn += withdrawAmount;
			return true
		}
		return false;
	}

    public boolean checkAccountBalance(double withdrawAmount){
		/* 	Simplifying the if value as one of the clauses was redundant 
			(if withdrawAmount + amountWithdrawn <= withdrawLimit, 
			then withdrawAmount is < to withdrawLimit so there is no need to check).
		*/
        return (withdrawAmount >= 0 && balance >= withdrawAmount && withdrawAmount + amountWithdrawn <= withdrawLimit);
    }
```

The CC value of **withdrawMoney()** has lowered to 2. However the CC value of **checkAccountBalance()** is 4.

![exo1](img/capture4.png)


## Exercise 3 (Repo 1): CK Metrics Across Classes: Who Looks “Smelly”?


