# Degan-Coin

This Solidity program is a "Degan Token" program that demonstrates the basic syntax and functionality of the Solidity programming language. The purpose of this program is to create a ERC20 token and use it as per the needs.

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract has fivr function such as "mintTo", "burnFrom", "redeem", "transferTo" and "getOwnedAssets" which allows owner to mint tokens, users to burn tokens, redeem token, transfer the tokens and get their owned/redeemed assests.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >0.8.9;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract DegenToken is ERC20 {
    address private owner;
    string[3] private items = ["Car","Bike","Shoes"];
    uint[3] private prices = [1000, 500, 100];
    mapping(address => string[]) private ownedAssets;
    constructor() ERC20("Degen", "DGN"){
        owner = msg.sender;
    }

    modifier onlyOwner{
        require(owner==msg.sender,"Only owner has access");
        _;
    }

    function mintTo(address _to,uint _val) public onlyOwner{
        _mint(_to,_val);
    }

    function burnFrom(uint _val) public {
        _burn(msg.sender, _val);
    }

    function redeem(uint _item) public {

        require(_item-1 < items.length && _item-1 >= 0, "Item index out of bounds");
        uint price = prices[_item-1];
        _burn(msg.sender, price);
         ownedAssets[msg.sender].push(items[_item - 1]);
    }

    function transferTo(address _to, uint _val) public  {
        _transfer(msg.sender, _to, _val);
    }

    function getOwnedAssets(address _owner) public view returns (string[] memory) {
        return ownedAssets[_owner];
    }

    
}
```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.4" (or another compatible version), and then click on the "Compile Degan.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "Degan" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the mintTo function. Click on the "Degan" contract in the left-hand sidebar, and then click on the "mintTo" function. Finally, click on the "transact" button to execute the function.

## Authors

Harshdeep Singh 
