keyes | 2024-09-07 22:09:58 UTC | #1

## 👩‍🚀 Summary

August was a very productive month for the Pinax team! 

As we [prepare to sunset our dfuse hosted service for EOS and WAX](https://eosnation.io/old-dfuse-tech-discontinued-new-antelope-services-available/), we’ve been working with dfuse users to prepare them to migrate to new EOS and WAX Subgraphs on The Graph and our new Token API, bringing support for WAX and EOS subgraphs on The Graph for the first time. We also shared our first [prototype of Datasets for Ethereum](https://docs.google.com/document/d/1uCKsON1Rz4c8y-SGydKRsFf1slh_Q_KuvU2LNX2t4GY/edit#heading=h.xx7kjzdxf096) with a handful of prospective customers, added support for 13 new chains and improvements and upgrades to a whole bunch more. And those are just some of the highlights - read on for more!

## :tada: Looking back (what was delivered)

### Provide infrastructure for chains currently supported on The Graph & to support protocol integration with new chains

**EOS and WAX Substreams-Powered-Subgraphs on The Graph**
- As we [prepare to sunset our dfuse hosted service for EOS and WAX](https://eosnation.io/old-dfuse-tech-discontinued-new-antelope-services-available/), we’ve been working with dfuse users to prepare them to migrate to new EOS and WAX Subgraphs on The Graph and our new Token API, bringing support for WAX and EOS subgraphs on The Graph for the first time.
- We’ve deployed a [WAX Transactions Substreams–Powered-Subgraph](https://thegraph.com/explorer/subgraphs/4bAe7NA8b6J14ZfZr3TXfzzjjSoGECTFuqv7CwnK1zzg?view=Query&chain=arbitrum-one) to The Graph.
- We’ve deployed an [EOS Transactions Substreams–Powered-Subgraph](https://thegraph.com/explorer/subgraphs/2RNdhL5p62dGN5UqKtsSEhYZiTJbFcuuhzk9qRJj8QeU?view=Query&chain=arbitrum-one) to The Graph.
- We’ve contributed [Antelope Foundational Substreams Modules](https://github.com/pinax-network/substreams-foundational-modules/tree/develop/antelope-common) to StreamingFast’s Substreams Foundational Modules

**RPCs**
- We’ve developed a Caddy prototype for handing RPC authentication.

**POl investigations**
- Graphix is now set up in Pinax Kubernetes infrastructure.

**New blockchains added since July 26, 2024:**
- Arbnova (RPC + Firehose + Substreams)
- Base Sepolia (Firehose + Substreams)
- Blast Sepolia (Firehose + Substreams)
- Cardona (Firehose + Substreams)
- Fantom (Firehose + Substreams)
- Moonriver (RPC + Firehose + Substreams)
- Optimism Sepolia (Firehose + Substreams)
- Pangea (RPC + Firehose + Substreams)
- Pangeatest (RPC + Firehose + Substreams)
- Polygon zkevm (Firehose + Substreams)
- Ronin (Firehose + Substreams)
- Rootstock (RPC)
- Solana (Firehose + Substreams)

**Chains transformed from light to full blocks during this period:**
- Optimism
- Base
- Zora

**Auxiliary Service Information for this period:**
- Bugs Fixes:
  - BSC mainnet reprocessing (block difficulty incorrect issue)
- Testing:
  - op-erigon (base/ optimism)
  - rootstock config testing
- New chains (not released yet)
  - Iotex
  - iotex testnet
  - etherlink
- Upgrades:
  - erigon upgrade to v2.60.6 (polygon/ethereum/holesky/amoy/gnosis/chiado/sepolia)
  - op-erigon upgrade v1.2.3 (boba/ boba sepolia)
  - op-erigon upgrade to v2.60.5-0.7.1 (optimism/base)
  - cosmos / near version upgrade
  - op-geth upgrade to v0.5.0 (opbnb)
  - op-node upgrade to v0.5.0 (opbnb)
  - zkevm-node upgrade to v0.7.3 (polygon zkevm / cardona)
  - op-geth upgrade to v1.101408.0 (mode/zora/ base/ base sepolia/ optimism/ optimism sepolia)
  - op-node upgrade to v1.9.1 (mode/zora/ base/ base sepolia/ optimism/ optimism sepolia)
  - pathfinder upgrade to v0.14.2 (starknet)
  - avalanchego upgrade to v1.11.11 (avalanche)
  - kava upgrade to v0.26.2 (kava)
  - nitro upgrade to v3.1.2 (arbitrum/ arbitrum sepolia/ xai/ geo /geo testnet / arbnova)
  - geth upgrade to v5.7.0 (scroll)
  - solana upgrade to anza-xyz/agave 1.18.22 (solana)

### Education, onboarding & community support for Indexers and Developers working with new data services

- We’ve delivered our first set of results of our Solana ecosystem scan and outreach campaign to The Graph core devs.
- We published 5 new YouTube videos:
  - [Create Subgraphs Like a Pro: Hack’N Heights Workshop Part 4 with Arturo Castañon](https://www.youtube.com/watch?v=1mzqC2_N9Tc)
  - [Graph Espresso Special Episode: Recap of Pinax’s Action-Packed Week at ETHGlobal Brussels & ETHCC!](https://www.youtube.com/watch?v=KOkblCI00us)
  - [The Graph Espresso 8: Celebrating Global Communities & Their Impact on The Graph Ecosystem](https://www.youtube.com/watch?v=t4wsLZRTW-8)
  - [Hack'n Heights Hackathon - GM Builders Demo - Pinax Bounty Winner 1/2 [Best use of Substreams]](https://www.youtube.com/watch?v=Ca1_QldEnfo)
  - [TickTicket: A Decentralized Ticketing System with Substreams Integration](https://www.youtube.com/watch?v=tv3AYJcbd4Q)
- Pinax is continuing to publish summaries of the Indexer Office hours on our blog every week:
  - [The Graph Indexer Office Hours #167](https://blog.pinax.network/events/the-graph-indexer-office-hours-167/)
  - [The Graph Indexer Office Hours #168](https://blog.pinax.network/events/the-graph-indexer-office-hours-168/)
  - [The Graph Indexer Office Hours #169](https://blog.pinax.network/events/the-graph-indexer-office-hours-169/)
  - [The Graph Indexer Office Hours #170](https://blog.pinax.network/events/the-graph-indexer-office-hours-170/)
  - [The Graph Indexer Office Hours #171](https://blog.pinax.network/events/the-graph-indexer-office-hours-171/)
  - [The Graph Indexer Office Hours #172](https://blog.pinax.network/events/the-graph-indexer-office-hours-172/)
  - [The Graph Indexer Office Hours #173](https://blog.pinax.network/events/the-graph-indexer-office-hours-173/)
 - We published 4 additional new blog posts with educational and promotional content on The Graph and Firehose & Substreams (available in English, French, and Vietnamese):
  - [Subgraph Studio, the Easy Choice for Building Your Subgraphs](https://blog.pinax.network/the-graph/subgraph-studio-the-easy-choice-for-building-your-subgraphs/)
  - [AI and Blockchain’s Shared Destiny: A People’s Internet](https://blog.pinax.network/insights/ai-and-blockchains-shared-destiny-a-peoples-internet/)
  - [Stream Seamless Antelope Data with Epic New Foundational Substreams Modules](https://blog.pinax.network/substreams/stream-seamless-antelope-data-with-epic-new-foundational-substreams-modules/)
  - [Web3 Made Simple: What Is The Graph?](https://blog.pinax.network/insights/web3-made-simple-what-is-the-graph/)
- Pinax China community managers, Lena and Eleven, manned The Graph booth at [ETH Shenzhen](https://www.ethshenzhen.org/) (Aug 16 - 18)
  - Lena delivered a presentation on stage giving an introduction to The Graph
  - They also met with representatives of Chinese Universities there to further discuss “Graph On Campus” initiatives
  - Lena is in charge of organizing “Graph On Campus” Events in Beijing
- Pinax team members promoted Firehose, Substreams, and The Graph at Futurist Conference in Toronto
- Pinax is continuing to supporting the Vietnamese Community Manager for The Graph
- Our Chinese Chinese community manager, Eleven, is continuing to manage The Graph Chinese communities in Telegram, Discord, and WeChat.
- We continue to support the production of The Graph Builders Office Hours each week.
- We continue to heavily promote The Graph ecosystem on [the Pinax X account](https://twitter.com/PinaxNetwork).

### Collaboration with core developers and new consumers on designing and testing new data services while augmenting the Indexer experience with new tooling

**Datasets (parquet files)**
- We’ve shared our first [prototype of Datasets for Ethereum](https://docs.google.com/document/d/1uCKsON1Rz4c8y-SGydKRsFf1slh_Q_KuvU2LNX2t4GY/edit#heading=h.xx7kjzdxf096) with a handful of prospective customers and are in the process of gathering feedback.
- We’ve [produced documentation on plans for verified datasets](https://github.com/pinax-network/substreams-raw-blocks/blob/main/docs/verifying_ethereum_firehose_blocks.md) based on conversations with Semiotic.
- We participated in good discussions with Edge & Node, Semiotic, and The Graph Foundation on using nozzle for datasets.
- We’ve developed [EVM and Antelope schemas for Raw Blocks using Substreams](https://github.com/pinax-network/substreams-raw-blocks).

**Token API**
- Began preparing our dfuse users to migrate to the first version of our Antelope Transaction API and Token API.
- Split use cases by level of detail: recent, more detailed in graph-node ([Antelope Transactions Subgraph](https://github.com/pinax-network/subgraph-antelope-transactions)); Long term, less detailed in ClickHouse ([Antelope Transactions API](https://github.com/pinax-network/antelope-transactions-api) and [Antelope Token API](https://github.com/pinax-network/antelope-token-api))


## :rocket: Looking ahead (upcoming priorities)

### Provide infrastructure for chains currently supported on The Graph & to support protocol integration with new chains

**EOS and WAX Substreams-Powered-Subgraphs on The Graph**
- Migrating dfuse users to new EOS and WAX transactions subgraphs.
- Chain foundation and dApp co-marketing initiatives announcing support for EOS and WAX on The Graph.
- Antelope Substreams "codegen" (like Injective).
- DefiBox Subgraph (DefiBox is the most active DeFi product on EOS).
- More dApp-specific subgraphs.

**Indexer performance**
- Setting up "pinax2" indexer sharded on dedicated hardware
- Optimizing our indexer to use multiple shards

**Firehose**
- Testing remote firehose reader.
- Re-generate firehose blocks for "fuse" (last remaining RPC poller chain that needs doing).
- Verifiable Firehose test.
- Erigon Firehose test.
- Firehose-near update to v2.

**RPCs**
- Improving proxy-auth by building prototype service with caddy.

**POl investigations**
- Authentication for Graphix.

### Education, onboarding & community support for Indexers and Developers working with new data services

- Pinax team member, Guillaume Cléroux, will do sharing at IOH on Kubernetes.
- Pinax team members attending Token2049 and Solana breakpoint in Singapore.
- Continuing our Solana ecosystem scan and outreach campaign.
- More documentation on Firehose & Substreams.
- More videos and blog content.

### Collaboration with core developers and new consumers on designing and testing new data services while augmenting the Indexer experience with new tooling

**Datasets (parquet files)**
- Exploring toolchain.
- Documenting plans/ideas for sharing to get feedback.
- We’re in the process of developing [Solana Raw Blocks schema using Substreams](https://github.com/pinax-network/substreams-raw-blocks).
- Expanding datasets prototype with support for more chains.

**Token API**
- Working on documenting plans.
- Migrating dfuse users to our Antelope Token API and Transaction Subgraphs.

**Billing (thegraph.market)**
- Developing a Kafka Sink Connector that consumes Substreams, Firehose and RPC requests.usage events from Kafka topics and sends them to the StreamingFast payment gateway.

-------------------------

