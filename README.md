# Web3-Full-Stack-Hiring

Hello! If you're reading this, you applied to a Full Stack Engineering role at Syndicate. This is Syndicate's hiring test for Full Stack engineers. (Note: If you have not applied but stumbled across this repository somehow, you are welcome to check out our [job postings](https://www.notion.so/syndicateprotocol/Full-Stack-Software-Engineer-db5887b717b94d8e8eb80748ae9b9d97).)

When you fork this repository, you should make your fork **private** and share it with [wpapper](https://github.com/wpapper) on Github with an admin role. By forking this repository, you agree to keep the MIT License intact and assign the MIT License to your fork as well.

## Project Description

In this repository, you will create a Web3 integration to look up balances in a smart contract known as Dai. Don't worry if you haven't worked with Web3 before, we'll have plenty of examples and guidance!

[Dai](https://community-development.makerdao.com/en/faqs/dai/) is a cryptocurrency known as a stablecoin. It's useful for buying goods and services on cryptocurrency networks -- you use it just like you'd use regular money. Because Dai is a stablecoin, the value of Dai fluctuates very little. In this case, you can assume that 1 DAI is always equal to 1 US Dollar. Various wallets hold balances of DAI. For example, [this wallet](https://etherscan.io/address/0x5d3a536E4D6DbD6114cc1Ead35777bAB948E3643) may hold 28,837,952 DAI (which, for the purposes of this exercise, we can assume is $28,837,952 US Dollars). (The value of DAI in the wallet will fluctuate, but the underlying principle remains the same.)

Your task is to use React, [the web3.js library](https://web3js.readthedocs.io/en/v1.3.4/) or a [React wrapper](https://github.com/NoahZinsmeister/web3-react/tree/v6/docs#web3-reactcore-api-reference) of your choosing, and some form of styling (we use Tailwind internally, but we understand that you might not have used it before) to create an interface that can query a user's DAI balance on the Ethereum blockchain. Your interface should have:

- An input bar where a user can enter in an Ethereum address
- A display that shows the DAI balance for the entered Ethereum address
- Atleast impressive since you will be working on the user interface

We don't have strong preferences on the styling -- if you are familiar with Bootstrap, Tailwind, or various Gatsby starters, feel free to use those. If you don't have familiarity with existing styling or templates, minimal styling is perfectly fine as well.

Note that Dai does have an [official library](https://www.npmjs.com/package/@makerdao/dai), but we want you to use web3 directly since that is what you'll use if you work at Syndicate. You can feel free to look at the official library for inspiration, but you should not use it to complete the project.

### Primary Task and Optional Additional Tasks

As discussed above, your **primary task** is to produce an interface that has:

- An input bar where a user can enter in an Ethereum address
- A display that shows the DAI balance for the entered Ethereum address. This should be displayed in US Dollars, not `wei`. This is described in more detail in the Helpful Resources section below.
- Atleast impressive since you will be working on the user interface
- Host your app on Heroku or on any other service you have access to and attach a link to the hosted app on your project's README.md file.

If you have extra time available, feel free to show off your strengths! You can style the site, cache the most recent input, or implement any of the following features:

- Displaying the value of DAI in alternative currencies (e.g. the value of DAI when the 1 DAI = $1 US Dollar representation is converted to Euros)
- Querying USDC in addition to DAI (You would use the erc20.js ABI and the USDC contract addresses found in Dai-Web3-Example.js). This is harder because USDC uses six decimals while DAI uses 18. Decimals are described in more detail in the Helpful Resources section below.

There is no need to complete any of these additional tasks, but you're always welcome to do so if you want to highlight an area of expertise.

## Helpful Resources

To query the Ethereum blockchain for the DAI balance, you will want to use [web3.js](https://web3js.readthedocs.io/en/v1.3.4/getting-started.html) or a [React wrapper](https://github.com/NoahZinsmeister/web3-react/tree/v6/docs#web3-reactcore-api-reference) for it. You will need a gateway to access the Ethereum blockchain (Dai refers to this as a provider and has examples [here](https://web3js.readthedocs.io/en/v1.3.4/include_package-core.html?highlight=givenProvider#example)). You can use any of the following gateways:

- The [Cloudflare Ethereum Gateway](https://developers.cloudflare.com/distributed-web/ethereum-gateway/interacting-with-the-eth-gateway). This does not require any API key.
- An [Infura.io gateway](https://infura.io/docs/ethereum). This does require a free API key. The network you'll want is "mainnet".
- A local Ethereum server using [Ganache](https://www.npmjs.com/package/ganache-cli). We already have one set up in [this repository](https://github.com/SyndicateProtocol/Bank-Solidity-Hiring#setup-instructions) that contains the hiring test for Solidity engineers. You can use this by running `npm install -g ganache-cli`, `npm install`, and then `npm start`.
- The [MetaMask Chrome browser extension](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?hl=en), which will automatically provision a gateway for you and make that available to `web3.js`.

The DAI code is hosted by a smart contract located [here](https://etherscan.io/address/0x6b175474e89094c44da98b954eedeac495271d0f). To query it, you will connect to the Ethereum blockchain via a gateway, import the DAI ABI (essentially a file that specifies the available methods) into web3.js, and then use the DAI's [balanceOf](https://docs.makerdao.com/smart-contract-modules/dai-module/dai-detailed-documentation#dai-glossary) method with a user's wallet address to query the DAI smart contract.

We know this can be complicated, so we have already put together a complete example of this process using the tests for our [Solidity Hiring Test](https://github.com/SyndicateProtocol/Bank-Solidity-Hiring) as a reference. [Lines 11 - 20](https://github.com/SyndicateProtocol/Bank-Solidity-Hiring/blob/main/test/Bank.js#L11) as well as line 8 show a complete example of this process. These lines include all of the steps to query a web3 contract. We've copied this file to the repository and renamed it to `Dai-Web3-Example.js`. The abi files referenced are in the `abi/` directory.

When you query the contract, you'll note that the value of the balance in the DAI contract is a lot higher than the balance listed on Etherscan. This is because the DAI contract is represented [in 18 decimals](https://docs.openzeppelin.com/contracts/3.x/erc20#a-note-on-decimals) known as `wei`. You'll want to [convert from wei to ether](https://web3js.readthedocs.io/en/v1.3.4/web3-utils.html#fromwei) to get the proper units.
