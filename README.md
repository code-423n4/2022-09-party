**NOTE:** The code for this contest is located [here](https://github.com/PartyDAO/party-contracts-c4).

# Contest Details

- $71,250 USDC main award pot
- $3,750 USDC gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-09-party-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts September 12, 2022 20:00 UTC
- Ends September 19, 2022 20:00 UTC

## Resources

- [Code](https://github.com/PartyDAO/party-contracts-c4)
- [Documentation](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs)
  - [Overview](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs/overview.md)
  - [Crowdfund Contracts Documentation](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs/crowdfund.md)
  - [Governance Contracts Documentation](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs/governance.md)

## Layout

```
docs/ # Start here
├── overview.md
├── crowdfund.md
└── governance.md
contracts/
│   # Used during the crowdfund phase
├── crowdfund/
│   ├── AuctionCrowdfund.sol
│   ├── BuyCrowdfund.sol
│   ├── CollectionBuyCrowdfund.sol
│   ├── CrowdfundFactory.sol
│   ├── Crowdfund.sol
│   └── CrowdfundNFT.sol
├── gatekeepers/
│   ├── AllowListGateKeeper.sol
│   └── TokenGateKeeper.sol
├── globals/
│   └── Globals.sol
│   # Used during the governance phase
├── party/
│   ├── Party.sol
│   ├── PartyFactory.sol
│   ├── PartyGovernance.sol
│   └── PartyGovernanceNFT.sol
├── proposals/
│   ├── ProposalExecutionEngine.sol
│   ├── ArbitraryCallsProposal.sol
│   ├── FractionalizeProposal.sol
│   ├── ListOnOpenseaProposal.sol
│   └── ListOnZoraProposal.sol
├── distribution/
│   └── TokenDistributor.sol
|   # Used to render crowdfund and governance NFTs
└── renderers/
    ├── CrowdfundNFTRenderer.sol
    └── PartyGovernanceNFTRenderer.sol
sol-tests/ # Foundry tests
tests/ # TS tests
```

![contract lifecycle](./contract-lifecycle.png)

## Contest Scope

| Contract Name                                                                                                                                       | LoC | Libraries | External Calls                                                                                                                 | Tags                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | --- | --------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`crowdfund/AuctionCrowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/AuctionCrowdfund.sol)               | 200 |           | IERC721, [PartyBidV1 Market Wrappers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/market-wrapper)       | Proxy Impl, Delegatecall                                                                                                                                      |
| [`crowdfund/BuyCrowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/BuyCrowdfund.sol)                       | 77  |           | IERC721                                                                                                                        | Proxy Impl                                                                                                                                                    |
| [`crowdfund/BuyCrowdfundBase.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/BuyCrowdfundBase.sol)               | 132 |           | Arbitrary calls, ERC721                                                                                                        | Abstract, Arbitrary calls                                                                                                                                     |
| [`crowdfund/CollectionBuyCrowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/CollectionBuyCrowdfund.sol)   | 94  |           | IERC721                                                                                                                        | Proxy Impl                                                                                                                                                    |
| [`crowdfund/Crowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/Crowdfund.sol)                             | 369 |           | IERC721, Globals, PartyFactory                                                                                                 | Abstract, Accounting, Admin functions, Assembly, ETH balance, ETH transfer, Payable                                                                           |
| [`crowdfund/CrowdfundFactory.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/CrowdfundFactory.sol)               | 104 |           | Arbitrary calls, [Gatekeepers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/gatekeepers), Globals, Proxy | Arbitrary calls, Proxy Factory                                                                                                                                |
| [`crowdfund/CrowdfundNFT.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/CrowdfundNFT.sol)                       | 139 | solmate   | Globals, [Renderers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/renderers)                             | Soulbound ERC721                                                                                                                                              |
| [`distribution/TokenDistributor.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/distribution/TokenDistributor.sol)         | 360 |           | IERC20, Party                                                                                                                  | Abstract, Accounting, Admin functions, Assembly, ERC20 balance, ETH balance, ERC20 transfer, ETH transfer, Honeypot, Singleton                                |
| [`globals/Globals.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/globals/Globals.sol)                                     | 78  |           |                                                                                                                                | Configuration Registry, Admin-only                                                                                                                            |
| [`party/Party.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/Party.sol)                                             | 39  |           |                                                                                                                                | Proxy Impl                                                                                                                                                    |
| [`party/PartyFactory.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/PartyFactory.sol)                               | 47  |           | Proxy, Globals                                                                                                                 | Proxy Factory                                                                                                                                                 |
| [`party/PartyGovernance.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/PartyGovernance.sol)                         | 853 |           | IERC20, TokenDistributor                                                                                                       | Abstract, Admin functions, Assembly, Delegatecall, ETH balance, Fallback, Governance, Payable, Roles, Snapshots                                               |
| [`party/PartyGovernanceNFT.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/PartyGovernanceNFT.sol)                   | 150 | solmate   | Globals, [Renderers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/renderers)                             | Abstract, ERC721, Minting                                                                                                                                     |
| [`proposals/ArbitraryCallsProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ArbitraryCallsProposal.sol)   | 199 |           | Arbitrary calls, IERC721                                                                                                       | Abstract, Arbitrary calls, Assembly, Decoding, Delegatecall target, ETH transfer                                                                              |
| [`proposals/FractionalizeProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/FractionalizeProposal.sol)     | 62  |           |                                                                                                                                | Abstract, Decoding, Delegatecall target, [Fractional V1 Vault Factory](https://etherscan.io/address/0x85Aa7f78BdB2DE8F3e0c0010d99AD5853fFcfC63#code), IERC721 |
| [`proposals/LibProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/LibProposal.sol)                         | 38  |           |                                                                                                                                | Library                                                                                                                                                       |
| [`proposals/ListOnOpenseaProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ListOnOpenseaProposal.sol)     | 298 |           | IERC721, [Seaport 1.1](https://etherscan.io/address/0x00000000006c3852cbEf3e08E8dF289169EdE581#code)                           | Abstract, Assembly, Decoding, Delegatecall target, Memory Hack, Multi-Step                                                                                    |
| [`proposals/ListOnZoraProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ListOnZoraProposal.sol)           | 163 |           | IERC721, [Zora Auction House V1](https://etherscan.io/address/0xE468cE99444174Bd3bBBEd09209577d25D1ad673#code)                 | Abstract, Decoding, Delegatecall target, Revert Handling, Multi-Step                                                                                          |
| [`proposals/ProposalExecutionEngine.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ProposalExecutionEngine.sol) | 214 |           |                                                                                                                                | Assembly, Decoding, Delegatecall target, Stateful, Storage, Upgradable                                                                                        |
| [`proposals/ProposalStorage.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ProposalStorage.sol)                 | 55  |           |                                                                                                                                | Abstract, Assembly, Delegatecall, Delegatecall target, Storage                                                                                                |
| [`tokens/ERC1155Receiver.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/tokens/ERC1155Receiver.sol)                       | 19  | solmate   |                                                                                                                                | Abstract, EIP165, ERC1155                                                                                                                                     |
| [`tokens/ERC721Receiver.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/tokens/ERC721Receiver.sol)                         | 28  | solmate   |                                                                                                                                | Abstract, EIP165, ERC721                                                                                                                                      |
| [`utils/EIP165.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/EIP165.sol)                                           | 12  |           |                                                                                                                                | Abstract, EIP165                                                                                                                                              |
| [`utils/Implementation.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/Implementation.sol)                           | 26  |           |                                                                                                                                | Abstract, Assembly, EVM Hacks                                                                                                                                 |
| [`utils/LibAddress.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibAddress.sol)                                   | 14  |           |                                                                                                                                | Library, ETH Transfer                                                                                                                                         |
| [`utils/LibERC20Compat.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibERC20Compat.sol)                           | 29  |           | IERC20                                                                                                                         | Assembly, Decoding, ERC20, Library, Low-Level call                                                                                                            |
| [`utils/LibRawResult.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibRawResult.sol)                               | 17  |           |                                                                                                                                | Assembly, Library                                                                                                                                             |
| [`utils/LibSafeCast.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibSafeCast.sol)                                 | 64  |           |                                                                                                                                | Integer Casting, Library                                                                                                                                      |
| [`utils/LibSafeERC721.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibSafeERC721.sol)                             | 24  |           | IERC721                                                                                                                        | Decoding, ERC721, Library, Low-Level call                                                                                                                     |
| [`utils/Proxy.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/Proxy.sol)                                             | 31  |           | Proxy Impl                                                                                                                     | Assembly, Delegatecall, Fallback, Low-Level call, Proxy                                                                                                       |
| [`utils/ReadOnlyDelegateCall.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/ReadOnlyDelegateCall.sol)               | 32  |           | Arbitrary calls                                                                                                                | Abstract, Delegatecall, Delegatecall target, Decoding, EVM Hack, Solidity Hack                                                                                |

## Inheritance Graph

Here's an abbreviated inheritance graph of the major contracts in the protocol (leaf nodes are deployable):

```
                              ┌─────►AuctionCrowdfund
                              │
CrowdfundNFT─────►Crowdfund───┤                           ┌─────►BuyCrowdfund
                              │                           │
                              └─────►BuyCrowdfundBase─────┤
                                                          │
                                                          └─────►CollectionBuyCrowdfund



PartyGovernance──────►PartyGovernanceNFT──────►Party




ListOnOpenseaProposal────┐
                         │
ListOnZoraProposal───────┤
                         ├─────►ProposalExecutionEngine
FractionalizeProposal────┤
                         │
ArbitraryCallsProposal───┘
```

## Areas of Concern / Unique Approaches

### Dependencies on External Protocols

Throughout both phases of the product (crowdfund and governance), we rely heavily on external protocols. It's critical that our integrations with them are correct. The governance proposal contracts (`ListOnOpenseaProposal`, `ListOnZoraProposal`, `ListOnFractionalProposal`) are areas of highest concern because a bad integration there can either cause the loss of an NFT held by the party or can brick the party until the proposal can be canceled.

### `delegatecall`'s on the `ProposalExecutionEngine`

The `ProposalExecutionEngine` implements all the logic with parsing and executing proposals passed by `PartyGovernance`. In addition to this it is stateful, reading and writing to storage slots shared with `PartyGovernance` and also utilizing its own "private" storage slots. Low-level storage operations are used to ensure these regions of storage are predictable and do not overlap.

### Unconventional Reentrancy Guards

To save gas, we do not use traditional reentrancy guard modifiers anywhere in our protocol. Instead, we try to make use of some existing state variables already being touched to prevent reentrancy. That, or we simply allow reentrancy in places that we've decided are low-risk. These assumptions should be tested.

### Voting Power Accounting

The `PartyGovernance` contract creates a record of voting power for members of the party (and delegates) every time a governance NFT is moved or delegation is changed. We search these records during voting to ensure members cannot game proposals by voting with voting power earned after voting begins. It's important to have high confidence in this accounting logic to ensure malicious proposals cannot be passed without consensus.

### Ruggability by Governance

A major goal that runs through the protocol design is to protect governance parties from unfairly losing the NFT they formed the party around. We call these NFTs "preciouses," and we have logic that restricts the way parties can interact with these NFTs to prevent them from being moved, or having the potential to be moved, without passing a rigorous (sometimes unanimous) governance process. For example, to list a precious NFT for sale on Opensea, it must first go through a Zora auction to mitigate a malicious whale with voting power from listing it for far below floor price and buying it themselves. We want to be sure these safeguards are effective for the majority of NFTs.

### `TokenDistributor`

The `TokenDistributor` is a single, canonical contract that's used across all governance parties. It custodies any ETH or ERC20 that a party transfers into it when creating a distribution. As such, it is a major honeypot for potential exploits. Also, anyone (not just official governance parties) can create a distribution on the `TokenDistributor`, and the creator of a distribution can dictate how funds within that distribution are split. Because of these properties, funds from each distribution must be isolated from the other (no distribution can transfer more than their initial deposit).

### Multi-Step Proposals

There are some proposals that can take multiple executions to complete (eg. `ListOnZoraProposal`), as opposed to proposals that are completed in one transaction like it commonly works in other governance implementations. While a multi-step proposal is in progress, no other proposals can be executed until it is finished. There is support for canceling proposals should they get "stuck" for any reason.

### Off-Chain Storage

The [off-chain storage](https://github.com/Dragonfly-Capital/useful-solidity-patterns/tree/main/patterns/off-chain-storage) pattern is used across almost all contracts to drastically reduce the gas costs involved in reading/writing storage. We verify the data coming off-chain is correct by checking it against an on-chain hash of the data we expect.

### Storage Buckets

The [explicit storage buckets](https://github.com/Dragonfly-Capital/useful-solidity-patterns/tree/main/patterns/explicit-storage-buckets) pattern is used in both the `PartyGovernance` and `ProposalExecutionEngine` implementation. Instead of relying on the compiler to assign/access these storage buckets, we manually define pointers that explicitly map to the storage slot of our choosing that does not overlap with any automatically assigned slot.

### Read-Only Delegate Calls

In places where we want to make sure `delegateCall`ing does not alter state (is read-only), we use a custom `_readOnlyDelegateCall()` function. It works by `delegateCalling`ing on a contract but always reverting with the return data than using a try/catch statement to bubble up the result to return.

### Unconventional Reinitialization Guards

We do not use any explicit state to indicate that a proxified contract has been initialized before (to prevent re-initialization attacks). Because all our initialization logic runs inside constructors, we simply check that our address has no code in it.

### Upgradeability Risks

There are two different upgrade models at play in the protocol. One is through the `Global` registry contract, which other contracts will use to look up the latest instance (address) of a contract. Often this is done just-in-time, such as looking up the `PartyFactory` when a crowdfund has won and is transitioning to the governance phase. This registry is also used to look up the latest implementation contract for `Proxy` instances when deploying new crowdfunds or governance parties. The PartyDAO multisig (which controls the `Globals` contract) has the ability to unilaterally change the addresses pointed to in these cases. The other upgrade mechanism is voluntary, occuring when a governance party passes a proposal to upgrade its `ProposalExecutionEngine` implementation to the latest version (also looked up in `Globals`). In either case, publishing a contract that is not backwards compatible with existing crowdfund and governance instances can brick them.

## Known Issues / Topics

- It is possible that someone could manipulate parties by contributing ETH and then buying their NFT that they own. This is known and not considered a bug or a valid finding by the team.
- For `PartyBuy` and `PartyCollectionBuy` crowdfunds, the contract allows arbitrary calls via the `buy()` method to buy the NFT and check if the NFT is owned by the contract at the end. A potential attack here happens if the crowdfund raises more than the buy price (or if the seller reduces the price). An attacker can then write a contract that when called with the crowdfunds entire ETH balance, buys the NFT for less and sends it to the crowdfund contract, then sends the remaining ETH to the attacker. This behavior exists in V1 as well. In V1, we used an allow list to help mitigate. The issue with this is that a motivated actor could still buy the original listing and create a new one on an allowed target then trigger the party to `buy()` that one instead at a higher price, pocketing the difference. We have made peace with this issue and accepted the risk, but the team is open to new solutions.
  - `PartyCollectionBuy` will be much less likely to be affected by this since only a host may call `buy()`.
  - On the frontend, we have thought about notifying contributors whose contribution would push the crowdfund above the buy price to reduce their contribution. Another solution is to cap contributions to `maximumPrice`, but we'd prefer to do this on the frontend.
- For `PartyBid` crowdfunds, in the case that a party did not bid at all on the NFT in the auction yet still (somehow) manages to acquire the NFT before `finalize()` is called, all contributions to the crowdfund are considered used so that everyone who contributed wins but no contributions will be refunded back. The ETH contribution would stay in the crowdfund and not be transferred over to the created `Party` instance, effectively burned. The crowdfund could transfer over contributions to the created `Party` to `distribute()` back (refunding it) but this introduces the possibility for someone to make a last minute contribution before `finalize()` is called to boost their voting power at no cost because they could get back all their contributions. This is a rare and atypical enough case that we feel comfortable leaving this behavior alone.
- In `_settleZoraAuction()` in `ListOnZoraProposal`, a try/catch statement is used to get the state of an auction. If the `endAuction()` call fails but returns an `"Auction doesn't exit"` we take this as meaning someone else had called `endAuction()` before we did, ending the auction and emitting a `ZoraAuctionSold` event. There is a possibility that a `safeTransferFrom()` call in Zora's `endAuction()` reverts at `onERC721Received()` with a `"Auction doesn't exit"` to trick the party into completing the proposal even though the auction wasn't settled. However, the party still has the NFT and can just list it elsewhere. This is a known grief and, unless there can be more serious implications, we do not consider it a valid finding.
- If a party were to list a malicious NFT (eg. reverts on transfer after listing), somewhere along the way it may break the proposal flow and put the party in a stuck state until `cancelDelay` is reached. While it is annoying, we do not consider it serious because (1) the proposal can always be canceled and (2) it is unlikely a malicious NFT will have a market.
- By controlling the `Globals` registry contract, it’s understood that the PartyDAO multisig has a lot of power over the protocol and could cause harm in various ways by updating the Globals contract maliciously or incorrectly. On top of this, there are emergency admin recovery functions on governance parties and the token distributor callable by the multisig that can execute arbitrary bytecode, though party hosts can disable them on governance parties.
- Party hosts have unilateral veto power on any proposal. Hosts can essentially block a governance party in this way. Therefore crowdfunds must be extremely careful with their host selection. We accept these risks, given that the PartyDAO multisig is comprised of several different members, all of whom have signed legal agreements to abide by the DAO's governance system.
- Because voting power is represented by governance NFTs proportional to their (used) crowdfund contribution, it limits the ways voting power can be distributed across party members. The lack of quorum or "no" votes can amplify this situation. For example, if someone contributed 51% of the ETH to a crowdfund and the passing threshold for that governance party is also 51%, whoever holds that governance NFT will always be able to pass proposals unless a host vetoes them.
- Canceling an `InProgress` proposal (mid-step) can leave the governance party in a vulnerable or undesirable state because there is no cleanup logic run during a cancel. For example, if a party cancels a Zora proposal while the Zora auction is active, the party will no longer possess the NFT (because Zora is custodial), and must either wait for the auction to conclude or execute an arbitrary call to cancel the action (directly on Zora) in order to retrieve it.

## License

This code is provided under the [Beta Software License Agreement](https://github.com/PartyDAO/party-contracts-c4/blob/main/LICENSE.pdf).
