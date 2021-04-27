<<<<<<< HEAD
# Conway's Game of Life

![game of life example](./assets/Gospers_glider_gun.gif)

The Game of life is a zero player game developed in the 70's by John Horton Conway. Check out the [Wikipedia article](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life) for a full description.
The evolving state of the game is determined by the initial configuration - some configurations become infinitely evolving constellations, others eventually evolve into a stable patterns, whilst others die off completely.
It is commonly used as a tech test as it can be solved in many different ways that clearly show the level of the programmer.

### The Brief

The rules are as follows:

* The game evolves in turns, commonly known as 'ticks'.
* All changes occur at the same time.
* Any live cell with 2 or 3 live neighbours survives until next tick.
* Any live cell with less than 2 live neighbours dies (underpopulation).
* Any live cell with more than 3 live neighbours dies (overpopulation).
* Any dead cell with exactly 3 neighbours becomes a live cell (reproduction).

Write code that is capable of calculating each new generation, given a starter board. Although you don't have to build a visualisation tool to be able to see the evolution, it should be easy to extend the program to add on a web or command line UI.
=======
# Bank tech test

This is a mock tech test for week 10 of Maker's Academy. I took a day and a half to build three classes, of which Bank is the dependant, and Transaction and Statement the dependencies. The trade-off benefit of the dependency introduced by the extra classes was to adhere better to the SRP. It made it more complicated as I had to add mocks to inject dependency, but it was a good opportunity to practise my mocking skills.

The rough planning can be seen at the bottom of the readme, and its progress tracked through the commits. I originally planned to have two separate classes for Deposit and Withdrawal, but when I built them out I noticed they were mirroring one another, so to keep things dry I combined them into one and just added a conditional to decide which column (credit/debit) the transaction should go in.

In its current iteration, the date and amount are input manually, and in fact will accept any data, which could be improved. This is an ethical bank which will let you overdraw yourself to an unlimited amount and never charge you any fees, because someone being poor is not a good reason to fine them.

To run this code, please clone the repo; `rspec` will run the test suite.
Please see below for irb demonstration and plans.

**After coach review**
Things to change/add:
- Follow user stories in feature spec
- **Autogenerate date / time, use strf, stub**
- "You should be able to indirectly test in your bank_spec that the transactions are being added to the array of transactions (by testing the public methods that are interacting with the private method carrying this out). It looks as though you are doing this manually in your tests."
- "Storing both the balance and the amount is a duplication of code, and you can actually just include the latter in order to calculate the balance after each transaction at runtime of the print statement."

## Specification

### Requirements

* You should be able to interact with your code via a REPL like IRB or the JavaScript console.  (You don't need to implement a command line interface that takes input from STDIN.)
* Deposits, withdrawal.
* Account statement (date, amount, balance) printing.
* Data can be kept in memory (it doesn't need to be stored in a database or anything).

### Acceptance criteria

**Given** a client makes a deposit of 1000 on 10-01-2012  
**And** a deposit of 2000 on 13-01-2012  
**And** a withdrawal of 500 on 14-01-2012  
**When** she prints her bank statement  
**Then** she would see

```
date || credit || debit || balance
14/01/2012 || || 500.00 || 2500.00
13/01/2012 || 2000.00 || || 3000.00
10/01/2012 || 1000.00 || || 1000.00
```

## Self-assessment

Once you have completed the challenge and feel happy with your solution, here's a form to help you reflect on the quality of your code: https://docs.google.com/forms/d/1Q-NnqVObbGLDHxlvbUfeAC7yBCf3eCjTmz6GOqC9Aeo/edit

## Planning

Class: Bank
Methods: transaction [create Transaction class], statement
Instance variables: balance, transactions [array of Transaction class]

Class: Transaction
Keeps track of amounts, date, current balance
Methods: initialize
Instance variables: details hash { amount, date, balance }

## irb
```$ irb -r "./lib/bank"
2.7.2 :001 > bank = Bank.new
 => #<Bank:0x00007fc65b9c25d8 @balance=0, @transactions=[]>
2.7.2 :002 > bank.transaction(100, "01.01.2000")
 => [#<Transaction:0x00007fc65b8e4ad0 @details={"amount"=>100, "date"=>"01.01.2000", "current_balance"=>100}>]
2.7.2 :003 > bank.transaction(1000, "03.01.2000")
 => [#<Transaction:0x00007fc65b8e4ad0 @details={"amount"=>100, "date"=>"01.01.2000", "current_balance"=>100}>, #<Transaction:0x00007fc65b9903f8 @details={"amount"=>1000, "date"=>"03.01.200
0", "current_balance"=>1100}>]
2.7.2 :004 > bank.transaction(-675, "04.01.2000")
 => [#<Transaction:0x00007fc65b8e4ad0 @details={"amount"=>100, "date"=>"01.01.2000", "current_balance"=>100}>, #<Transaction:0x00007fc65b9903f8 @details={"amount"=>1000, "date"=>"03.01.200
0", "current_balance"=>1100}>, #<Transaction:0x00007fc65b999408 @details={"amount"=>-675, "date"=>"04.01.2000", "current_balance"=>425}>]
2.7.2 :005 > bank.create_statement
date || credit || debit || balance
04.01.2000 || || 675 || 425
03.01.2000 || 1000 || || 1100
01.01.2000 || 100 || || 100```
>>>>>>> 8e5b50807d086747ff876294c1959026c3693fa4
