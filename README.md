# Module3 ERC20 Token Contract

# Overview
This repository contains an ERC20 token contract named `Module3`, developed using the Solidity programming language and intended to run on the Ethereum blockchain. The contract utilizes the OpenZeppelin library to ensure security and standard functionality.

# Functions
The `Module3` contract provides the following main functions:

1. **transfer**: Transfers tokens from the sender's account to the recipient's account. This function also emits a `TransferCustom` event upon successful transfer.
   ```solidity
   function transfer(address recipient, uint256 amount) public virtual override returns (bool);
   ```

2. **burn**: Allows users to destroy a specific amount of their own tokens, reducing the total supply. This function emits a `Burn` event.
   ```solidity
   function burn(uint256 amount) public;
   ```

3. **mint**: Allows the contract owner to create new tokens and assign them to a specified address. This function emits a `Mint` event.
   ```solidity
   function mint(address to, uint256 amount) public;
   ```

# Usage
This code is designed to be run in the Remix IDE, a powerful web-based tool for developing, deploying, and managing Solidity smart contracts. To run this code in Remix IDE:
1. Open Remix IDE in your web browser.
2. Create a new file and paste the provided Solidity code.
3. Compile the contract using the Solidity compiler in Remix.
4. Deploy the contract to an Ethereum testnet or the mainnet.
5. Interact with the deployed contract using the Remix interface.

# Owner
This contract is created and maintained by **Ralph Lauren Bensurto**.

# License
This project is licensed under the MIT License. See the LICENSE file for details.

# solidity

   ```// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract Module3 is ERC20 {
    event TransferCustom(address indexed from, address indexed to, uint256 value);
    event Burn(address indexed burner, uint256 value);
    event Mint(address indexed to, uint256 value);

    constructor() ERC20("ASSESSMENT", "RALPH LAUREN") {
        _mint(msg.sender, 200 * (2 * uint256(decimals())));
    }

    function transfer(address recipient, uint256 amount) public virtual override returns (bool) {
        bool success = super.transfer(recipient, amount);
        if (success) {
            emit TransferCustom(msg.sender, recipient, amount);
        }
        return success;
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
        emit Burn(msg.sender, amount);
    }

    function mint(address to, uint256 amount) public {
        _mint(to, amount);
        emit Mint(to, amount);
    }
}
   ```
