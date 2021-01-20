# Unit_20_Homework

## These contracts will serve as payroll for our up and coming firm. Associates will be compensated in ETH with amounts based on tier.

### The first function, AssociateProfitSplitter, will divide balance and deposit into associate accounts. To run this function, navigate to "deploy and run transactions" in remix. select the employee accounts Ox addresses and put them in the three spots on the "deploy" dropdown. Ensure that the Account of the message sender is the HR payroll account. Press Deploy. Refer to "Completion - Ganache" screenshot in above repository for a view of the correct contract

-Bjorn



.sol file is as follows:

pragma solidity ^0.5.0;

// lvl 1: equal split
contract AssociateProfitSplitter {
    
    address payable employee_one;
    address payable employee_two;
    address payable employee_three;
    
    
    constructor(address payable _employee_one, address payable _employee_two, address payable _employee_three) public {
        employee_one = _employee_one;
        employee_two = _employee_two;
        employee_three = _employee_three;
    }

    function balance() public view returns(uint) {
        return address(this).balance;
    }

    function deposit() public payable {
        
        uint amount = msg.value / 3;

         employee_one.transfer(amount);
         employee_two.transfer(amount);
         employee_three.transfer(amount);

        msg.sender.transfer(msg.value - amount * 3);
    }

    function() external payable {
        uint amount = msg.value / 3;

         employee_one.transfer(amount);
         employee_two.transfer(amount);
         employee_three.transfer(amount);

        msg.sender.transfer(msg.value - amount * 3); 
    }
}
