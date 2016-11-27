# CurrencyExchange

CS160 Project 3

Due: November 13, 11:59 PM 		 Total Points: 100 pts	 

Problem Statement 

You have been hired by a travel firm.  Design and implement a program to quote currency exchange rates for different currencies, from different banks.  This way, the firm’s clients can get the best rates on foreign currency when traveling.

Problem Description

Our project requires us to define banks.  Each bank can exchange three currencies to and from US dollars.  For each currency, there is a rate at which the bank will buy and sell the currency in exchange for US dollars.  In addition, the bank charges a commission as a fee for performing the exchange.  All of this information is specified a file for each bank, which will be in the following format:

bank name
commission_rate
currency_code exchange_rate
currency_code exchange_rate
currency_code exchange_rate

As an example, consider this bank:
Shady Airport Bank
0.2
GBP 0.64
CAD 1.24
JPY 119.2

The above bank is called Shady Airport Bank and takes a 20% commission.  It will trade .64 Pounds for 1 US dollar, 1.24 Canadian dollars for 1 US dollar, and 119.2 Yen for 1 US dollar.  Note that this project has not been updated to consider Brexit.  The project assumes two banks, in two files – bank1.txt and bank2.txt.

Your code will first read in the bank files, to establish the banks we are using.  After reading the bank information, your program should prompt the user to enter
•	the type of transaction ("buy" or "sell")
•	the currency code (e.g., "GBP" or "gbp" or "Gbp")
•	the amount of the foreign currency to buy or sell
Then the program will display quotes from the two banks for the proposed currency exchange. All of this input and output happens at the console. Here is an example, which defines the messages you should print (output is in normal font, input is bold font):




Do you wish to buy or sell? what
Please try again.
Do you wish to buy or sell? buy
Which currency? Funbucks
I'm sorry. There is no bank that can exchange SCHRUTEBUCKS. Please start again.
Do you wish to buy or sell? sell
Which currency? jpy
There is one bank that can exchange JPY.
How many JPY? 4858.28
Big Name Bank will give you 342.48 USD for 4858.28 JPY, after collecting a commission of 33.87 USD (9%)
Do you wish to perform another transaction? yes
Do you wish to buy or sell? buy
Which currency? Cad
There are two banks that can exchange CAD.
How many CAD? 1000
Big Name Bank will give you 1000.00 CAD for 742.34 USD, after collecting a commission of 66.81 USD (9%)
Shady Airport Bank will give you 1000.00 CAD for 843.91 USD, after collecting a commission of 168.78 USD (20%) 
Do you wish to perform another transaction? no

Please note that all currency amounts are rounded to two digits.  The commission percentage is rounded to the nearest whole percent.  The code is always printed in UPPER CASE, as it appears in the bank file.  Our code should allow the user to input in any capitalization they wish, though.


Project Requirements

The requirements for this project are provided as a list of classes needed to solve the problem put forward in the project.  This is your first project writing your own classes and making objects of them.  You should feel free to add other methods if you desire them, but your code must include the following classes with the specified methods:

Currency Class (10 points)
Each currency line in one of the bank information files will be translated into an instance of a Currency class that should contain the following:
•	[2 pts] Two private data fields, one to hold the currency code and one to hold the exchange rate. Note that the exchange rate for the same currency could be different for different banks.
•	[4 pts] A constructor that takes two arguments: the currency code and exchange rate. The constructor should assign the private members from the values of the arguments.
•	[4 pts] An accessor method for each data field.








