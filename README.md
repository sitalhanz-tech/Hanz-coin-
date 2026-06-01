# HANZCoin Smart Contract

A Solidity-based ERC20 token with revenue-sharing mechanism for content creators and fans.

## Features

- **ERC20 Token**: Standard token implementation with 18 decimals
- **Content Creation**: Creators can register content on-chain
- **Fan Staking**: Fans can stake tokens to support content
- **Revenue Distribution**: Automated revenue sharing (85% creators, 10% fans, 5% protocol)
- **Reward Claims**: Fans can claim proportional rewards based on their stake

## Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- MetaMask or similar Web3 wallet
- Private key with testnet ETH

## Installation

```bash
# Install dependencies
npm install

# Copy environment template
cp .env.example .env
```

## Configuration

Edit `.env` with your values:

```env
PRIVATE_KEY=your_private_key_here
INFURA_API_KEY=your_infura_key_here
ETHERSCAN_API_KEY=your_etherscan_key_here
POLYGONSCAN_API_KEY=your_polygonscan_key_here
```

### Get Required Keys

1. **Private Key**:
   - Open MetaMask → Click profile icon → Account Details → Export Private Key
   - ⚠️ **Never share your private key**

2. **Infura API Key** (Free RPC Provider):
   - Go to [infura.io](https://infura.io/)
   - Sign up and create a new project
   - Copy the Project ID

3. **Etherscan API Key** (For verification):
   - Go to [etherscan.io/apis](https://etherscan.io/apis)
   - Sign up and create an API key
   - ✅ Enable "Contract Source Code Verification"

4. **Test ETH**:
   - Sepolia: [sepoliaethereumfaucet.com](https://www.sepoliaethereumfaucet.com/)
   - Goerli: [goerlifaucet.com](https://goerlifaucet.com/)
   - Polygon Mumbai: [faucet.polygon.technology/](https://faucet.polygon.technology/)

## Deployment

### Deploy to Sepolia Testnet

```bash
npm run deploy:sepolia
```

### Deploy to Ethereum Mainnet

```bash
npm run deploy:mainnet
```

### Deploy to Polygon Mainnet

```bash
npm run deploy:polygon
```

### Deploy to Polygon Mumbai Testnet

```bash
npm run deploy:mumbai
```

## Contract Verification

### Automatic Verification (Recommended)

The deployment script automatically verifies your contract if you provided an API key:

```bash
npm run deploy:sepolia
# Automatically verifies on Etherscan after deployment
```

### Manual Verification on Etherscan

If automatic verification fails, verify manually:

1. Go to your contract on [sepolia.etherscan.io](https://sepolia.etherscan.io/)
2. Click **"Contract"** tab
3. Click **"Verify and Publish"**

#### Step 1: Contract Address
```
Enter your deployed contract address
```

#### Step 2: Compiler Type
```
Select: Single File (Solidity)
```

#### Step 3: Compiler Version
```
Select: v0.8.20
```

#### Step 4: Optimization
```
Toggle: Yes (8 runs recommended)
```

#### Step 5: Contract Code
Copy your entire `HANZCoin.sol` contract code and paste it in the text area.

#### Step 6: Constructor Arguments
If your contract has constructor arguments, provide them in ABI-encoded format. For HANZCoin (no arguments):
```
Leave empty
```

#### Step 7: License
```
Select: MIT
```

#### Step 8: Verification
Click **"Verify and Publish"**

### Verification Using Hardhat Plugin (Alternative)

```bash
npx hardhat verify --network sepolia <DEPLOYED_ADDRESS>
```

Example:
```bash
npx hardhat verify --network sepolia 0x1234567890123456789012345678901234567890
```

## Testing

```bash
# Run all tests
npm test

# Run specific test file
npm test test/HANZCoin.test.js

# Run with gas reporter
npm run test:gas
```

## Contract Functions

### createContent(string memory _title)
Creates new content entry
- Returns: Content ID

### stakeAsFan(uint256 _contentId, uint256 _amount)
Stake tokens as a fan to support content
- Parameters:
  - `_contentId`: ID of content to stake on
  - `_amount`: Amount of HNZ tokens to stake

### distributeRevenue(uint256 _contentId)
Distribute revenue for content (payable function)
- Parameters:
  - `_contentId`: Content ID
  - Value: Amount of ETH/native token to distribute

### claimFanReward(uint256 _contentId)
Claim fan rewards based on stake
- Parameters:
  - `_contentId`: Content ID

## Revenue Distribution

- **Creator**: 85%
- **Fans**: 10%
- **Protocol**: 5%

## Security Considerations

⚠️ **Important**: This contract includes:
- OpenZeppelin's audited ERC20 and Ownable contracts
- Access control for sensitive functions
- Event logging for transparency

Consider:
- Full security audit before mainnet deployment
- Testnet deployment and thorough testing first
- Using a multisig wallet for owner functions on mainnet

## Deployment Checklist

- [ ] Obtained testnet ETH
- [ ] Set up `.env` with all required keys
- [ ] Tested contract on Sepolia or Mumbai
- [ ] Verified contract on block explorer
- [ ] Reviewed contract code and security
- [ ] (Optional) Obtained security audit
- [ ] Ready for mainnet deployment

## Block Explorers

- **Ethereum Sepolia**: https://sepolia.etherscan.io/
- **Ethereum Mainnet**: https://etherscan.io/
- **Polygon Mumbai**: https://mumbai.polygonscan.com/
- **Polygon Mainnet**: https://polygonscan.com/

## Troubleshooting

### Verification Failed
- Check API key is correct and has verification permission
- Ensure compiler version matches (v0.8.20)
- Check contract address is correct
- Wait 1-2 minutes after deployment before verifying

### Deployment Failed
- Ensure you have sufficient testnet ETH
- Check RPC endpoint is working
- Verify private key is correct
- Check network is correct in `.env`

### Constructor Arguments Error
- HANZCoin has no constructor parameters
- Leave ABI-encoded arguments empty during verification

## Resources

- [Hardhat Documentation](https://hardhat.org/getting-started)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/)
- [Solidity Documentation](https://docs.soliditylang.org/)
- [Etherscan API Docs](https://docs.etherscan.io/)

## License

MIT License - See LICENSE file for details

