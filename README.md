# Creating a SimpleWallet Smart Contract

The `SimpleWallet` is a Solidity smart contract that allows an owner to manage Ether deposits and withdrawals. It includes functionality for depositing Ether, withdrawing specified amounts, checking the balance, and withdrawing all funds.

## Features

- **Owner Management**: Only the contract owner can withdraw funds.
- **Ether Deposits**: Anyone can deposit Ether into the contract.
- **Ether Withdrawals**: The owner can withdraw specified amounts or all Ether from the contract.
- **Balance Checks**: Anyone can check the contract's Ether balance.
- **Error Handling**: Demonstrates the use of `require()`, `assert(),` and `revert()` for safety checks and error handling.

## Events

- **Deposit**: Emitted when Ether is deposited into the contract.
  - `depositor`: The address of the depositor.
  - `depositAmount`: The amount of Ether deposited.

- **Withdraw**: Emitted when Ether is withdrawn from the contract.
  - `withdrawer`: The address of the withdrawer.
  - `withdrawAmount`: The amount of Ether withdrawn.

## Functions

### Constructor

```solidity
constructor() {
    walletOwner = msg.sender; // Set the contract deployer as the owner
    walletBalance = 0;
}
```
## Modifiers 

### onlyOwner

```modifier onlyOwner() {
    require(msg.sender == walletOwner, "Caller is not the owner");
    _;
}
```
Ensures that the caller is the contract owner.

### Deposit Ether
```function deposit() public payable {
    require(msg.value > 0, "Deposit amount must be greater than zero");
    
    walletBalance += msg.value;
    emit Deposit(msg.sender, msg.value);
}
```
Allows anyone to deposit Ether into the contract. The deposit amount must be greater than zero.

### Withdraw Ether
```function withdraw(uint256 withdrawAmount) public onlyOwner {
    require(withdrawAmount <= walletBalance, "Insufficient balance in the contract");

    walletBalance -= withdrawAmount;
    payable(msg.sender).transfer(withdrawAmount);
    emit Withdraw(msg.sender, withdrawAmount);
}
```
Allows the owner to withdraw a specified amount of Ether from the contract. The amount must not exceed the contract's balance.

### Check Balance
```function checkWalletBalance() public view returns (uint256) {
    assert(walletBalance >= 0); // Ensure the balance is never negative
    return walletBalance;
}
```
Returns the current Ether balance of the contract. Ensures the balance is never negative using assert().

### Force Revert
```function forceRevert() public pure {
    revert("This function always reverts");
}
```
Demonstrates the use of revert() by always reverting the transaction with a custom error message.

### Withdraw All Ether
```function withdrawAll() public onlyOwner {
    uint256 amount = walletBalance;
    walletBalance = 0;
    payable(walletOwner).transfer(amount);
    emit Withdraw(walletOwner, amount);
}
```
Allows the owner to withdraw all Ether from the contract, setting the balance to zero.

## Usage
Deploy the SimpleWallet contract to an Ethereum-compatible blockchain.

Interact with the contract using a web3-enabled browser or a dApp interface.

Use the deposit function to send Ether to the contract.

Use the withdraw or withdrawAll functions to retrieve Ether from the contract (owner only).

## Help
If you encounter any issues or have questions, please refer to the documentation or contact the contributors:

## Authors

Vatsalya Mishra

https://github.com/Vatsalya117
