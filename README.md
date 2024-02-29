# Create Foundry project
mkdir foundry_project && cd foundry_project
npm init -y
# (Install Foundry)
curl -L https://foundry.paradigm.xyz | bash 
foundryup
#  Initialize a Foundry project:
forge init; # forge init --force; # if there is already an existing .git repository associated

# Project structure:
.
├── README.md
├── foundry.toml
├── lib
│   └── forge-std
├── script
│   └── Counter.s.sol
├── src
│   └── Counter.sol
└── test
    └── Counter.t.sol

# Install the dependencies needed for an ERC20 contract from OpenZeppelin, by funning the following:
forge install OpenZeppelin/openzeppelin-contracts;

# Creating the ERC20 Contract:
Convert the existing .src/Counter.sol --> "TokenName.sol" and replace the code with the following Solidity code.
Rename: test/Counter.t.sol --> test/TokenName.t.sol ---> Edit test script

# Compile contract:
forge compile;

# Testing the ERC20 Contract:
forge test -vvv;

# Configuring Foundry for Berachain Contract Deployment:
Rename: script/Counter.s.sol script/TokenName.s.sol;
Write deploy script

# With the provided private key, replace the WALLET_PRIVATE_KEY in .env file:
File: ./.env
WALLET_PRIVATE_KEY="0x...."

# Deployment to Berachain Testnet should be the same process, but with a specified RPC URL endpoint:
forge script script/JOSE.s.sol --rpc-url "https://rpc.ankr.com/berachain_testnet" --broadcast;

# Verifying ERC20 Contract:
forge verify-contract "Contract Address" "Contract name" \
    --etherscan-api-key="XXXXXXXX" \
    --watch \
    --constructor-args $(cast abi-encode "constructor(string,string,uint256)" "JOSEToken" "JOSE" 100000000000000000000) \
    --retries=2 \
    --verifier-url=https://api.routescan.io/v2/network/testnet/evm/80085/etherscan/api/;


