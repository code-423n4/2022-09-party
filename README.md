# Contest Details

- $71,250 USDC main award pot
- $3,750 USDC gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-09-party-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts September 12, 2022 20:00 UTC
- Ends September 19, 2022 20:00 UTC

[ ⭐️ SPONSORS ADD INFO HERE ]

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

TODO: Light intro to product design and contract architecture.

| Contract Name | LoC | Libraries | External Calls | Tags |
|---------------|---------------|-----------|----------------|------|
| [`crowdfund/AuctionCrowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/AuctionCrowdfund.sol)                  | 200 |          | IERC721, [PartyBidV1 Market Wrappers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/market-wrapper)                | Proxy Impl, Delegatecall |
| [`crowdfund/BuyCrowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/BuyCrowdfund.sol)                  | 77  |          | IERC721 | Proxy Impl |
| [`crowdfund/BuyCrowdfundBase.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/BuyCrowdfundBase.sol)              | 132 |          | Arbitrary calls, ERC721 | Abstract, Arbitrary calls |
| [`crowdfund/CollectionBuyCrowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/CollectionBuyCrowdfund.sol)        | 94  |          | IERC721 | Proxy Impl |
| [`crowdfund/Crowdfund.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/Crowdfund.sol)            | 369 |          | IERC721, Globals, PartyFactory | Abstract, Accounting, Admin functions, Assembly, ETH balance, ETH transfer, Payable |
| [`crowdfund/CrowdfundFactory.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/CrowdfundFactory.sol)     | 104 |          | Arbitrary calls, [Gatekeepers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/gatekeepers), Globals,  Proxy                | Arbitrary calls, Proxy Factory |
| [`crowdfund/CrowdfundNFT.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/crowdfund/CrowdfundNFT.sol)         | 139 | solmate  | Globals, [Renderers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/renderers) | Soulbound ERC721 |
| [`distribution/TokenDistributor.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/distribution/TokenDistributor.sol)       | 360 |          | IERC20, Party | Abstract, Accounting, Admin functions, Assembly, ERC20 balance, ETH balance, ERC20 transfer, ETH transfer, Honeypot, Singleton |
| [`globals/Globals.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/globals/Globals.sol)                     | 78  |          |                | Configuration Registry, Admin-only |
| [`party/Party.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/Party.sol)                         | 39  |          |                | Proxy Impl |
| [`party/PartyFactory.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/PartyFactory.sol)                  | 47  |          | Proxy, Globals | Proxy Factory |
| [`party/PartyGovernance.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/PartyGovernance.sol)               | 853 |          | IERC20, TokenDistributor | Abstract, Admin functions, Assembly, Delegatecall, ETH balance, Fallback, Governance, Payable, Roles, Snapshots |
| [`party/PartyGovernanceNFT.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/party/PartyGovernanceNFT.sol)            | 150 | solmate | Globals, [Renderers](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/renderers) | Abstract, ERC721, Minting |
| [`proposals/ArbitraryCallsProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ArbitraryCallsProposal.sol)    | 199 | | Arbitrary calls, IERC721 | Abstract, Arbitrary calls, Assembly, Decoding, Delegatecall target, ETH transfer |
| [`proposals/FractionalizeProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/FractionalizeProposal.sol)     | 62  |  |  | Abstract, Decoding, Delegatecall target, [Fractional V1 Vault Factory](https://etherscan.io/address/0x85Aa7f78BdB2DE8F3e0c0010d99AD5853fFcfC63#code), IERC721 |
| [`proposals/LibProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/LibProposal.sol)               | 38  |          |                | Library |
| [`proposals/ListOnOpenseaProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ListOnOpenseaProposal.sol) | 298 |          | IERC721, [Seaport 1.1](https://etherscan.io/address/0x00000000006c3852cbEf3e08E8dF289169EdE581#code)               | Abstract, Assembly, Decoding, Delegatecall target, Memory Hack, Multi-Step |
| [`proposals/ListOnZoraProposal.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ListOnZoraProposal.sol)        | 163 |          | IERC721, [Zora Auction House V1](https://etherscan.io/address/0xE468cE99444174Bd3bBBEd09209577d25D1ad673#code)               | Abstract, Decoding, Delegatecall target, Revert Handling, Multi-Step  |
| [`proposals/ProposalExecutionEngine.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ProposalExecutionEngine.sol)   | 214 |          |                | Assembly, Decoding, Delegatecall target, Stateful, Storage, Upgradable |
| [`proposals/ProposalStorage.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/proposals/ProposalStorage.sol)           | 55  |          |                | Abstract, Assembly, Delegatecall, Delegatecall target, Storage |
| [`tokens/ERC1155Receiver.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/tokens/ERC1155Receiver.sol)              | 19  | solmate  |                | Abstract, EIP165, ERC1155 |
| [`tokens/ERC721Receiver.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/tokens/ERC721Receiver.sol)               | 28  | solmate  |                | Abstract, EIP165, ERC721 |
| [`utils/EIP165.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/EIP165.sol)                        | 12  |          |                | Abstract, EIP165 |
| [`utils/Implementation.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/Implementation.sol)                | 26  |          |                | Abstract, Assembly, EVM Hacks |
| [`utils/LibAddress.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibAddress.sol)                    | 14  |          |                | Library, ETH Transfer |
| [`utils/LibERC20Compat.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibERC20Compat.sol)                | 29  |          | IERC20         | Assembly, Decoding, ERC20, Library, Low-Level call |
| [`utils/LibRawResult.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibRawResult.sol)                  | 17  |          |                | Assembly, Library |
| [`utils/LibSafeCast.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibSafeCast.sol)                   | 64  |          |                | Integer Casting, Library |
| [`utils/LibSafeERC721.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/LibSafeERC721.sol)                 | 24  |          | IERC721        | Decoding, ERC721, Library, Low-Level call |
| [`utils/Proxy.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/Proxy.sol)                         | 31  |          | Proxy Impl     | Assembly, Delegatecall, Fallback, Low-Level call, Proxy |
| [`utils/ReadOnlyDelegateCall.sol`](https://github.com/PartyDAO/party-contracts-c4/tree/main/contracts/utils/ReadOnlyDelegateCall.sol)          | 32  |          | Arbitrary calls               | Abstract, Delegatecall, Delegatecall target, Decoding, EVM Hack, Solidity Hack |


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

- Throughout both phases of the product (crowdfund and governance), we rely heavily on external protocols. It’s critical that our integrations with them are correct. The governance proposal contracts (`ListOnOpenseaProposal`, `ListOnZoraProposal`, `ListOnFractionalProposal`) are areas of highest concern because a bad integration there can either cause the loss of an NFT held by the party or can brick the party until the proposal can be canceled.

# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos:
- **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
- **a _findings_ repo**, where issues are submitted (shared with you after the contest)

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest report is published and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

---

# Contest setup

## ⭐️ Sponsor: Provide contest details

Under "SPONSORS ADD INFO HERE" heading below, include the following:

- [x] Create a PR to this repo with the below changes:
- [x] Name of each contract and:
  - [x] source lines of code (excluding blank lines and comments) in each
  - [x] external contracts called in each
  - [x] libraries used in each
- [x] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [x] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
- [x] Describe anything else that adds any special logic that makes your approach unique
- [x] Identify any areas of specific concern in reviewing the code
- [x] Add all of the code to this repo that you want reviewed


---

# Contest prep

## ⭐️ Sponsor: Contest prep
- [x] Provide a self-contained repository with working commands that will build (at least) all in-scope contracts, and commands that will run tests producing gas reports for the relevant contracts.
- [x] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [x] Modify the bottom of this `README.md` file to describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. ([Here's a well-constructed example.](https://github.com/code-423n4/2021-06-gro/blob/main/README.md))
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 24 hours prior to contest start time.**
- [x] Be prepared for a 🚨code freeze🚨 for the duration of the contest — important because it establishes a level playing field. We want to ensure everyone's looking at the same code, no matter when they look during the contest. (Note: this includes your own repo, since a PR can leak alpha to our wardens!)
- [ ] ~~Promote the contest on Twitter (optional: tag in relevant protocols, etc.)~~
- [ ] ~~Share it with your own communities (blog, Discord, Telegram, email newsletters, etc.)~~
- [ ] ~~Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.~~
- [ ] Delete this checklist and all text above the line below when you're ready.
