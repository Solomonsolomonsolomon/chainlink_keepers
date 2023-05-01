#  How to Integrate the Chainlink Keepers on Celo Blockchain:

## Table of Contents:

- [How to Integrate the Chainlink Keepers on Celo Blockchain](#how-to-integrate-the-chainlink-keepers-on-celo-blockchain)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Pre-requisites](#pre-requisites)
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

## Introduction:

**[Chainlink Keepers](https://docs.chain.link/chainlink-automation/introduction/)** is a decentralized service that enables smart contracts to be triggered based on external events, without the need for manual intervention. This makes it possible to automate the execution of certain functions in a smart contract, which can save time and reduce costs.

**[Celo](https://docs.celo.org/learn/celo-overview)** is a mobile-first blockchain platform that aims to provide financial access to anyone with a mobile phone. It is built on Ethereum and uses a proof-of-stake consensus mechanism. By integrating Chainlink Keepers with Celo, developers can create more robust and efficient smart contracts that can be triggered automatically.

## Prerequisites:

To follow this tutorial, you will need the following:

- Understanding of Blockchain Technology & Smart Contracts.
- Familiarity with Solidity & Javascript programming language.
- Knowledge of Celo blockchain.

## Requirements:

- Install [Node.js](https://nodejs.org/en/download) and [npm](https://www.npmjs.com/package/download)  
- Install [Hardhat](https://www.npmjs.com/package/hardhat) 
- Access to a [Celo testnet node](https://github.com/celo-org/celo-blockchain/blob/master/Dockerfile.celo-node)
- Access to a [Chainlink node](https://docs.chain.link/chainlink-nodes/v1/running-a-chainlink-node/)


## What is Chainlink Keepers? -

**[Chainlink Keepers](https://docs.chain.link/chainlink-automation/introduction/)** is a decentralized service which allows developers to reliably automate regular Smart Contract triggers without the resources and risks associated with performing keeper operations manually or through centralized systems. Because Keepers automates key time and event-based smart contract functions, it frees developers to focus on building new use cases across industries like DeFi, insurance, gaming and NFT art.

Chainlink Keepers works by using external adapters to monitor events on various external data sources. When an event occurs, the adapter triggers the Smart Contract which then executes the specific function. This process is completely automated and does not require any manual intervention.

Chainlink Keepers is useful for applications that require the execution of certain functions at specific intervals or when certain conditions are met. For example: a Smart Contract that requires a certain action to be taken when the price of an asset reaches a certain threshold can be automated using Chainlink Keeper.

## Use Cases of Chainlink Keepers:

**[Celo](https://docs.celo.org/learn/celo-overview)** is a mobile-first blockchain platform that focuses on financial inclusion. Thus, by integrating Chainlink Keepers with Celo, developers can create more efficient and robust Smart Contracts that can be triggered automatically. This can help to reduce costs and increase the overall efficiency of the platform.

Chainlink Keepers can also be used to automate certain functions in Celo's governance system like triggering a vote when a certain condition is met. This can help to make the governance process more transparent and efficient.

Some important use cases for Chainlink Keepers include:

1. **Automated market-making:** Chainlink Keepers can be used to automate the re-balancing of a liquidity pool. This ensures that the pool remains balanced and that traders are always able to execute trades at a fair price.

2. **Contract maintenance:** It can be used to perform routine maintenance tasks on Smart Contracts. For example; they can update contract parameters or check for security vulnerabilities.

3. **Decentralized finance (DeFi) applications:** They can be used to automate the execution of complex financial transactions in DeFi applications. This can help to reduce the risk of human error and ensure that transactions are executed in a timely and efficient manner.

4. **Decentralized autonomous organizations (DAOs):** They can be used to automate the governance processes of DAOs. For example: they can be used to automatically trigger a vote when a proposal meets certain conditions.

5. **Gaming:** It can be used to automate game logic in blockchain-based games. For example: they can be used to trigger certain events when certain conditions are met like when a player completes a level or reaches a certain score.

## Setting up your Environment:

To get started, you will need to set up your development environment. Here are the steps you need to follow:

1. Install [Node.js](https://nodejs.org/en/download) and [npm](https://www.npmjs.com/package/download) on your system.
2. Install [Hardhat](https://hardhat.org/) by running the following command in your terminal:

  ```bash
    npm install --save-dev hardhat
  ```

3. Create a new directory for your project and navigate to it in your terminal.
4. Initialize a new Hardhat project by running the following command:

  ```bash
    npx hardhat
  ```

5. Follow the prompts to set up your project. Choose the options that best suits your needs.

6. Once the project is set up, open it in your favorite code editor.

## Installing Hardhat and Chainlink Libraries:

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
// This module.exports object defines the configuration options for your Hardhat network.
module.exports = {
  // Set the default network to "hardhat".
  defaultNetwork: "hardhat",

  // Define the network configurations.
  networks: {
    // Configuration for the "hardhat" network, which forks from the Celo mainnet for testing/development purposes.
    hardhat: {
      forking: {
        url: "https://forno.celo.org",
      },
    },
    // Configuration for the "celo" network, which uses the Celo mainnet.
    celo: {
      url: "https://forno.celo.org",
      // Specify the mnemonic for the account(s) that will be used for transactions on this network.
      accounts: {
        mnemonic: "<your-mnemonic>",
      },
      // Define the configuration options for the Keeper-compatible contracts.
      keeper: {
        // Set the URL for your Chainlink node.
        url: "https://<your-chainlink-node-url>",
        // Set the address of your KeeperRegistry contract.
        keeperRegistry: "<your-keeper-registry-address>",
      },
    },
  },

  // Define the Solidity compiler configurations.
  solidity: {
    compilers: [
      {
        // Specify the version of the Solidity compiler to use.
        version: "0.8.9",
        settings: {
          optimizer: {
            // Enable the optimizer to optimize the generated bytecode.
            enabled: true,
            // Set the number of optimization runs to perform.
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

import "@chainlink/contracts/src/v0.8/AutomationCompatible.sol";

// Define a contract named KeeperCount that implements the AutomationCompatibleInterface interface
contract KeeperCount is AutomationCompatibleInterface {
  // Define two public state variables of type uint256 named counter and interval
  uint256 public counter;
  uint256 public interval;

  // Define a constructor that takes a uint256 parameter named _interval and sets the interval variable to its value
  constructor(uint256 _interval) {
    interval = _interval;
  }

  // Define a function named checkUpkeep that takes a bytes calldata parameter named checkData and returns a tuple of two values: upkeepNeeded of type bool and performData of type bytes memory
  function checkUpkeep(bytes calldata /* checkData */) external override returns (bool upkeepNeeded, bytes memory /* performData */) {
    // Check if the current timestamp is greater than or equal to the sum of the counter and interval variables, and return a boolean value indicating whether an upkeep is needed
    return (block.timestamp >= counter + interval, "");
  }

  // Define a function named performUpkeep that takes a bytes calldata parameter named performData and updates the counter variable to the current timestamp
  function performUpkeep(bytes calldata /* performData */) external override {
    counter = block.timestamp;
  }
}

```

Let's go through the `KeeperCount` contract together:

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
// Import the ethers module from the Hardhat framework
const { ethers } = require("hardhat");

// Define an async function named main
async function main() {
  // Use the ethers.getContractFactory() method to retrieve the contract factory for the KeeperCount contract
  const KeeperCount = await ethers.getContractFactory("KeeperCount");
  // Use the deploy() method of the contract factory to deploy an instance of the KeeperCount contract with an interval of 3600 seconds (1 hour)
  const keeperCount = await KeeperCount.deploy(3600);
  // Log the address of the deployed contract to the console
  console.log("KeeperCount deployed to:", keeperCount.address);
}

// Call the main function and exit the process with a status code of 0 if it succeeds, or 1 if it fails
main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });

```
The code above is a JavaScript file that uses the Hardhat framework to deploy the `KeeperCount` Smart Contract to the Celo.

The first line imports the `ethers` library from the Hardhat package.

The `main` function is an asynchronous function that deploys the `KeeperCount` contract to the blockchain using the `getContractFactory` method from the `ethers` library. It sets the `interval` variable to 3600, which corresponds to 1 hour. It then logs the address of the deployed contract to the console.

The last few lines of code calls the `main` function and handles any errors that may occur during deployment.

1. Deploy the Smart Contract to the Celo network by running the following command:

  ```bash
    npx hardhat run --network celo scripts/deploy.js
  ```

2. Verify that the smart contract was deployed by checking the output in your terminal. You should see a message similar to the following:

  ```bash
    KeeperCount deployed to: 0x1234567890123456789012345678901234567890
  ```

## Registering the Keeper with the Keeper Registry:

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

## Testing the Smart Contract with Chainlink Keepers:

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
      "type": "cron", // initiate cron job
      "params": {
        "schedule": "0 */1 * * * *" // execute every minute
      }
    }
  ],
  "tasks": [
    {
      "type": "keeper", // initiate keeper task
      "confirmations": 0, // number of confirmations required
      "params": {
        "contractAddress": "<your-contract-address>", // address of your contract
        "functionSelector": "performUpkeep" // name of the function to execute
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

Congratulations! You have successfully integrated the Chainlink Keepers on Celo blockchain and tested it with a Smart Contract example.

## Conclusion:

Hence, Chainlink Keepers provides a powerful tool for developers to automate the maintenance and upkeep of their smart contracts. By leveraging off-chain computing resources, developers can ensure that their Smart Contracts remain operational and secure without the need for manual intervention.

In this tutorial, we have explored how to integrate Chainlink Keepers on the Celo blockchain using Hardhat. We began by setting up our development environment and deploying a sample smart contract. We then proceeded to create a Chainlink node and configure it to communicate with our Celo blockchain node.

We then demonstrated how to create a Chainlink Keeper job definition that executes a function on our smart contract at regular intervals. This allows for automated upkeep and maintenance of the smart contract without the need for manual intervention.

