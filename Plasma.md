# Plasma and Raiden Network

Janice Ng, October 2018



## Raiden Network

- Off-chain scaling solution that is compatible with ERC-20 token transfers in  *bidirectional*
  payment channels (permit funds to flow in both directions along the channel)

- Bidirectional payment channels allow for nearly unlimited token transfers
  between 2 participants as long as their net sum does not exceed initial deposit
  amount

- Interacting with Raiden: developers interact with API to build scalable applications 

- Designed to provide near-instant payments, increase transaction privacy, micropayments, low fees and atomic token swaps 

  - Payment channels exist off-chain + sometimes on-chain 
  - Reduces on-chain transaction capacity 

- Does not need for global consensus of the state of the network required for on-chain transactions 

  - Uses hash-locked transfers called “balance proofs”

    - “Balance Proofs” = collateralized by on-chain deposits that are made 

      before setting up bidirectional payment channels 

**Example of Raiden Network: Raidos**

- Research and planning phase 
- Sidechain technology to generalise state channels 
  - Generalized state channels can be used to implement arbitrary state machines which allow Ethereum’s computational capabilities to scale through satellite chains, which can host any smart contract 
    - State Channels: Transactions take place entirely off the blockchain and exclusively  between the participants, meaning they are cheap and very fast to execute compared to on-chain payments. 

## Plasma

- Series of contracts that run on top of a root chain
- Consist of a network of “child chains” (side-chains) connected to a root chain
  - Each child chain functions as its own blockchain with own consensus
- Process of utilizing Plasma conceptually work by: 
  - Smart contracts created on the root chain and act as the child chain’s anchor to root chain 
  - Child chain is created that functions as its own blockchain with its own consensus (something like PoS) 
  - All states within child chain are enforced with  *fraud proofs* t  hat ensure all state transitions are valid + enforce the protocol for funds withdrawal 
  - Smart contracts specific to that Dapp or child chain can be deployed to child chain 
  - Necessary assets can be transferred from the root chain to child chain 
- dAPP running on child chain does not have to  *interact*  with root chain 
  - Can withdraw assets to the root-chain whenever they want 
  - Exits from child chain allow users to safely retain their funds through Merkle proof through verifying ownership of specified amount of funds 

**Benefits of Plasma**

- Ability to substantially alleviate the computation that is currently congesting the main chain 
- Lower processing and storage requirements 

Disadvantages of Plasma

- Concept of “ *mass exits”*  from the child chains 
- Coordinated simultaneous exit from the child chain may potentially result in a  *lack* of processing capacity to withdraw all the funds. As a result, users *could lose funds*. 

## **Plasma Cash**

- Construction that gives tokens on the network unique serial numbers to unique coins 

- Benefits 

  - No need for confirmations, more straightforward support for all kinds of tokens + mitigation against child chain mass exists (OmiseGo is an example)

  - Plasma Cash utilizes unique identifiers when depositing ETH into a Plasma 

    contract that allows users to only store information about their coin 

**Example: OmniseGo**

- A white-label eWallet, smart contract platform and ERC-20 token built on Plasma 

- Working on a proof of concept for Plasma Cash and Loom is planning on using Plasma Cash to facilitate Plasma Exits for their dappchains 

- Uses PoS algorithm 

- Decentralized bank, exchange, and asset-backed blockchain getaway 

- Goal 

  - Help unbanked get banking services (those who have no access to financial services) 
  - Build fully decentralized P2P system to enable “asset agnostic” value exchange in real time on an Ethereum-based blockchain 
  - Wants decentralized wallet development + ability to send funds across networks 

- Launched own mainnet; allows users to send, receive and exchange any currency or crypto 

  - Use SDK which allows any organization which issues some unit of value (currency/cryptocurrency) to create their own branded wallets which interact with OMG network, which facilitates the swapping of currencies by bonding ETH to the Smart Contract 
    - EG: If Alice wants Bob to send him US dollars, but Alice only has RMB, Alice can send RMB which will be traded for ETH, and sent to Bob in US Dollars 

- Allow people and businesses to send and receive payment in any currency 

  - Based on ERC-20 = recognised smart contract code functions across Ethereum ecosystem 

  - Allow to transfer token data (supply, balance) 

    

    
