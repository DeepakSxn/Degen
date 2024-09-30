# DegenToken Smart Contract

## Introduction
The **DegenToken** is an ERC20-based token that allows users to mint, burn, transfer tokens, and redeem digital assets (e.g., LAPTOP, HEADPHONE, and EARPICE) by spending tokens. The contract is deployed on the Ethereum blockchain and makes use of OpenZeppelin’s ERC20 implementation.

## Features
- **Minting**: Only the contract owner can mint new tokens.
- **Burning**: Users can burn tokens they own.
- **Redeeming**: Users can redeem specific items (like LAPTOP, HEADPHONE) by burning tokens.
- **Transfer**: Standard ERC20 token transfer functionality.
- **Track Redeemed Assets**: Users can view the assets they have redeemed.

## Smart Contract Details

### Minting Tokens
Only the contract owner can mint tokens to any user.
```solidity
function mintTo(address _to, uint _val) public onlyOwner {
    _mint(_to, _val);
}
```

### Burning Tokens
Users can burn their tokens, reducing their balance.
```solidity
function burnFrom(uint _val) public {
    _burn(msg.sender, _val);
}
```

### Redeeming Items
Users can redeem specific items like "LAPTOP" by burning the required amount of tokens.
```solidity
function redeem(uint _item) public {
    require(_item-1 < items.length && _item-1 >= 0, "Item index out of bounds");
    uint price = prices[_item-1];
    _burn(msg.sender, price);
    ownedAssets[msg.sender].push(items[_item - 1]);
}
```

### Viewing Redeemed Items
Users can view the list of assets they have redeemed.
```solidity
function getOwnedAssets(address _owner) public view returns (string[] memory) {
    return ownedAssets[_owner];
}
```

## Technologies Used
- **Solidity**
- **OpenZeppelin** for ERC20 implementation.
- **Ethereum Blockchain**

## Getting Started

### Prerequisites
- **Node.js** and **npm**
- **Hardhat** for testing and deploying the smart contract
- **MetaMask** or any Ethereum wallet for interacting with the deployed contract.

### Installation

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/your-username/DegenToken.git
    cd DegenToken
    ```

2. **Install Dependencies**:
    ```bash
    npm install
    ```

3. **Compile the Smart Contract**:
    ```bash
    npx hardhat compile
    ```

4. **Run Tests**:
    You can run the test cases to ensure the contract works as expected:
    ```bash
    npx hardhat test
    ```

## Deploying the Contract

1. **Configure the Network**:  
   Update the `hardhat.config.js` file with your desired network settings (e.g., Ethereum Sepolia testnet) and private keys.

2. **Deploy the Contract**:
    ```bash
    npx hardhat run scripts/deploy.js --network sepolia
    ```

## Usage

### Minting Tokens
Only the contract owner can mint tokens:
```bash
npx hardhat run scripts/mint.js --network sepolia
```

### Redeeming Items
Users can redeem items by specifying the item number (e.g., LAPTOP = 1):
```bash
npx hardhat run scripts/redeem.js --network sepolia --item 1
```

### Viewing Redeemed Items
```bash
npx hardhat run scripts/getOwnedAssets.js --network sepolia --address 0xYourAddress
```

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Contact
For any questions or inquiries, feel free to reach out at deepaksaxena192837@gmail.com.

---
