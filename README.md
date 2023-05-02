#  How to Integrate Chainlink Keepers on the Celo Blockchain

## Table of Contents
- [How to Integrate Chainlink Keepers on the Celo Blockchain](#how-to-integrate-chainlink-keepers-on-the-celo-blockchain)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Prerequisites](#prerequisites)
  - [Requirements](#requirements)
  - [What is Chainlink Keepers?](#what-is-chainlink-keepers)
  - [Use Cases of Chainlink Keepers](#use-cases-of-chainlink-keepers)
  - [Setting up your Environment](#setting-up-your-environment)
  - [Installing Hardhat and Chainlink Libraries](#installing-hardhat-and-chainlink-libraries)
  - [Creating a Smart Contract with Chainlink Keepers](#creating-a-smart-contract-with-chainlink-keepers)
  - [Deploying the Smart Contract to Celo Testnet](#deploying-the-smart-contract-to-celo-testnet)
  - [Registering the Keeper with the Keeper Registry](#registering-the-keeper-with-the-keeper-registry)
  - [Testing the Smart Contract with Chainlink Keepers](#testing-the-smart-contract-with-chainlink-keepers)
  - [Conclusion](#conclusion)

## Introduction

**[Chainlink Keepers](https://docs.chain.link/chainlink-automation/introduction/)** is a decentralized service that enables smart contracts to be triggered based on external events, without the need for manual intervention. This makes it possible to automate the execution of certain functions in a smart contract, which can save time and reduce costs.

**[Celo](https://docs.celo.org/learn/celo-overview)** is a mobile-first blockchain platform that aims to provide financial access to anyone with a mobile phone. It is built on Ethereum and uses a proof-of-stake consensus mechanism. By integrating Chainlink Keepers with Celo, developers can create more robust and efficient smart contracts that can be triggered automatically.

## Prerequisites

To follow this tutorial, you will need the following:

- Basic understanding of blockchain technology and smart contracts
- Familiarity with Solidity programming language
- Basic Javascript programming skills
- Basic knowledge of Celo blockchain
- Access to a Celo testnet node
- Access to a Chainlink node

## Requirements
- Node.js and npm installed on your system
- Hardhat installed on your system
- Access to a Celo testnet node
- Access to a Chainlink node


## What is Chainlink Keepers?

**[Chainlink Keepers](https://docs.chain.link/chainlink-automation/introduction/)** is a decentralized service that allows developers to reliably automate regular smart contract triggers without the resources and risks associated with performing keeper operations manually or through centralized systems. Because Keepers automates key time and event-based smart contract functions, it frees developers to focus on building new use cases across industries such as DeFi, insurance, gaming, and NFT art.

Chainlink Keepers works by using external adapters to monitor events on various external data sources. When an event occurs, the adapter triggers the smart contract, which then executes a specific function. This process is completely automated and does not require any manual intervention.

Chainlink Keepers is especially useful for applications that require the execution of certain functions at specific intervals or when certain conditions are met. For example, a smart contract that requires a certain action to be taken when the price of an asset reaches a certain threshold can be automated using Chainlink Keeper.

## Use Cases of Chainlink Keepers 

**[Celo](https://docs.celo.org/learn/celo-overview)** is a mobile-first blockchain platform that focuses on financial inclusion. Thus, by integrating Chainlink Keepers with Celo, developers can create more efficient and robust smart contracts that can be triggered automatically. This can help to reduce costs and increase the overall efficiency of the platform.

Chainlink Keepers can also be used to automate certain functions in Celo's governance system, such as triggering a vote when a certain condition is met. This can help to make the governance process more transparent and efficient.

Some important use cases for Chainlink Keepers include:

1. Automated market-making: Chainlink Keepers can be used to automate the rebalancing of a liquidity pool. This ensures that the pool remains balanced and that traders are always able to execute trades at a fair price.

2. Contract maintenance: Chainlink Keepers can be used to perform routine maintenance tasks on smart contracts. For example, they can update contract parameters or check for security vulnerabilities.

3. Decentralized finance (DeFi) applications: Chainlink Keepers can be used to automate the execution of complex financial transactions in DeFi applications. This can help to reduce the risk of human error and ensure that transactions are executed in a timely and efficient manner.

4. Decentralized autonomous organizations (DAOs): Chainlink Keepers can be used to automate the governance processes of DAOs. For example, they can be used to automatically trigger a vote when a proposal meets certain conditions.

5. Gaming: Chainlink Keepers can be used to automate game logic in blockchain-based games. For example, they can be used to trigger certain events when certain conditions are met, such as when a player completes a level or reaches a certain score.



## Setting up your Environment

To get started, you will need to set up your development environment. Here are the steps you need to follow:

1. Install Node.js and npm on your system. You can download them from the official website: https://nodejs.org/en/.
2. Install Hardhat by running the following command in your terminal:

  ```bash
    npm install --save-dev hardhat
  ```

3. Create a new directory for your project and navigate to it in your terminal.
4. Initialize a new Hardhat project by running the following command:

  ```bash
    npx hardhat
  ```

5. Follow the prompts to set up your project. Choose the options that best suit your needs.

6. Once the project is set up, open it in your favorite code editor

## Installing Hardhat and Chainlink Libraries

After setting up your environment, you will need to install the necessary libraries to use Chainlink Keepers on Celo. Here are the steps you need to follow:

1. Install the Hardhat Celo plugin by running the following command:

  ```bash
    npm install @celo/hardhat-plugin
  ```

2. Install the Hardhat Chainlink plugin by running the following command:

  ```bash
    npm install @chainlink/hardhat-ethers@0.1.3
  ```

3. Install the Chainlink Keeper library by running the following command:

  ```bash
    npm install @chainlink/keeper-contracts
  ```

4. Configure your Hardhat project to use the Celo and Chainlink plugins. Open your hardhat.config.js file and add the following code:

  ```bash
    require("@celo/hardhat-plugin");
    require("@chainlink/hardhat-ethers");
  ```

5. Configure your Chainlink node URL and the Keeper registry address in your hardhat.config.js file. You can get these values from your Chainlink node:

```bash
  module.exports = {
  defaultNetwork: "hardhat",
  networks: {
    hardhat: {
      forking: {
        url: "https://forno.celo.org",
      },
    },
    celo: {
      url: "https://forno.celo.org",
      accounts: {
        mnemonic: "<your-mnemonic>",
      },
    },
  },
  keeper: {
    url: "https://<your-chainlink-node-url>",
    keeperRegistry: "<your-keeper-registry-address>",
  },
  solidity: {
    compilers: [
      {
        version: "0.8.9",
        settings: {
          optimizer: {
            enabled: true,
            runs: 200,
          },
        },
      },
    ],
  },
};
```

Note: Replace `<your-mnemonic>`, `<your-chainlink-node-url>`, and `<your-keeper-registry-address>` with the appropriate values for your project.

## Creating a Smart Contract with Chainlink Keepers

Now that your environment is set up, you can create a sample smart contract that uses Chainlink Keepers on Celo. Here are the steps you need to follow:

1. Create a new Solidity file in your `contracts` directory. For this tutorial, we will call it `KeeperCount.sol`.
2. Define a new contract in your Solidity file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.9;

import import "@chainlink/contracts/src/v0.8/AutomationCompatible.sol";

contract KeeperCount is AutomationCompatibleInterface {
  uint256 public counter;
  uint256 public interval;

  constructor(uint256 _interval) {
    interval = _interval;
  }

  function checkUpkeep(bytes calldata /* checkData */) external override returns (bool upkeepNeeded, bytes memory /* performData */) {
    return (block.timestamp >= counter + interval, "");
  }

  function performUpkeep(bytes calldata /* performData */) external override {
    counter = block.timestamp;
  }
}
```

Let's go through the `KeeperCount` contract together;

The `KeeperCounter` contract imports the `AutomationCompatible.sol` file from the `@chainlink/contracts/src/v0.8/` directory. This file contains an interface called `AutomationCompatibleInterface`, which this contract implements. The purpose of this interface is to allow the contract to be used with Chainlink Keepers, which are a type of automated system that can perform certain tasks.

The contract has two public variables: `counter` and `interval`. The `counter` variable keeps track of the last time the `performUpkeep` function was called, while the `interval` variable specifies how often the upkeep function should be performed.

The contract also has two functions that implement the `AutomationCompatibleInterface` interface. The `checkUpkeep` function checks whether the upkeep function needs to be performed, based on the current time and the `interval` variable. If upkeep is needed, it returns a boolean value of true, along with an empty byte array. If upkeep is not needed, it returns a boolean value of false, along with an empty byte array.

The `performUpkeep` function updates the `counter` variable to the current time. This function is called by the Chainlink Keeper system when the `checkUpkeep` function returns true.

Let's now proceed and compile the smart contract.

Compile the contract by running the following command in your terminal:

  ```bash
    npx hardhat compile
  ```

## Deploying the Smart Contract to Celo Testnet

Now that you have created your smart contract, you can deploy it to the Celo network. Here are the steps you need to follow:

1. Create a new deployment script in your `scripts` directory. For this example, we will call it `deploy.js`.
2. Import the necessary libraries and define your deployment function:

```javascript
const { ethers } = require("hardhat");

async function main() {
  const KeeperCount = await ethers.getContractFactory("KeeperCount");
  const keeperCount = await KeeperCount.deploy(3600); // set interval to 1 hour
  console.log("KeeperCount deployed to:", keeperCount.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```
The code above is a JavaScript file that uses the Hardhat framework to deploy the `KeeperCount` smart contract to the Celo

The first line imports the `ethers` library from the Hardhat package.

The `main` function is an asynchronous function that deploys the `KeeperCount` contract to the blockchain using the `getContractFactory` method from the `ethers` library. It sets the `interval` variable to 3600, which corresponds to 1 hour. It then logs the address of the deployed contract to the console.

The last few lines of code calls the `main` function and handles any errors that may occur during deployment.

1. Deploy the smart contract to the Celo network by running the following command:

  ```bash
    npx hardhat run --network celo scripts/deploy.js
  ```

4. Verify that the smart contract was deployed by checking the output in your terminal. You should see a message similar to the following:

  ```bash
    KeeperCount deployed to: 0x1234567890123456789012345678901234567890
  ```

## Registering the Keeper with the Keeper Registry

Now that your smart contract is deployed, you can register it with the Keeper Registry so that it can be executed by Chainlink Keepers. Here are the steps you need to follow:

1. Get the ABI for your smart contract by running the following command:

  ```bash
    npx hardhat compile --export-artifacts
  ```

This command will generate a `artifacts/contracts/KeeperCount.sol/KeeperCount.json` file that contains the ABI for your smart contract.

2. Register your smart contract with the Keeper Registry by running the following command:

  ```bash
    npx hardhat keeper-register --network celo --contract-name KeeperCount --contract-address <your-contract-address> --method-   name performUpkeep --abi-path artifacts/contracts/KeeperCount.sol/KeeperCount.json
  ```

This command registers the `KeeperCount` contract with the Keeper Registry and specifies the `performUpkeep` function as the function to be executed by Chainlink Keepers.

Note: Replace `<your-contract-address>` with the address of your deployed `KeeperCount` contract.

3. Verify that your contract is registered with the Keeper Registry by running the following command:

  ```bash
    npx hardhat keeper-list --network celo
  ```

This command should return a list of all contracts registered with the Keeper Registry, including your `KeeperCount` contract.

## Testing the Smart Contract with Chainlink Keepers

Now that your smart contract is registered with the Keeper Registry, you can test it with Chainlink Keepers. Here are the steps you need to follow:

1. Start your Chainlink node by running the following command:

  ```bash
    cd <your-chainlink-node-directory>
    ./chainlink node start
  ```

Note: Replace `<your-chainlink-node-directory>` with the directory where your Chainlink node is installed.

2. Create a new job definition for your smart contract by running the following command:

```json
curl -X POST -H "Content-Type: application/json" -d '{
  "initiators": [
    {
      "type": "cron",
      "params": {
        "schedule": "0 * * * * *" // execute every minute
      }
    }
  ],
  "tasks": [
    {
      "type": "keeper",
      "confirmations": 0,
      "params": {
        "contractAddress": "<your-contract-address>",
        "functionSelector": "performUpkeep"
      }
    }
  ]
}' "http://localhost:6688/v2/specs"
```

Again, replace `<your-contract-address>` with the address of your deployed KeeperCount contract.

This command creates a new job definition that executes the `performUpkeep` function on your `KeeperCount` contract every minute. It uses a cron initiator to schedule the job and a `keeper` task to execute the function.

3. Verify that the job definition was created by running the following command:

  ```bash
    curl -H "Content-Type: application/json" "http://localhost:6688/v2/specs"
  ```

This command should return a list of all job definitions registered with your Chainlink node, including the job definition you just created.

4. Wait for the Chainlink Keepers to execute your `performUpkeep` function. You can monitor the execution of your job by checking the logs of your Chainlink node:

  ```bash
    cd <your-chainlink-node-directory>
    ./chainlink logs
  ```

This will display the logs for your Chainlink node, including any executions of your job definition.

Congratulations! You have successfully integrated Chainlink Keepers on the Celo blockchain and tested it with a smart contract example.

## Conclusion

Chainlink Keepers provides a powerful tool for developers to automate the maintenance and upkeep of their smart contracts. By leveraging off-chain computing resources, developers can ensure that their smart contracts remain operational and secure without the need for manual intervention.

In this tutorial, we have explored how to integrate Chainlink Keepers on the Celo blockchain using Hardhat. We began by setting up our development environment and deploying a sample smart contract. We then proceeded to create a Chainlink node and configure it to communicate with our Celo blockchain node.

We then demonstrated how to create a Chainlink Keeper job definition that executes a function on our smart contract at regular intervals. This allows for automated upkeep and maintenance of the smart contract without the need for manual intervention.

