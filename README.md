# Party DAO Contest Details

- $71,250 USDC main award pot
- $3,750 USDC gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-09-party-dao-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts September 12, 2022 20:00 UTC
- Ends September 19, 2022 20:00 UTC

### 🚨🚨🚨🚨 The code and docs for this contest are located in a separate [[PartyDAO Protocol Repo]](https://github.com/PartyDAO/party-contracts-c4). 🚨🚨🚨🚨

## Resources

- [Code](https://github.com/PartyDAO/party-contracts-c4)
- [Protocol Documentation](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs)
  - [Overview](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs/overview.md)
  - [Crowdfund Contracts Documentation](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs/crowdfund.md)
  - [Governance Contracts Documentation](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs/governance.md)

## Scoping Intake Details

- Number of non-library contracts in scope: 46
- Number of library dependencies: 1
- Number of structs in scope: 34
- Number of interfaces in scope: 15
- Number of external calls: 4+
    - Seaport 1.1, Zora V1, Fractional V1, PartyBid V1 MarketWrappers, user-supplied arbitrary calls, arbitrary ERC20s and ERC721s.
- Codebase uses mostly inheritance.
- Total in-scope SLOC: 3995
- No oracles used.
- No unique curve logic or math models.
- It is not an AMM.
- It is not a fork of a popular project.
- It does not use rollups.
- It does not implement an ERC20 token.
- Some contracts are NFTs (ERC721).
- It relies on time-based logic.
- It is not multi-chain.
- It does not use a side-chain.
- Preferred communication timezone: EDT or PDT

## All-in-one command

Here's an example one-liner to immediately get started with the codebase. It will clone the project, build it, run every test, and display gas reports (except that the TS tests do not have a gas report since they only use waffle).

```bash
export FORK_URL='<your_alchemy_mainnet_url_goes_here>' && rm -Rf party-contracts-c4 || true && git clone https://github.com/PartyDAO/party-contracts-c4 && cd party-contracts-c4 && nvm install 16.0 && foundryup && forge install && yarn -D && yarn build:sol && yarn test:ts && yarn test:gas && forge test -m testFork --fork-url $FORK_URL --gas-report
```

Refer to the [code repo README](https://github.com/PartyDAO/party-contracts-c4) for targeted, individual test commands you can run.

## Slither Issue

Note that slither does not seem to be working with the repo as-is 🤷, resulting in an enum type not found error:

```
slither.solc_parsing.exceptions.ParsingError: Type not found enum Crowdfund.CrowdfundLifecycle
```

Seems to be related to https://github.com/crytic/slither/pull/1300, which will be included in the 0.8.4 release.

There's mixed success with running slither against individual files.

## Code Repo Layout

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


## Contest Scope

### Files in scope
|File|[SLOC](#nowhere "(nSLOC, SLOC, Lines)")|[Coverage](#nowhere "(Lines hit / Total)")|
|:-|:-:|:-:|
|_Contracts (20)_|
|[contracts/utils/EIP165.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/EIP165.sol)|[11](#nowhere "(nSLOC:6, SLOC:11, Lines:17)")|[0.00%](#nowhere "(Hit:0 / Total:1)")|
|[contracts/tokens/ERC1155Receiver.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/tokens/ERC1155Receiver.sol)|[15](#nowhere "(nSLOC:9, SLOC:15, Lines:21)")|[0.00%](#nowhere "(Hit:0 / Total:1)")|
|[contracts/tokens/ERC721Receiver.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/tokens/ERC721Receiver.sol)|[24](#nowhere "(nSLOC:13, SLOC:24, Lines:34)")|[50.00%](#nowhere "(Hit:1 / Total:2)")|
|[contracts/utils/Proxy.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/Proxy.sol) [🖥](#nowhere "Uses Assembly") [💰](#nowhere "Payable Functions") [👥](#nowhere "DelegateCall")|[26](#nowhere "(nSLOC:26, SLOC:26, Lines:37)")|[100.00%](#nowhere "(Hit:2 / Total:2)")|
|[contracts/utils/ReadOnlyDelegateCall.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/ReadOnlyDelegateCall.sol) [👥](#nowhere "DelegateCall") [♻️](#nowhere "TryCatch Blocks")|[27](#nowhere "(nSLOC:25, SLOC:27, Lines:40)")|[100.00%](#nowhere "(Hit:4 / Total:4)")|
|[contracts/party/Party.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/party/Party.sol) [💰](#nowhere "Payable Functions")|[32](#nowhere "(nSLOC:29, SLOC:32, Lines:48)")|[100.00%](#nowhere "(Hit:1 / Total:1)")|
|[contracts/party/PartyFactory.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/party/PartyFactory.sol) [🌀](#nowhere "create/create2")|[40](#nowhere "(nSLOC:32, SLOC:40, Lines:54)")|[80.00%](#nowhere "(Hit:4 / Total:5)")|
|[contracts/proposals/ProposalStorage.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/ProposalStorage.sol) [🖥](#nowhere "Uses Assembly") [👥](#nowhere "DelegateCall") [🧮](#nowhere "Uses Hash-Functions")|[46](#nowhere "(nSLOC:36, SLOC:46, Lines:59)")|[80.00%](#nowhere "(Hit:8 / Total:10)")|
|[contracts/proposals/FractionalizeProposal.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/FractionalizeProposal.sol)|[55](#nowhere "(nSLOC:50, SLOC:55, Lines:80)")|[100.00%](#nowhere "(Hit:10 / Total:10)")|
|[contracts/globals/Globals.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/globals/Globals.sol)|[59](#nowhere "(nSLOC:59, SLOC:59, Lines:82)")|[35.71%](#nowhere "(Hit:5 / Total:14)")|
|[contracts/crowdfund/BuyCrowdfund.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/crowdfund/BuyCrowdfund.sol) [💰](#nowhere "Payable Functions")|[69](#nowhere "(nSLOC:57, SLOC:69, Lines:116)")|[100.00%](#nowhere "(Hit:4 / Total:4)")|
|[contracts/crowdfund/CollectionBuyCrowdfund.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/crowdfund/CollectionBuyCrowdfund.sol) [💰](#nowhere "Payable Functions")|[82](#nowhere "(nSLOC:68, SLOC:82, Lines:133)")|[100.00%](#nowhere "(Hit:3 / Total:3)")|
|[contracts/crowdfund/CrowdfundFactory.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/crowdfund/CrowdfundFactory.sol) [💰](#nowhere "Payable Functions")|[94](#nowhere "(nSLOC:66, SLOC:94, Lines:131)")|[93.33%](#nowhere "(Hit:14 / Total:15)")|
|[contracts/crowdfund/CrowdfundNFT.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/crowdfund/CrowdfundNFT.sol)|[115](#nowhere "(nSLOC:82, SLOC:115, Lines:169)")|[44.00%](#nowhere "(Hit:11 / Total:25)")|
|[contracts/party/PartyGovernanceNFT.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/party/PartyGovernanceNFT.sol)|[129](#nowhere "(nSLOC:86, SLOC:129, Lines:181)")|[57.69%](#nowhere "(Hit:15 / Total:26)")|
|[contracts/proposals/ListOnZoraProposal.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/ListOnZoraProposal.sol) [🧮](#nowhere "Uses Hash-Functions") [♻️](#nowhere "TryCatch Blocks")|[151](#nowhere "(nSLOC:127, SLOC:151, Lines:205)")|[100.00%](#nowhere "(Hit:25 / Total:25)")|
|[contracts/crowdfund/AuctionCrowdfund.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/crowdfund/AuctionCrowdfund.sol) [💰](#nowhere "Payable Functions") [👥](#nowhere "DelegateCall")|[181](#nowhere "(nSLOC:168, SLOC:181, Lines:283)")|[87.50%](#nowhere "(Hit:49 / Total:56)")|
|[contracts/proposals/ArbitraryCallsProposal.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/ArbitraryCallsProposal.sol) [🖥](#nowhere "Uses Assembly") [🧮](#nowhere "Uses Hash-Functions")|[186](#nowhere "(nSLOC:151, SLOC:186, Lines:238)")|[96.36%](#nowhere "(Hit:53 / Total:55)")|
|[contracts/proposals/ProposalExecutionEngine.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/ProposalExecutionEngine.sol) [🖥](#nowhere "Uses Assembly") [🧮](#nowhere "Uses Hash-Functions")|[192](#nowhere "(nSLOC:167, SLOC:192, Lines:275)")|[86.44%](#nowhere "(Hit:51 / Total:59)")|
|[contracts/distribution/TokenDistributor.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/distribution/TokenDistributor.sol) [🖥](#nowhere "Uses Assembly") [💰](#nowhere "Payable Functions")|[326](#nowhere "(nSLOC:240, SLOC:326, Lines:414)")|[90.48%](#nowhere "(Hit:57 / Total:63)")|
|_Abstracts (5)_|
|[contracts/utils/Implementation.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/Implementation.sol) [🖥](#nowhere "Uses Assembly")|[21](#nowhere "(nSLOC:21, SLOC:21, Lines:30)")|-|
|[contracts/crowdfund/BuyCrowdfundBase.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/crowdfund/BuyCrowdfundBase.sol)|[120](#nowhere "(nSLOC:102, SLOC:120, Lines:174)")|[79.31%](#nowhere "(Hit:23 / Total:29)")|
|[contracts/proposals/ListOnOpenseaProposal.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/ListOnOpenseaProposal.sol) [🖥](#nowhere "Uses Assembly")|[282](#nowhere "(nSLOC:255, SLOC:282, Lines:374)")|[97.75%](#nowhere "(Hit:87 / Total:89)")|
|[contracts/crowdfund/Crowdfund.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/crowdfund/Crowdfund.sol) [🖥](#nowhere "Uses Assembly") [💰](#nowhere "Payable Functions")|[339](#nowhere "(nSLOC:282, SLOC:339, Lines:494)")|[77.36%](#nowhere "(Hit:82 / Total:106)")|
|[contracts/party/PartyGovernance.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/party/PartyGovernance.sol) [🖥](#nowhere "Uses Assembly") [💰](#nowhere "Payable Functions") [👥](#nowhere "DelegateCall") [🧮](#nowhere "Uses Hash-Functions")|[783](#nowhere "(nSLOC:626, SLOC:783, Lines:1137)")|[71.43%](#nowhere "(Hit:150 / Total:210)")|
|_Libraries (6)_|
|[contracts/utils/LibAddress.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/LibAddress.sol)|[12](#nowhere "(nSLOC:10, SLOC:12, Lines:16)")|[0.00%](#nowhere "(Hit:0 / Total:3)")|
|[contracts/utils/LibRawResult.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/LibRawResult.sol) [🖥](#nowhere "Uses Assembly")|[15](#nowhere "(nSLOC:9, SLOC:15, Lines:20)")|-|
|[contracts/utils/LibSafeERC721.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/LibSafeERC721.sol)|[19](#nowhere "(nSLOC:15, SLOC:19, Lines:31)")|[0.00%](#nowhere "(Hit:0 / Total:4)")|
|[contracts/utils/LibERC20Compat.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/LibERC20Compat.sol) [🖥](#nowhere "Uses Assembly")|[26](#nowhere "(nSLOC:24, SLOC:26, Lines:32)")|[0.00%](#nowhere "(Hit:0 / Total:12)")|
|[contracts/proposals/LibProposal.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/LibProposal.sol)|[34](#nowhere "(nSLOC:21, SLOC:34, Lines:39)")|[0.00%](#nowhere "(Hit:0 / Total:8)")|
|[contracts/utils/LibSafeCast.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/LibSafeCast.sol)|[56](#nowhere "(nSLOC:48, SLOC:56, Lines:65)")|[0.00%](#nowhere "(Hit:0 / Total:19)")|
|_Interfaces (15)_|
|[contracts/distribution/ITokenDistributorParty.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/distribution/ITokenDistributorParty.sol)|[5](#nowhere "(nSLOC:5, SLOC:5, Lines:15)")|-|
|[contracts/proposals/vendor/IOpenseaConduitController.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/vendor/IOpenseaConduitController.sol)|[5](#nowhere "(nSLOC:5, SLOC:5, Lines:7)")|-|
|[contracts/gatekeepers/IGateKeeper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/gatekeepers/IGateKeeper.sol)|[8](#nowhere "(nSLOC:4, SLOC:8, Lines:16)")|-|
|[contracts/tokens/IERC721Receiver.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/tokens/IERC721Receiver.sol)|[9](#nowhere "(nSLOC:4, SLOC:9, Lines:12)")|-|
|[contracts/tokens/IERC20.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/tokens/IERC20.sol)|[10](#nowhere "(nSLOC:10, SLOC:10, Lines:14)")|-|
|[contracts/market-wrapper/IMarketWrapper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/market-wrapper/IMarketWrapper.sol)|[16](#nowhere "(nSLOC:9, SLOC:16, Lines:89)")|-|
|[contracts/party/IPartyFactory.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/party/IPartyFactory.sol)|[16](#nowhere "(nSLOC:9, SLOC:16, Lines:37)")|-|
|[contracts/globals/IGlobals.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/globals/IGlobals.sol)|[17](#nowhere "(nSLOC:17, SLOC:17, Lines:23)")|-|
|[contracts/proposals/IProposalExecutionEngine.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/IProposalExecutionEngine.sol)|[17](#nowhere "(nSLOC:16, SLOC:17, Lines:38)")|-|
|[contracts/tokens/IERC721.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/tokens/IERC721.sol)|[17](#nowhere "(nSLOC:17, SLOC:17, Lines:21)")|-|
|[contracts/proposals/vendor/FractionalV1.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/vendor/FractionalV1.sol)|[23](#nowhere "(nSLOC:13, SLOC:23, Lines:32)")|-|
|[contracts/vendor/markets/IZoraAuctionHouse.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/vendor/markets/IZoraAuctionHouse.sol) [💰](#nowhere "Payable Functions")|[34](#nowhere "(nSLOC:26, SLOC:34, Lines:53)")|-|
|[contracts/tokens/IERC1155.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/tokens/IERC1155.sol)|[39](#nowhere "(nSLOC:24, SLOC:39, Lines:43)")|-|
|[contracts/distribution/ITokenDistributor.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/distribution/ITokenDistributor.sol) [💰](#nowhere "Payable Functions")|[89](#nowhere "(nSLOC:47, SLOC:89, Lines:169)")|-|
|[contracts/proposals/vendor/IOpenseaExchange.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/vendor/IOpenseaExchange.sol) [💰](#nowhere "Payable Functions")|[123](#nowhere "(nSLOC:120, SLOC:123, Lines:137)")|-|
|Total (over 46 files):| [3995](#nowhere "(nSLOC:3236, SLOC:3995, Lines:5735)")| [76.54%](#nowhere "Hit:659 / Total:861")|

### All other source contracts (not in scope)
|File|[SLOC](#nowhere "(nSLOC, SLOC, Lines)")|[Coverage](#nowhere "(Lines hit / Total)")|
|:-|:-:|:-:|
|_Contracts (9)_|
|[contracts/gatekeepers/AllowListGateKeeper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/gatekeepers/AllowListGateKeeper.sol) [🖥](#nowhere "Uses Assembly")|[25](#nowhere "(nSLOC:21, SLOC:25, Lines:37)")|[100.00%](#nowhere "(Hit:7 / Total:7)")|
|[contracts/gatekeepers/TokenGateKeeper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/gatekeepers/TokenGateKeeper.sol)|[32](#nowhere "(nSLOC:25, SLOC:32, Lines:54)")|[100.00%](#nowhere "(Hit:7 / Total:7)")|
|[contracts/market-wrapper/FoundationMarketWrapper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/market-wrapper/FoundationMarketWrapper.sol)|[56](#nowhere "(nSLOC:37, SLOC:56, Lines:121)")|[0.00%](#nowhere "(Hit:0 / Total:10)")|
|[contracts/market-wrapper/ZoraMarketWrapper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/market-wrapper/ZoraMarketWrapper.sol)|[74](#nowhere "(nSLOC:54, SLOC:74, Lines:140)")|[0.00%](#nowhere "(Hit:0 / Total:14)")|
|[contracts/market-wrapper/NounsMarketWrapper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/market-wrapper/NounsMarketWrapper.sol)|[76](#nowhere "(nSLOC:55, SLOC:76, Lines:138)")|[0.00%](#nowhere "(Hit:0 / Total:21)")|
|[contracts/market-wrapper/KoansMarketWrapper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/market-wrapper/KoansMarketWrapper.sol)|[77](#nowhere "(nSLOC:56, SLOC:77, Lines:140)")|[0.00%](#nowhere "(Hit:0 / Total:21)")|
|[contracts/utils/PartyHelpers.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/PartyHelpers.sol)|[97](#nowhere "(nSLOC:76, SLOC:97, Lines:126)")|[96.55%](#nowhere "(Hit:28 / Total:29)")|
|[contracts/renderers/CrowdfundNFTRenderer.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/renderers/CrowdfundNFTRenderer.sol)|[137](#nowhere "(nSLOC:137, SLOC:137, Lines:177)")|[65.38%](#nowhere "(Hit:34 / Total:52)")|
|[contracts/renderers/PartyGovernanceNFTRenderer.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/renderers/PartyGovernanceNFTRenderer.sol)|[143](#nowhere "(nSLOC:139, SLOC:143, Lines:186)")|[100.00%](#nowhere "(Hit:34 / Total:34)")|
|_Abstracts (4)_|
|[contracts/proposals/ZoraHelpers.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/proposals/ZoraHelpers.sol)|[27](#nowhere "(nSLOC:10, SLOC:27, Lines:42)")|-|
|[contracts/vendor/solmate/ERC20.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/vendor/solmate/ERC20.sol) [🧮](#nowhere "Uses Hash-Functions") [🔖](#nowhere "Handles Signatures: ecrecover") [Σ](#nowhere "Unchecked Blocks")|[119](#nowhere "(nSLOC:107, SLOC:119, Lines:205)")|[26.92%](#nowhere "(Hit:7 / Total:26)")|
|[contracts/vendor/solmate/ERC721.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/vendor/solmate/ERC721.sol) [Σ](#nowhere "Unchecked Blocks")|[135](#nowhere "(nSLOC:113, SLOC:135, Lines:230)")|[15.79%](#nowhere "(Hit:6 / Total:38)")|
|[contracts/vendor/solmate/ERC1155.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/vendor/solmate/ERC1155.sol) [Σ](#nowhere "Unchecked Blocks")|[162](#nowhere "(nSLOC:115, SLOC:162, Lines:244)")|[18.18%](#nowhere "(Hit:8 / Total:44)")|
|_Libraries (3)_|
|[contracts/globals/LibGlobals.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/globals/LibGlobals.sol)|[25](#nowhere "(nSLOC:25, SLOC:25, Lines:28)")|-|
|[contracts/utils/vendor/Base64.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/vendor/Base64.sol) [🖥](#nowhere "Uses Assembly")|[41](#nowhere "(nSLOC:41, SLOC:41, Lines:63)")|[100.00%](#nowhere "(Hit:6 / Total:6)")|
|[contracts/utils/vendor/Strings.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/utils/vendor/Strings.sol)|[49](#nowhere "(nSLOC:49, SLOC:49, Lines:71)")|[0.00%](#nowhere "(Hit:0 / Total:30)")|
|_Interfaces (4)_|
|[contracts/renderers/IERC721Renderer.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/renderers/IERC721Renderer.sol)|[5](#nowhere "(nSLOC:5, SLOC:5, Lines:7)")|-|
|[contracts/vendor/markets/IFoundationMarket.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/vendor/markets/IFoundationMarket.sol) [💰](#nowhere "Payable Functions")|[29](#nowhere "(nSLOC:19, SLOC:29, Lines:37)")|-|
|[contracts/vendor/markets/INounsAuctionHouse.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/vendor/markets/INounsAuctionHouse.sol) [💰](#nowhere "Payable Functions")|[32](#nowhere "(nSLOC:32, SLOC:32, Lines:77)")|-|
|[contracts/vendor/markets/IKoansAuctionHouse.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/vendor/markets/IKoansAuctionHouse.sol) [💰](#nowhere "Payable Functions")|[37](#nowhere "(nSLOC:37, SLOC:37, Lines:71)")|-|
|Total (over 20 files):| [1378](#nowhere "(nSLOC:1153, SLOC:1378, Lines:2194)")| [40.41%](#nowhere "Hit:137 / Total:339")|

## External imports
* **openzeppelin/contracts/interfaces/IERC2981.sol**
  * [contracts/party/PartyGovernanceNFT.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/party/PartyGovernanceNFT.sol)
* **openzeppelin/contracts/utils/cryptography/MerkleProof.sol**
  * ~~[contracts/gatekeepers/AllowListGateKeeper.sol](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/gatekeepers/AllowListGateKeeper.sol)~~

## Contracts For Further Context
Additional out-of-scope contracts that are either consumed by or referenced by the in-scope business logic:

- [Gatekeepers](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/gatekeepers): Contracts that crowdfunds can optionally use to enforce who can participate in a crowdfund.
- [MarketWrappers](https://github.com/PartyDAO/party-contracts-c4/blob/main/contracts/market-wraper): Wrappers to various NFT auction markets to provide a unified interface for the `AuctionCrowdfund`. Inherited from V1 of the protocol.
- [PartyBidV1](https://github.com/PartyDAO/partybid): Prior iteration of the protocol. Only featured the crowdfunds phase. Historical and motivational context.

## Lifecycle and Diagrams

At a high level, the typical business flow of the key contracts in this protocol goes like:

1. Someone starts a crowdfund (`AuctionCrowdfund`, `BuyCrowdfund`, or `CollectionBuyCrowdfund`) to acquire an NFT (could be a specific one or any from a collection) and form a party around it.
    1. At creation time they also choose the (fixed) parameters for the governance phase, should they succeed.
    2. At creation time they also choose initial "party hosts" for the crowdfund, which have special powers that carry over to the governance phase.
2. While the crowdfund is active (not expired or finalized), people can contribute ETH to the crowdfund.
    1. This mints each contributor a soulbound "participation NFT" as well.
    2. Contributors may also preemptively choose whom to delegate their voting power to if the party goes on to the governance phase.
3. At any time while the crowdfund is active, someone can take an action on the crowdfund (depends on the crowdfund type) to attempt to purchase an NFT.
    1. This could be placing a bid on an auction market or executing arbitrary call data to outright buy a fixed price listing (e.g., on opensea).
4. If the crowdfund fails to acquire an NFT before it expires, Anyone can burn a contributor's participation NFT to return their contributed ETH. That is the end of the lifecycle for that party. Stop here.
5. If the crowdfund can successfully acquire the NFT before it expires, it transitions into governance phase.
6. A "governance party" (`Party`) is deployed.
    1. The fixed governance parameters chosen when the crowdfund was created are used to initialize the party.
    2. The bought NFT is transferred into this party.
7. Anyone can burn a contributor's participation NFT to:
    1. Refund any of the contributor's ETH that was not used to purchase the NFT.
    2. Mint voting power for the contributor in the governance party equal to the amount of their ETH that was used.
        1. This voting power is tokenized as a transferrable NFT ("governance NFT").
        2. If an initial delegate was chosen (other then themselves), the voting power will also be delegated at this time.
8. The governance party now has the purchased NFT (called "precious") and users with effective voting power can make, vote, and execute proposals through governance.
    1. Party hosts (inherited from the crowdfund phase) can unilaterally veto any proposal made.
    2. Snapshots of voting power are taken whenever a user's voting power or delegation is updated to make sure only voting power at the time a proposal is made is used in voting.
9. When a proposal passes and is executed, the governance party will delegatecall into the `ProposalExecutionEngine` logic contract which decodes and executes the proposal.
    1. Some proposal types are non-atomic, multi-step, requiring repeated executions. No other proposal may be executed while another proposal is incomplete.
10. If any ETH or ERC20s accrue in the party, anyone with effective voting power can trigger a "distribution".
    1. This moves all of the chosen asset (ETH or ERC20) into the canonical `TokenDistributor` contract and creates a distribution within it.
    2. Anyone with a governance NFT in that party can redeem their share of the asset distribution.
        1. Distribution share for a governance NFT is generally equal to its individual voting power over the total voting power of the party.

![image]( https://github.com/code-423n4/2022-09-party/raw/main/contract-lifecycle.png)


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

**For deeper details, visit the [Protocol Documentation](https://github.com/PartyDAO/party-contracts-c4/tree/main/docs).**

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
