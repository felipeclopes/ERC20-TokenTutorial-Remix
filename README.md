# Issue an ERC-20 token with Remix, OpenZeppelin and Metamask

In this step-by-step tutorial you will learn how to issue and play with your own ERC-20 token on Ethereum. This tutorial can be completed by people with no blockchain programming experience and novice programmers.

We will use [Metamask](www.metamask.com) and the online version of [Remix IDE](www.remix.ethereum.org)

By the end of this tutorial you will be able to deploy standard ERC-20 Tokens! Please get your code verified and audited by a 3rd party before releasing any token to the public.

### Preparation

Download and Install [MetaMask](https://metamask.io)

- Install on Chrome, Firefox or Brave Browser
- Create a new account and save your 12 word mnemonic
- Select a test network. The Ropsten Network should work fine.

Get Some Testnet Ether

- Click "Buy" or "Deposit" on Metamask or go to the [Metamask Faucet](https://faucet.metamask.io/) or [Ropsten Faucet](https://faucet.ropsten.be/)
- Hit "Send Me Ether". It should not take long (10-20 seconds)
- Double check Ether was received by hitting the MetaMask Icon

### Use OpenZeppelin for your Smart Contract Implentation

Find Source Code for a Standard ERC-20 Smart Contract. You want a well tested open source implementation such as the official Open Zeppelin implementation.

- Navigate to the [OpenZeppelin Smart Contract Repository] (https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts). Find

OpenZeppelin contain the solidity code you need to deploy your token, as well as useful tools and interfaces for more complex contract implementations. Their Github and documentation is worth a reading id you want to dive deeper into contract concepts.

### Build your Solidity Smart Contract in Remix

- Launch [Remix](http://remix.ethereum.org)

- Enable the "Solidity Compiler" and "Deploy & Run Transactions" Tabs. Find them using the plugin manager on the left.

- Copy the .sol files you need into remix. To create a new .sol file, click the "+" button in the top left. Either copy the code directly from github, or clone the repository and open the local files. e.g.

  ```solidity
  // SPDX-License-Identifier MIT AND GPL-3.0-only
  pragma solidity ^0.8.0;

  import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
  import "@openzeppelin/contracts/access/Ownable.sol";

  contract MyOwnableToken is ERC20, Ownable {
      constructor() ERC20("MyOwnableToken", "MOTK") {
          _mint(msg.sender, 1000 * 10 ** decimals());
      }

      function mint(address to, uint256 amount) public onlyOwner {
          _mint(to, amount);
      }
  }
  ```

- Remix will import all dependencies automatically and create metadata necessary for deployment.

- Try compiling the contract by pressing ctrl-s or pressing the compile button on the compile tab.

- Ensure the contract compiles correctly

- Rename your base file to rename your token e.g. YourTokenName.sol

### Customize your Smart Contract

Now you can personalize the token according to your preferences.

The guides in the [OpenZeppelin docs site](https://docs.openzeppelin.com/contracts) will teach about different concepts, and how to use the related contracts that OpenZeppelin Contracts provides:

- [Access Control](https://docs.openzeppelin.com/contracts/access-control): decide who can perform each of the actions on your system.
- [Tokens](https://docs.openzeppelin.com/contracts/tokens): create tradeable assets or collectives, and distribute them via [Crowdsales](https://docs.openzeppelin.com/contracts/crowdsales).
- [Gas Station Network](https://docs.openzeppelin.com/contracts/gsn): let your users interact with your contracts without having to pay for gas themselves.
- [Utilities](https://docs.openzeppelin.com/contracts/utilities): generic useful tools, including non-overflowing math, signature verification, and trustless paying systems.

### Compiling and Deploying

- Check for errors on remix. Yellow warnings are ok. Red warnings must be fixed before the next step.

- Make sure you are still on the Run tab

- Select YourTokenName in the drop down menu

- Select "Injected Web3" for your environment (Make sure MetaMask is logged in and running)

- Click Deploy

- Approve the transaction on metamask. You may need to enable pop ups on your browser

- Wait for the transaction to mine! Check for confirmation on [EtherScan](https://ropsten.etherscan.io/). You can click on your latest transaction in metamask.

- After the transaction has mined, click the contract address and copy it

- Paste it into the Tokens sectionin Metamask

**You have now issued your first Token. Great Work! This is just the tip of the iceberg.**

## Notes

- Gas price should auto update. For live Eth use https://ethgasstation.info/

## Optional - Register and Verify

Now we are going to register this contract. To do this:

- Using Etherscan: In the Overview Tab → Click on the Contract Address

- Go to the Contract Code Tab → Click Verify and Publish

- Make sure to install Flattener plugin and flatten your code (so it includes all the imports)

- On Etherscan select single file and MIT license

### Words of Wisdom: Get it right once or get it wrong forever.

- Be sure that the contract address field corresponds to the contract address that you have just deployed.
  _Remember contract address is different to your public key_

- The contract name has to match the one in the code.

- Enter the correct compiler version. At the time of writing, this is `Compiler: 0.8.7+commit.e28d00a7`
  _In future builds, this can be found by hitting the Details tab under Compile, and selecting the Compiler dropdown under MetaData._

- On Optimisation, choose **No**.

- On ENTER THE SOLIDITY CONTRACT CODE BELOW, copy the flattener output code from Remix, and paste in that area.

- Leave the other fields in blank and click on Verify and Publish.

**If you get a success! It worked.**

To confirm that it worked, go to https://ropsten.etherscan.io/ and look up your metamask address. Hit the **View Tokens** dropdown to see if you tokens are in there.

## Sending Tokens

Send some to your neighbours:

- In Metamask Open the menu and click "Add Tokens"

- Click Add Custom Token and Input your Contract Address. Your token details should appear automatically

- You should now see your token balance. Try sending some tokens to your friend's address Check Etherscan for progress

- Your friend can then enter your contract info and code to view your tokens in their wallet!
