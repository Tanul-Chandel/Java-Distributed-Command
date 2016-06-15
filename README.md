# Java-Distributed-Command

We have a BankAccount and we know how to calculate interest on the account but interest calculation takes a very long time on our machine.We don't want to do the computation on our machine. We want to write down the instruction for interest calculation and ship it along with our BankAccount to a powerful server. The server executes interest calculation instruction, saves the result in our BankAccount and returns back the BankAccount with calculated interest saved on the BankAccount.This is an example of "Distributed Command" pattern.

1.Command : an interface called Command that has only one method "execute" .This interface is implemented by different classes to use the same Client/ Server to do the calculations as per the implementation of execute method .

2.CalculateInterestCommand : a sub-class of BankAccount that implements Command interface.

3.CommandRouter : a class, a TCP/IP client . This has a method: public Command route(Command anyCommand) . This method will send any Command to the ThreadedCommandServer and receive the Command back from the server.

4.ThreadedCommandServer : a class that receives any command, hand it off to CommandServerThread and call execute on this. When done , the server returns the command object back to the router (caller).

5.CalculateInterestCommand : a tester that creates a CalculateInterestCommand, populates it and forwards it to a ComamandRouter for routing. When the CalculateInterestCommand returns, the returned CalculateInterestCommand has the interest amount populated in it and tester would print it by calling getInterestAmount.

6.Mortgage, MortgageCommand, MortgageCommandTester: Similar to BankAccount, CalculateInterestCommand & CalculateInterestCommand that uses the same router ( CommandRouter ) and Server (ThreadedCommandServer) to calculate Mortgage instead of Interest.