Bank Class (34 points)
Each bank will be represented by an instance of a Bank class, which should contain the following:
•	[5 pts] Five private data fields
o	The name of the bank
o	The commission rate
o	Three fields for the three currencies exchanged by the bank. Each of these should have type Currency.
•	A constructor that takes a file name (a String) as an argument. The constructor should...
o	[2 pts] open the file,
o	[8 pts] read in the information about the bank, initializing all of the bank's data fields.
•	[3 pts] A method supportCurrency that takes a currency code (a String) as its only argument. It should return true if the bank can exchange the given currency and false if it cannot.
•	[4 pts] A method getRate that takes a currency code (a String) as its only argument. It should return the rate of exchange for that currency, or -1.0 if the bank does not exchange that currency.
•	Two additional methods: quoteBuy and quoteSell. Each of these takes two arguments, a double for the amount of foreign currency, and a String for the currency code. Each method will return a Quote object (defined below) if the bank supports that currency and null if the bank does not. Call the getRate method you wrote within your quote methods.
Use the following formulas to calculate the number of US dollars and the bank's commission:
o	For selling amt units of currency with exchange rate rate, the number of US dollars before commission is amt / rate; call that base. Then the commission is the commission rate times base and the amount of US dollars the customer will receive is base minus the commission.
o	For buying amt units of currency with exchange rate rate and commission rate com (where com is between 0.0 and 1.0), the number of US dollars the customer will pay is  amt / (rate * (1 - com)); call that dollarsOwed. The commission is com * dollarsOwed.
[For each of buy and sell, the method prototype is worth 1 point, the correct calculation is worth 3 points, and creating and returning a Quote object is worth 2 points.]

Quote Class (16 points)
You will define a Quote class to capture the information about a potential currency exchange. It should contain the following:
•	[3 pts] Seven private data fields:
o	The name of the bank issuing the quote
o	The currency code of the currency given to the bank. Call this codeToBank.
o	The currency amount given to the bank. Call this amtToBank.
o	The currency code of the currency received from the bank. Call this codeFromBank.
o	The currency amount received from the bank. Call this amtFromBank.
o	The commission rate charged by the bank.
o	The dollar amount of the commission.
o	A DecimalFormat object for formatting currencies (i.e., two digits after the decimal point).
•	[3 pts] A constructor that takes 7 arguments, corresponding to the first 7 data fields listed above. The constructor should set those fields from the values of the arguments and create the DecimalFormat field.
•	[10 pts] A method called toString that takes no arguments and returns a String. It should return the message that will be printed out for the quote, as listed above (i.e., "Shady Airport Bank will give you 1000.00 CAD for 843.91 USD, after collecting a commission of 168.78 USD (20%)"). Note that the commission amount should always be reported in US dollars. 





CurrencyExchange Class (25 points)
Your main method should be in a CurrencyExchange class. It should follow this control flow:
•	[2 pts] Create two Bank objects, one for each file "bank1.txt" and "bank2.txt"
•	do{
o	[1 pt] Prompt the user if they want to buy or sell and get the user input
o	[2 pts] If the input is not valid, print error message and use continue to restart the loop
o	[1 pt] Prompt the user for the foreign currency and get the user input
o	[3 pts] Check how many banks support that currency
	[1 pt] If none, print the error message and use continue to restart the loop
	[1 pt] Otherwise, print how many banks can exchange that currency
o	[1 pt] Prompt the user for the amount of foreign currency and get the user input
o	[3 pts] Use the quoteBuy or quoteSell methods of the Bank objects to get a Quote from every bank supporting the foreign currency.
o	[4 pts] Print the quote(s) from the bank(s), using the toString method of the Quote object(s).
o	[4 pts] Use the console to prompt the user for another transaction
•	[2 pts] while the user wants to continue performing transactions


Documentation Requirements

•	Each class and each method should have a JavaDoc style comment, using /** */ commenting style above the class name and method name
•	Code should be legibly indented
•	Include a header comment at the top of the main file (in this case, CurrencyExchange), like:
		/*Max Fowler
	CS160 Project 3*/

Testing

To test your code, try making different bank files and ensuring that your project works and calculates correctly.  You should feel free to do the calculation by hand to ensure that the results are correct in your code. 

Hand-In

Submit all your code in a zip file (or your equivalent, like a rar or a tar) on Blackboard.









Evaluation

Correctness (85 points).  These points will be allocated as follows: 
10 points for correct Currency class
34 points for correct Bank class
16 points for correct Quote class
25 points for correct CurrencyExchange main class

Documentation and Design (15 points): Your code will receive up to 15 points for following the documentation requirements specified above and following the design specified in the project document.
