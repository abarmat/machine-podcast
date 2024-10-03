---
title: Publishing a Subgraph to the Decentralized Network
---

Once you have [deployed your subgraph to Subgraph Studio](/deploying/deploying-a-subgraph-to-studio) and it's ready to go into production, you can publish it to the decentralized network.

When you publish a subgraph to the decentralized network, you make it available for:

- [Curators](/network/curating) to begin curating it.
- [Indexers](/network/indexing) to begin indexing it.

<VideoEmbed youtube="satdwdbvzAQ" />

Check out the list of [supported networks](/developing/supported-networks).

## Publishing from Subgraph Studio

1. Go to the [Subgraph Studio](https://thegraph.com/studio/) dashboard
2. Click on the **Publish** button
3. Your subgraph will now be visible in [Graph Explorer](https://thegraph.com/explorer/).

All published versions of an existing subgraph can:

- Be published to Arbitrum One. [Learn more about The Graph Network on Arbitrum](/arbitrum/arbitrum-faq).

- Index data on any of the [supported networks](/developing/supported-networks), regardless of the network on which the subgraph was published.

### Updating metadata for a published subgraph

- After publishing your subgraph to the decentralized network, you can update the metadata anytime in Subgraph Studio.
- Once you’ve saved your changes and published the updates, they will appear in Graph Explorer.
- It's important to note that this process will not create a new version since your deployment has not changed.

## Publishing from the CLI

As of version 0.73.0, you can also publish your subgraph with the [`graph-cli`](https://github.com/graphprotocol/graph-tooling/tree/main/packages/cli).

1. Open the `graph-cli`.
2. Use the following commands: `graph codegen && graph build` then `graph publish`.
3. A window will open, allowing you to connect your wallet, add metadata, and deploy your finalized subgraph to a network of your choice.

![cli-ui](/img/cli-ui.png)

### Customizing your deployment

You can upload your subgraph build to a specific IPFS node and further customize your deployment with the following flags:

```
USAGE
  $ graph publish [SUBGRAPH-MANIFEST] [-h] [--protocol-network arbitrum-one|arbitrum-sepolia --subgraph-id <value>] [-i <value>] [--ipfs-hash <value>] [--webapp-url
    <value>]

FLAGS
  -h, --help                   Show CLI help.
  -i, --ipfs=<value>           [default: https://api.thegraph.com/ipfs/api/v0] Upload build results to an IPFS node.
  --ipfs-hash=<value>          IPFS hash of the subgraph manifest to deploy.
  --protocol-network=<option>  [default: arbitrum-one] The network to use for the subgraph deployment.
                               <options: arbitrum-one|arbitrum-sepolia>
  --subgraph-id=<value>        Subgraph ID to publish to.
  --webapp-url=<value>         [default: https://cli.thegraph.com/publish] URL of the web UI you want to use to deploy.

```

## Adding signal to your subgraph

Developers can add GRT signal to their subgraphs to incentivize Indexers to query the subgraph.

- If a subgraph is eligible for indexing rewards, Indexers who provide a "proof of indexing" will receive a GRT reward, based on the amount of GRT signalled.

- You can check indexing reward eligibility based on subgraph feature usage [here](https://github.com/graphprotocol/indexer/blob/main/docs/feature-support-matrix.md).

- Specific supported networks can be checked [here](/developing/supported-networks).

> Adding signal to a subgraph which is not eligible for rewards will not attract additional Indexers.

> If your subgraph is eligible for rewards, it is recommended that you curate your own subgraph with at least 3,000 GRT in order to attract additional indexers to index your subgraph.

The [Sunrise Upgrade Indexer](/sunrise/#what-is-the-upgrade-indexer) ensures the indexing of all subgraphs. However, signaling GRT on a particular subgraph will draw more indexers to it. This incentivization of additional Indexers through curation aims to enhance the quality of service for queries by reducing latency and enhancing network availability.

When signaling, Curators can decide to signal on a specific version of the subgraph or to signal using auto-migrate. If they signal using auto-migrate, a curator’s shares will always be updated to the latest version published by the developer. If they decide to signal on a specific version instead, shares will always stay on this specific version.

Indexers can find subgraphs to index based on curation signals they see in Graph Explorer.

![Explorer subgraphs](/img/explorer-subgraphs.png)

Subgraph Studio enables you to add signal to your subgraph by adding GRT to your subgraph's curation pool in the same transaction it is published.

![Curation Pool](/img/curate-own-subgraph-tx.png)

Alternatively, you can add GRT signal to a published subgraph from Graph Explorer.

![Signal from Explorer](/img/signal-from-explorer.png)

Learn more about [Curating](/network/curating/) on The Graph Network.
---
title: Post-Sunrise + Upgrading to The Graph Network FAQ
---

> Note: The Sunrise of Decentralized Data ended June 12th, 2024.

## What was the Sunrise of Decentralized Data?

The Sunrise of Decentralized Data was an initiative spearheaded by Edge & Node. This initiative enabled subgraph developers to upgrade to The Graph’s decentralized network seamlessly.

This plan drew on previous developments from The Graph ecosystem, including an upgrade Indexer to serve queries on newly published subgraphs.

### What happened to the hosted service?

The hosted service query endpoints are no longer available, and developers cannot deploy new subgraphs on the hosted service.

During the upgrade process, owners of hosted service subgraphs could upgrade their subgraphs to The Graph Network. Additionally, developers were able to claim auto-upgraded subgraphs.

### Was Subgraph Studio impacted by this upgrade?

No, Subgraph Studio was not impacted by Sunrise. Subgraphs were immediately available for querying, powered by the upgrade Indexer, which uses the same infrastructure as the hosted service.

### Why were subgraphs published to Arbitrum, did it start indexing a different network?

The Graph Network was initially deployed on Ethereum mainnet but was later moved to Arbitrum One in order to lower gas costs for all users. As a result, all new subgraphs are published to The Graph Network on Arbitrum so that Indexers can support them. Arbitrum is the network that subgraphs are published to, but subgraphs can index any of the [supported networks](/developing/supported-networks/)

## About the Upgrade Indexer

> The upgrade Indexer is currently active.

The upgrade Indexer was implemented to improve the experience of upgrading subgraphs from the hosted service to The Graph Network and support new versions of existing subgraphs that had not yet been indexed.

### What does the upgrade Indexer do?

- It bootstraps chains that have yet to receive indexing rewards on The Graph Network and ensures that an Indexer is available to serve queries as quickly as possible after a subgraph is published.
- It supports chains that were previously only available on the hosted service. Find a comprehensive list of supported chains [here](/developing/supported-networks/).
- Indexers that operate an upgrade Indexer do so as a public service to support new subgraphs and additional chains that lack indexing rewards before The Graph Council approves them.

### Why is Edge & Node running the upgrade Indexer?

Edge & Node historically maintained the hosted service and, as a result, already have synced data for hosted service subgraphs.

### What does the upgrade indexer mean for existing Indexers?

Chains previously only supported on the hosted service were made available to developers on The Graph Network without indexing rewards at first.

However, this action unlocked query fees for any interested Indexer and increased the number of subgraphs published on The Graph Network. As a result, Indexers have more opportunities to index and serve these subgraphs in exchange for query fees, even before indexing rewards are enabled for a chain.

The upgrade Indexer also provides the Indexer community with information about the potential demand for subgraphs and new chains on The Graph Network.

### What does this mean for Delegators?

The upgrade Indexer offers a powerful opportunity for Delegators. As it allowed more subgraphs to be upgraded from the hosted service to The Graph Network, Delegators benefit from the increased network activity.

### Did the upgrade Indexer compete with existing Indexers for rewards?

No, the upgrade Indexer only allocates the minimum amount per subgraph and does not collect indexing rewards.

It operates on an “as needed” basis, serving as a fallback until sufficient service quality is achieved by at least three other Indexers in the network for respective chains and subgraphs.

### How does this affect subgraph developers?

Subgraph developers can query their subgraphs on The Graph Network almost immediately after upgrading from the hosted service or [publishing from Subgraph Studio](/publishing/publishing-a-subgraph/), as no lead time was required for indexing. Please note that [creating a subgraph](/developing/creating-a-subgraph) was not impacted by this upgrade.

### How does the upgrade Indexer benefit data consumers?

The upgrade Indexer enables chains on the network that were previously only supported on the hosted service. Therefore, it widens the scope and availability of data that can be queried on the network.

### How does the upgrade Indexer price queries?

The upgrade Indexer prices queries at the market rate to avoid influencing the query fee market.

### When will the upgrade Indexer stop supporting a subgraph?

The upgrade Indexer supports a subgraph until at least 3 other Indexers successfully and consistently serve queries made to it.

Furthermore, the upgrade Indexer stops supporting a subgraph if it has not been queried in the last 30 days.

Other Indexers are incentivized to support subgraphs with ongoing query volume. The query volume to the upgrade Indexer should trend towards zero, as it has a small allocation size, and other Indexers should be chosen for queries ahead of it.
---
title: TAP Migration Guide
---

Learn about The Graph’s new payment system, **Timeline Aggregation Protocol, TAP**. This system provides fast, efficient microtransactions with minimized trust.

## Overview

[TAP](https://docs.rs/tap_core/latest/tap_core/index.html) is a drop-in replacement to the Scalar payment system currently in place. It provides the following key features:

- Efficiently handles micropayments.
- Adds a layer of consolidations to on-chain transactions and costs.
- Allows Indexers control of receipts and payments, guaranteeing payment for queries.
- It enables decentralized, trustless gateways and improves `indexer-service` performance for multiple senders.

## Specifics

TAP allows a sender to make multiple payments to a receiver, **TAP Receipts**, which aggregates these payments into a single payment, a **Receipt Aggregate Voucher**, also known as a **RAV**. This aggregated payment can then be verified on the blockchain, reducing the number of transactions and simplifying the payment process.

For each query, the gateway will send you a `signed receipt` that is stored on your database. Then, these queries will be aggregated by a `tap-agent` through a request. Afterwards, you’ll receive a RAV. You can update a RAV by sending it with newer receipts and this will generate a new RAV with an increased value.

### RAV Details

- It’s money that is waiting to be sent to the blockchain.

- It will continue to send requests to aggregate and ensure that the total value of non-aggregated receipts does not exceed the `amount willing to lose`.

- Each RAV can be redeemed once in the contracts, which is why they are sent after the allocation is closed.

### Redeeming RAV

As long as you run `tap-agent` and `indexer-agent`, everything will be executed automatically. The following provides a detailed breakdown of the process:

1. An Indexer closes allocation.

2. `<recently-closed-allocation-buffer> period, tap-agent` takes all pending receipts for that specific allocation and requests an aggregation into a RAV, marking it as `last`.

3. `indexer-agent` takes all the last RAVS and sends redeem requests to the blockchain, which will update the value of `redeem_at`.

4. During the `<finality-time>` period, `indexer-agent` monitors if the blockchain has any reorganizations that revert the transaction.

   - If it was reverted, the RAV is resent to the blockchain. If it was not reverted, it gets marked as `final`.

## Blockchain Addresses

### Contracts

| Contract            | Arbitrum Sepolia (421614)                    | Arbitrum Mainnet (42161)                     |
| ------------------- | -------------------------------------------- | -------------------------------------------- |
| TAP Verifier        | `0xfC24cE7a4428A6B89B52645243662A02BA734ECF` | `0x33f9E93266ce0E108fc85DdE2f71dab555A0F05a` |
| AllocationIDTracker | `0xAaC28a10d707bbc6e02029f1bfDAEB5084b2aD11` | `0x5B2F33d7Ca6Ec88f5586f2528f58c20843D9FE7c` |
| Escrow              | `0x1e4dC4f9F95E102635D8F7ED71c5CdbFa20e2d02` | `0x8f477709eF277d4A880801D01A140a9CF88bA0d3` |

### Gateway

| Component  | Edge and Node Mainnet (Arbitrum Sepolia)      | Edge and Node Testnet (Aribtrum Mainnet)      |
| ---------- | --------------------------------------------- | --------------------------------------------- |
| Sender     | `0xDDE4cfFd3D9052A9cb618fC05a1Cd02be1f2F467`  | `0xC3dDf37906724732FfD748057FEBe23379b0710D`  |
| Signers    | `0xfF4B7A5EfD00Ff2EC3518D4F250A27e4c29A2211`  | `0xFb142dE83E261e43a81e9ACEADd1c66A0DB121FE`  |
| Aggregator | `https://tap-aggregator.network.thegraph.com` | `https://tap-aggregator.testnet.thegraph.com` |

### Requirements

In addition to the typical requirements to run an indexer, you’ll need a `tap-escrow-subgraph` endpoint to query TAP updates. You can use The Graph Network to query or host yourself on your `graph-node`.

- [Graph TAP Aribtrum Sepolia subgraph (for The Graph testnet)](https://thegraph.com/explorer/subgraphs/7ubx365MiqBH5iUz6XWXWT8PTof5BVAyEzdb8m17RvbD)
- [Graph TAP Arbitrum One subgraph (for The Graph mainnet)](https://thegraph.com/explorer/subgraphs/4sukbNVTzGELnhdnpyPqsf1QqtzNHEYKKmJkgaT8z6M1)

> Note: `indexer-agent` does not currently handle the indexing of this subgraph like it does for the network subgraph deployement. As a result, you have to index it manually.

## Migration Guide

### Software versions

| Component | Version | Image Link |
| --- | --- | --- |
| indexer-service | v1.0.0-rc.6 | [indexer-service](https://github.com/graphprotocol/indexer-rs/pkgs/container/indexer-service-rs/264320627?tag=1.0.0-rc.6) |
| indexer-agent | PR #995 | [indexer-agent](https://github.com/graphprotocol/indexer/pkgs/container/indexer-agent/266166026?tag=sha-d98cf80) |
| tap-agent | v1.0.0-rc.6 | [tap-agent](https://github.com/graphprotocol/indexer-rs/pkgs/container/indexer-tap-agent/264320547?tag=1.0.0-rc.6) |

### Steps

1. **Indexer Agent**

   - Follow the [same process](https://github.com/graphprotocol/indexer/pkgs/container/indexer-agent#graph-protocol-indexer-components).
   - Give the new argument `--tap-subgraph-endpoint` to activate the new TAP codepaths and enable redeeming of TAP RAVs.

2. **Indexer Service**

   - Fully replace your current configuration with the [new Indexer Service rs](https://github.com/graphprotocol/indexer-rs). It's recommend that you use the [container image](https://github.com/orgs/graphprotocol/packages?repo_name=indexer-rs).
   - Like the older version, you can scale Indexer Service horizontally easily. It is still stateless.

3. **TAP Agent**

   - Run _one_ single instance of [TAP Agent](https://github.com/graphprotocol/indexer-rs) at all times. It's recommend that you use the [container image](https://github.com/orgs/graphprotocol/packages?repo_name=indexer-rs).

4. **Configure Indexer Service and TAP Agent**

   Configuration is a TOML file shared between `indexer-service` and `tap-agent`, supplied with the argument `--config /path/to/config.toml`.

   Check out the full [configuration](https://github.com/graphprotocol/indexer-rs/blob/main/config/maximal-config-example.toml) and the [default values](https://github.com/graphprotocol/indexer-rs/blob/main/config/default_values.toml)

For minimal configuration, use the following template:

```bash
# You will have to change *all* the values below to match your setup.
#
# Some of the config below are global graph network values, which you can find here:
# <https://github.com/graphprotocol/indexer/tree/main/docs/networks>
#
# Pro tip: if you need to load some values from the environment into this config, you
# can overwrite with environment variables. For example, the following can be replaced
# by [PREFIX]_DATABASE_POSTGRESURL, where PREFIX can be `INDEXER_SERVICE` or `TAP_AGENT`:
#
# [database]
# postgres_url = "postgresql://indexer:${POSTGRES_PASSWORD}@postgres:5432/indexer_components_0"

[indexer]
indexer_address = "0x1111111111111111111111111111111111111111"
operator_mnemonic = "celery smart tip orange scare van steel radio dragon joy alarm crane"

[database]
# The URL of the Postgres database used for the indexer components. The same database
# that is used by the `indexer-agent`. It is expected that `indexer-agent` will create
# the necessary tables.
postgres_url = "postgres://postgres@postgres:5432/postgres"

[graph_node]
# URL to your graph-node's query endpoint
query_url = "<http://graph-node:8000>"
# URL to your graph-node's status endpoint
status_url = "<http://graph-node:8000/graphql>"

[subgraphs.network]
# Query URL for the Graph Network subgraph.
query_url = "<http://example.com/network-subgraph>"
# Optional, deployment to look for in the local `graph-node`, if locally indexed.
# Locally indexing the subgraph is recommended.
# NOTE: Use `query_url` or `deployment_id` only
deployment_id = "Qmaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"

[subgraphs.escrow]
# Query URL for the Escrow subgraph.
query_url = "<http://example.com/network-subgraph>"
# Optional, deployment to look for in the local `graph-node`, if locally indexed.
# Locally indexing the subgraph is recommended.
# NOTE: Use `query_url` or `deployment_id` only
deployment_id = "Qmaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"

[blockchain]
# The chain ID of the network that the graph network is running on
chain_id = 1337
# Contract address of TAP's receipt aggregate voucher (RAV) verifier.
receipts_verifier_address = "0x2222222222222222222222222222222222222222"

########################################
# Specific configurations to tap-agent #
########################################
[tap]
# This is the amount of fees you are willing to risk at any given time. For ex.
# if the sender stops supplying RAVs for long enough and the fees exceed this
# amount, the indexer-service will stop accepting queries from the sender
# until the fees are aggregated.
# NOTE: Use strings for decimal values to prevent rounding errors
# e.g:
# max_amount_willing_to_lose_grt = "0.1"
max_amount_willing_to_lose_grt = 20

[tap.sender_aggregator_endpoints]
# Key-Value of all senders and their aggregator endpoints
# This one below is for the E&N testnet gateway for example.
0xDDE4cfFd3D9052A9cb618fC05a1Cd02be1f2F467 = "https://tap-aggregator.network.thegraph.com"
```

Notes:

- Values for `tap.sender_aggregator_endpoints` can be found in the [gateway section](/tap/#gateway).
- Values for `blockchain.receipts_verifier_address` must be used accordingly to the [Blockchain addresses section](/tap/#contracts) using the appropriate chain id.

**Log Level**

- You can set the log level by using the `RUST_LOG` environment variable.
- It’s recommended that you set it to `RUST_LOG=indexer_tap_agent=debug,info`.

## Monitoring

### Metrics

All components expose the port 7300 to be queried by prometheus.

### Grafana Dashboard

You can download [Grafana Dashboard](https://github.com/graphprotocol/indexer-rs/blob/main/docs/dashboard.json) and import.

### Launchpad

Currently, there is a WIP version of `indexer-rs` and `tap-agent` that can be found [here](https://github.com/graphops/launchpad-charts/tree/feat/indexer-rs/charts/graph-network-indexer)
---
title: Supported Networks
---

import { getStaticPropsForSupportedNetworks } from '@/src/buildGetStaticProps'
import { SupportedNetworksTable } from '@/src/supportedNetworks'

export const getStaticProps = getStaticPropsForSupportedNetworks(__filename)

<SupportedNetworksTable networks={props.networks} />

\* Baseline network support provided by the [upgrade Indexer](https://thegraph.com/blog/upgrade-indexer/).  
\*\* Integration with Graph Node: `evm`, `near`, `cosmos`, `osmosis` and `ar` have native handler and type support in Graph Node. Chains which are Firehose- and Substreams-compatible can leverage the generalised [Substreams-powered subgraph](/cookbook/substreams-powered-subgraphs) integration (this includes `evm` and `near` networks). &#8288;<sup>†</sup> Supports deployment of [Substreams-powered subgraphs](/cookbook/substreams-powered-subgraphs).

- Subgraph Studio relies on the stability and reliability of the underlying technologies, for example JSON-RPC, Firehose and Substreams endpoints.
- Subgraphs indexing Gnosis Chain can now be deployed with the `gnosis` network identifier.
- If a subgraph was published via the CLI and picked up by an Indexer, it could technically be queried even without support, and efforts are underway to further streamline integration of new networks.
- For a full list of which features are supported on the decentralized network, see [this page](https://github.com/graphprotocol/indexer/blob/main/docs/feature-support-matrix.md).

## Running Graph Node locally

If your preferred network isn't supported on The Graph's decentralized network, you can run your own [Graph Node](https://github.com/graphprotocol/graph-node) to index any EVM-compatible network. Make sure that the [version](https://github.com/graphprotocol/graph-node/releases) you are using supports the network and you have the needed configuration.

Graph Node can also index other protocols, via a Firehose integration. Firehose integrations have been created for NEAR, Arweave and Cosmos-based networks. Additionally, Graph Node can support Substreams-powered subgraphs for any network with Substreams support.
---
title: Substreams-powered subgraphs FAQ
---

## What are Substreams?

Developed by [StreamingFast](https://www.streamingfast.io/), Substreams is an exceptionally powerful processing engine capable of consuming rich streams of blockchain data. Substreams allow you to refine and shape blockchain data for fast and seamless digestion by end-user applications. More specifically, Substreams is a blockchain-agnostic, parallelized, and streaming-first engine, serving as a blockchain data transformation layer. Powered by the [Firehose](https://firehose.streamingfast.io/), it ​​enables developers to write Rust modules, build upon community modules, provide extremely high-performance indexing, and [sink](https://substreams.streamingfast.io/reference-and-specs/manifests#sink) their data anywhere.

Go to the [Substreams Documentation](/substreams) to learn more about Substreams.

## What are Substreams-powered subgraphs?

[Substreams-powered subgraphs](/cookbook/substreams-powered-subgraphs/) combine the power of Substreams with the queryability of subgraphs. When publishing a Substreams-powered Subgraph, the data produced by the Substreams transformations, can [output entity changes](https://github.com/streamingfast/substreams-sink-entity-changes/blob/develop/substreams-entity-change/src/tables.rs), which are compatible with subgraph entities.

If you are already familiar with subgraph development, then note that Substreams-powered subgraphs can then be queried, just as if it had been produced by the AssemblyScript transformation layer, with all the Subgraph benefits, like providing a dynamic and flexible GraphQL API.

## How are Substreams-powered subgraphs different from subgraphs?

Subgraphs are made up of datasources which specify on-chain events, and how those events should be transformed via handlers written in Assemblyscript. These events are processed sequentially, based on the order in which events happen on-chain.

By contrast, substreams-powered subgraphs have a single datasource which references a substreams package, which is processed by the Graph Node. Substreams have access to additional granular on-chain data compared to conventional subgraphs, and can also benefit from massively parallelised processing, which can mean much faster processing times.

## What are the benefits of using Substreams-powered subgraphs?

Substreams-powered subgraphs combine all the benefits of Substreams with the queryability of subgraphs. They bring greater composability and high-performance indexing to The Graph. They also enable new data use cases; for example, once you've built your Substreams-powered Subgraph, you can reuse your [Substreams modules](https://substreams.streamingfast.io/documentation/develop/manifest-modules) to output to different [sinks](https://substreams.streamingfast.io/reference-and-specs/manifests#sink) such as PostgreSQL, MongoDB, and Kafka.

## What are the benefits of Substreams?

There are many benefits to using Substreams, including:

- Composable: You can stack Substreams modules like LEGO blocks, and build upon community modules, further refining public data.

- High-performance indexing: Orders of magnitude faster indexing through large-scale clusters of parallel operations (think BigQuery).

- Sink anywhere: Sink your data to anywhere you want: PostgreSQL, MongoDB, Kafka, subgraphs, flat files, Google Sheets.

- Programmable: Use code to customize extraction, do transformation-time aggregations, and model your output for multiple sinks.

- Access to additional data which is not available as part of the JSON RPC

- All the benefits of the Firehose.

## What is the Firehose?

Developed by [StreamingFast](https://www.streamingfast.io/), the Firehose is a blockchain data extraction layer designed from scratch to process the full history of blockchains at speeds that were previously unseen. Providing a files-based and streaming-first approach, it is a core component of StreamingFast's suite of open-source technologies and the foundation for Substreams.

Go to the [documentation](https://firehose.streamingfast.io/) to learn more about the Firehose.

## What are the benefits of the Firehose?

There are many benefits to using Firehose, including:

- Lowest latency & no polling: In a streaming-first fashion, the Firehose nodes are designed to race to push out the block data first.

- Prevents downtimes: Designed from the ground up for High Availability.

- Never miss a beat: The Firehose stream cursor is designed to handle forks and to continue where you left off in any condition.

- Richest data model:  Best data model that includes the balance changes, the full call tree, internal transactions, logs, storage changes, gas costs, and more.

- Leverages flat files: Blockchain data is extracted into flat files, the cheapest and most optimized computing resource available.

## Where can developers access more information about Substreams-powered subgraphs and Substreams?

The [Substreams documentation](/substreams) will teach you how to build Substreams modules.

The [Substreams-powered subgraphs documentation](/cookbook/substreams-powered-subgraphs/) will show you how to package them for deployment on The Graph.

The [latest Substreams Codegen tool](https://streamingfastio.medium.com/substreams-codegen-no-code-tool-to-bootstrap-your-project-a11efe0378c6) will allow you to bootstrap a Substreams project without any code.

## What is the role of Rust modules in Substreams?

Rust modules are the equivalent of the AssemblyScript mappers in subgraphs. They are compiled to WASM in a similar way, but the programming model allows for parallel execution. They define the sort of transformations and aggregations you want to apply to the raw blockchain data.

See [modules documentation](https://substreams.streamingfast.io/documentation/develop/manifest-modules) for details.

## What makes Substreams composable?

When using Substreams, the composition happens at the transformation layer enabling cached modules to be re-used.

As an example, Alice can build a DEX price module, Bob can use it to build a volume aggregator for some tokens of his interest, and Lisa can combine four individual DEX price modules to create a price oracle. A single Substreams request will package all of these individual's modules, link them together, to offer a much more refined stream of data. That stream can then be used to populate a subgraph, and be queried by consumers.

## How can you build and deploy a Substreams-powered Subgraph?

After [defining](/cookbook/substreams-powered-subgraphs/) a Substreams-powered Subgraph, you can use the Graph CLI to deploy it in [Subgraph Studio](https://thegraph.com/studio/).

## Where can I find examples of Substreams and Substreams-powered subgraphs?

You can visit [this Github repo](https://github.com/pinax-network/awesome-substreams) to find examples of Substreams and Substreams-powered subgraphs.

## What do Substreams and Substreams-powered subgraphs mean for The Graph Network?

The integration promises many benefits, including extremely high-performance indexing and greater composability by leveraging community modules and building on them.
---
title: Unit Testing Framework
---

Matchstick is a unit testing framework, developed by [LimeChain](https://limechain.tech/), that enables subgraph developers to test their mapping logic in a sandboxed environment and deploy their subgraphs with confidence!

## Getting Started

### Install dependencies

In order to use the test helper methods and run the tests, you will need to install the following dependencies:

```sh
yarn add --dev matchstick-as
```

❗ `graph-node` depends on PostgreSQL, so if you don't already have it, you will need to install it. We highly advise using the commands below as adding it in any other way may cause unexpected errors!

#### MacOS

Postgres installation command:

```sh
brew install postgresql
```

Create a symlink to the latest libpq.5.lib _You may need to create this dir first_ `/usr/local/opt/postgresql/lib/`

```sh
ln -sf /usr/local/opt/postgresql@14/lib/postgresql@14/libpq.5.dylib /usr/local/opt/postgresql/lib/libpq.5.dylib
```

#### Linux

Postgres installation command (depends on your distro):

```sh
sudo apt install postgresql
```

### WSL (Windows Subsystem for Linux)

You can use Matchstick on WSL both using the Docker approach and the binary approach. As WSL can be a bit tricky, here's a few tips in case you encounter issues like

```
static BYTES = Symbol("Bytes") SyntaxError: Unexpected token =
```

or

```
<PROJECT_PATH>/node_modules/gluegun/build/index.js:13 throw up;
```

Please make sure you're on a newer version of Node.js graph-cli doesn't support **v10.19.0** anymore, and that is still the default version for new Ubuntu images on WSL. For instance Matchstick is confirmed to be working on WSL with **v18.1.0**, you can switch to it either via **nvm** or if you update your global Node.js. Don't forget to delete `node_modules` and to run `npm install` again after updating you nodejs! Then, make sure you have **libpq** installed, you can do that by running

```
sudo apt-get install libpq-dev
```

And finally, do not use `graph test` (which uses your global installation of graph-cli and for some reason that looks like it's broken on WSL currently), instead use `yarn test` or `npm run test` (that will use the local, project-level instance of graph-cli, which works like a charm). For that you would of course need to have a `"test"` script in your `package.json` file which can be something as simple as

```json
{
  "name": "demo-subgraph",
  "version": "0.1.0",
  "scripts": {
    "test": "graph test",
    ...
  },
  "dependencies": {
    "@graphprotocol/graph-cli": "^0.56.0",
    "@graphprotocol/graph-ts": "^0.31.0",
    "matchstick-as": "^0.6.0"
  }
}
```

### Usage

To use **Matchstick** in your subgraph project just open up a terminal, navigate to the root folder of your project and simply run `graph test [options] <datasource>` - it downloads the latest **Matchstick** binary and runs the specified test or all tests in a test folder (or all existing tests if no datasource flag is specified).

### CLI options

This will run all tests in the test folder:

```sh
graph test
```

This will run a test named gravity.test.ts and/or all test inside of a folder named gravity:

```sh
graph test gravity
```

This will run only that specific test file:

```sh
graph test path/to/file.test.ts
```

**Options:**

```sh
-c, --coverage                Run the tests in coverage mode
-d, --docker                  Run the tests in a docker container (Note: Please execute from the root folder of the subgraph)
-f, --force                   Binary: Redownloads the binary. Docker: Redownloads the Dockerfile and rebuilds the docker image.
-h, --help                    Show usage information
-l, --logs                    Logs to the console information about the OS, CPU model and download url (debugging purposes)
-r, --recompile               Forces tests to be recompiled
-v, --version <tag>           Choose the version of the rust binary that you want to be downloaded/used
```

### Docker

From `graph-cli 0.25.2`, the `graph test` command supports running `matchstick` in a docker container with the `-d` flag. The docker implementation uses [bind mount](https://docs.docker.com/storage/bind-mounts/) so it does not have to rebuild the docker image every time the `graph test -d` command is executed. Alternatively you can follow the instructions from the [matchstick](https://github.com/LimeChain/matchstick#docker-) repository to run docker manually.

❗ `graph test -d` forces `docker run` to run with flag `-t`. This must be removed to run inside non-interactive environments (like GitHub CI).

❗ If you have previously ran `graph test` you may encounter the following error during docker build:

```sh
  error from sender: failed to xattr node_modules/binary-install-raw/bin/binary-<platform>: permission denied
```

In this case create a `.dockerignore` in the root folder and add `node_modules/binary-install-raw/bin`

### Configuration

Matchstick can be configured to use a custom tests, libs and manifest path via `matchstick.yaml` config file:

```yaml
testsFolder: path/to/tests
libsFolder: path/to/libs
manifestPath: path/to/subgraph.yaml
```

### Demo subgraph

You can try out and play around with the examples from this guide by cloning the [Demo Subgraph repo](https://github.com/LimeChain/demo-subgraph)

### Video tutorials

Also you can check out the video series on ["How to use Matchstick to write unit tests for your subgraphs"](https://www.youtube.com/playlist?list=PLTqyKgxaGF3SNakGQwczpSGVjS_xvOv3h)

## Tests structure

_**IMPORTANT: The test structure described below depens on `matchstick-as` version >=0.5.0**_

### describe()

`describe(name: String , () => {})` - Defines a test group.

**_Notes:_**

- _Describes are not mandatory. You can still use test() the old way, outside of the describe() blocks_

Example:

```typescript
import { describe, test } from "matchstick-as/assembly/index"
import { handleNewGravatar } from "../../src/gravity"

describe("handleNewGravatar()", () => {
  test("Should create a new Gravatar entity", () => {
    ...
  })
})
```

Nested `describe()` example:

```typescript
import { describe, test } from "matchstick-as/assembly/index"
import { handleUpdatedGravatar } from "../../src/gravity"

describe("handleUpdatedGravatar()", () => {
  describe("When entity exists", () => {
    test("updates the entity", () => {
      ...
    })
  })

  describe("When entity does not exists", () => {
    test("it creates a new entity", () => {
      ...
    })
  })
})
```

---

### test()

`test(name: String, () =>, should_fail: bool)` - Defines a test case. You can use test() inside of describe() blocks or independently.

Example:

```typescript
import { describe, test } from "matchstick-as/assembly/index"
import { handleNewGravatar } from "../../src/gravity"

describe("handleNewGravatar()", () => {
  test("Should create a new Entity", () => {
    ...
  })
})
```

or

```typescript
test("handleNewGravatar() should create a new entity", () => {
  ...
})


```

---

### beforeAll()

Runs a code block before any of the tests in the file. If `beforeAll` is declared inside of a `describe` block, it runs at the beginning of that `describe` block.

Examples:

Code inside `beforeAll` will execute once before _all_ tests in the file.

```typescript
import { describe, test, beforeAll } from "matchstick-as/assembly/index"
import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"
import { Gravatar } from "../../generated/schema"

beforeAll(() => {
  let gravatar = new Gravatar("0x0")
  gravatar.displayName = “First Gravatar”
  gravatar.save()
  ...
})

describe("When the entity does not exist", () => {
  test("it should create a new Gravatar with id 0x1", () => {
    ...
  })
})

describe("When entity already exists", () => {
  test("it should update the Gravatar with id 0x0", () => {
    ...
  })
})
```

Code inside `beforeAll` will execute once before all tests in the first describe block

```typescript
import { describe, test, beforeAll } from "matchstick-as/assembly/index"
import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"
import { Gravatar } from "../../generated/schema"

describe("handleUpdatedGravatar()", () => {
  beforeAll(() => {
    let gravatar = new Gravatar("0x0")
    gravatar.displayName = “First Gravatar”
    gravatar.save()
    ...
  })

  test("updates Gravatar with id 0x0", () => {
    ...
  })

  test("creates new Gravatar with id 0x1", () => {
    ...
  })
})
```

---

### afterAll()

Runs a code block after all of the tests in the file. If `afterAll` is declared inside of a `describe` block, it runs at the end of that `describe` block.

Example:

Code inside `afterAll` will execute once after _all_ tests in the file.

```typescript
import { describe, test, afterAll } from "matchstick-as/assembly/index"
import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"
import { store } from "@graphprotocol/graph-ts"

afterAll(() => {
  store.remove("Gravatar", "0x0")
  ...
})

describe("handleNewGravatar, () => {
  test("creates Gravatar with id 0x0", () => {
    ...
  })
})

describe("handleUpdatedGravatar", () => {
  test("updates Gravatar with id 0x0", () => {
    ...
  })
})
```

Code inside `afterAll` will execute once after all tests in the first describe block

```typescript
import { describe, test, afterAll, clearStore } from "matchstick-as/assembly/index"
import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"

describe("handleNewGravatar", () => {
	afterAll(() => {
    store.remove("Gravatar", "0x1")
    ...
	})

  test("It creates a new entity with Id 0x0", () => {
    ...
  })

  test("It creates a new entity with Id 0x1", () => {
    ...
  })
})

describe("handleUpdatedGravatar", () => {
  test("updates Gravatar with id 0x0", () => {
    ...
  })
})
```

---

### beforeEach()

Runs a code block before every test. If `beforeEach` is declared inside of a `describe` block, it runs before each test in that `describe` block.

Examples: Code inside `beforeEach` will execute before each tests.

```typescript
import { describe, test, beforeEach, clearStore } from "matchstick-as/assembly/index"
import { handleNewGravatars } from "./utils"

beforeEach(() => {
  clearStore() // <-- clear the store before each test in the file
})

describe("handleNewGravatars, () => {
  test("A test that requires a clean store", () => {
    ...
  })

  test("Second that requires a clean store", () => {
    ...
  })
})

 ...
```

Code inside `beforeEach` will execute only before each test in the that describe

```typescript
import { describe, test, beforeEach } from 'matchstick-as/assembly/index'
import { handleUpdatedGravatar, handleNewGravatar } from '../../src/gravity'

describe('handleUpdatedGravatars', () => {
  beforeEach(() => {
    let gravatar = new Gravatar('0x0')
    gravatar.displayName = 'First Gravatar'
    gravatar.imageUrl = ''
    gravatar.save()
  })

  test('Upates the displayName', () => {
    assert.fieldEquals('Gravatar', '0x0', 'displayName', 'First Gravatar')

    // code that should update the displayName to 1st Gravatar

    assert.fieldEquals('Gravatar', '0x0', 'displayName', '1st Gravatar')
    store.remove('Gravatar', '0x0')
  })

  test('Updates the imageUrl', () => {
    assert.fieldEquals('Gravatar', '0x0', 'imageUrl', '')

    // code that should changes the imageUrl to https://www.gravatar.com/avatar/0x0

    assert.fieldEquals('Gravatar', '0x0', 'imageUrl', 'https://www.gravatar.com/avatar/0x0')
    store.remove('Gravatar', '0x0')
  })
})
```

---

### afterEach()

Runs a code block after every test. If `afterEach` is declared inside of a `describe` block, it runs after each test in that `describe` block.

Examples:

Code inside `afterEach` will execute after every test.

```typescript
import { describe, test, beforeEach, afterEach } from "matchstick-as/assembly/index"
import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"

beforeEach(() => {
  let gravatar = new Gravatar("0x0")
  gravatar.displayName = “First Gravatar”
  gravatar.save()
})

afterEach(() => {
  store.remove("Gravatar", "0x0")
})

describe("handleNewGravatar", () => {
  ...
})

describe("handleUpdatedGravatar", () => {
  test("Upates the displayName", () => {
     assert.fieldEquals("Gravatar", "0x0", "displayName", "First Gravatar")

    // code that should update the displayName to 1st Gravatar

    assert.fieldEquals("Gravatar", "0x0", "displayName", "1st Gravatar")
  })

  test("Updates the imageUrl", () => {
    assert.fieldEquals("Gravatar", "0x0", "imageUrl", "")

    // code that should changes the imageUrl to https://www.gravatar.com/avatar/0x0

    assert.fieldEquals("Gravatar", "0x0", "imageUrl", "https://www.gravatar.com/avatar/0x0")
  })
})
```

Code inside `afterEach` will execute after each test in that describe

```typescript
import { describe, test, beforeEach, afterEach } from "matchstick-as/assembly/index"
import { handleUpdatedGravatar, handleNewGravatar } from "../../src/gravity"

describe("handleNewGravatar", () => {
  ...
})

describe("handleUpdatedGravatar", () => {
  beforeEach(() => {
    let gravatar = new Gravatar("0x0")
    gravatar.displayName = "First Gravatar"
    gravatar.imageUrl = ""
    gravatar.save()
  })

  afterEach(() => {
    store.remove("Gravatar", "0x0")
  })

  test("Upates the displayName", () => {
     assert.fieldEquals("Gravatar", "0x0", "displayName", "First Gravatar")

    // code that should update the displayName to 1st Gravatar

    assert.fieldEquals("Gravatar", "0x0", "displayName", "1st Gravatar")
  })

  test("Updates the imageUrl", () => {
    assert.fieldEquals("Gravatar", "0x0", "imageUrl", "")

    // code that should changes the imageUrl to https://www.gravatar.com/avatar/0x0

    assert.fieldEquals("Gravatar", "0x0", "imageUrl", "https://www.gravatar.com/avatar/0x0")
  })
})
```

## Asserts

```typescript
fieldEquals(entityType: string, id: string, fieldName: string, expectedVal: string)

equals(expected: ethereum.Value, actual: ethereum.Value)

notInStore(entityType: string, id: string)

addressEquals(address1: Address, address2: Address)

bytesEquals(bytes1: Bytes, bytes2: Bytes)

i32Equals(number1: i32, number2: i32)

bigIntEquals(bigInt1: BigInt, bigInt2: BigInt)

booleanEquals(bool1: boolean, bool2: boolean)

stringEquals(string1: string, string2: string)

arrayEquals(array1: Array<ethereum.Value>, array2: Array<ethereum.Value>)

tupleEquals(tuple1: ethereum.Tuple, tuple2: ethereum.Tuple)

assertTrue(value: boolean)

assertNull<T>(value: T)

assertNotNull<T>(value: T)

entityCount(entityType: string, expectedCount: i32)
```

As of version 0.6.0, asserts support custom error messages as well

```typescript
assert.fieldEquals('Gravatar', '0x123', 'id', '0x123', 'Id should be 0x123')
assert.equals(ethereum.Value.fromI32(1), ethereum.Value.fromI32(1), 'Value should equal 1')
assert.notInStore('Gravatar', '0x124', 'Gravatar should not be in store')
assert.addressEquals(Address.zero(), Address.zero(), 'Address should be zero')
assert.bytesEquals(Bytes.fromUTF8('0x123'), Bytes.fromUTF8('0x123'), 'Bytes should be equal')
assert.i32Equals(2, 2, 'I32 should equal 2')
assert.bigIntEquals(BigInt.fromI32(1), BigInt.fromI32(1), 'BigInt should equal 1')
assert.booleanEquals(true, true, 'Boolean should be true')
assert.stringEquals('1', '1', 'String should equal 1')
assert.arrayEquals([ethereum.Value.fromI32(1)], [ethereum.Value.fromI32(1)], 'Arrays should be equal')
assert.tupleEquals(
  changetype<ethereum.Tuple>([ethereum.Value.fromI32(1)]),
  changetype<ethereum.Tuple>([ethereum.Value.fromI32(1)]),
  'Tuples should be equal',
)
assert.assertTrue(true, 'Should be true')
assert.assertNull(null, 'Should be null')
assert.assertNotNull('not null', 'Should be not null')
assert.entityCount('Gravatar', 1, 'There should be 2 gravatars')
assert.dataSourceCount('GraphTokenLockWallet', 1, 'GraphTokenLockWallet template should have one data source')
assert.dataSourceExists(
  'GraphTokenLockWallet',
  Address.zero().toHexString(),
  'GraphTokenLockWallet should have a data source for zero address',
)
```

## Write a Unit Test

Let's see how a simple unit test would look like using the Gravatar examples in the [Demo Subgraph](https://github.com/LimeChain/demo-subgraph/blob/main/src/gravity.ts).

Assuming we have the following handler function (along with two helper functions to make our life easier):

```typescript
export function handleNewGravatar(event: NewGravatar): void {
  let gravatar = new Gravatar(event.params.id.toHex())
  gravatar.owner = event.params.owner
  gravatar.displayName = event.params.displayName
  gravatar.imageUrl = event.params.imageUrl
  gravatar.save()
}

export function handleNewGravatars(events: NewGravatar[]): void {
  events.forEach((event) => {
    handleNewGravatar(event)
  })
}

export function createNewGravatarEvent(
  id: i32,
  ownerAddress: string,
  displayName: string,
  imageUrl: string,
): NewGravatar {
  let mockEvent = newMockEvent()
  let newGravatarEvent = new NewGravatar(
    mockEvent.address,
    mockEvent.logIndex,
    mockEvent.transactionLogIndex,
    mockEvent.logType,
    mockEvent.block,
    mockEvent.transaction,
    mockEvent.parameters,
  )
  newGravatarEvent.parameters = new Array()
  let idParam = new ethereum.EventParam('id', ethereum.Value.fromI32(id))
  let addressParam = new ethereum.EventParam(
    'ownderAddress',
    ethereum.Value.fromAddress(Address.fromString(ownerAddress)),
  )
  let displayNameParam = new ethereum.EventParam('displayName', ethereum.Value.fromString(displayName))
  let imageUrlParam = new ethereum.EventParam('imageUrl', ethereum.Value.fromString(imageUrl))

  newGravatarEvent.parameters.push(idParam)
  newGravatarEvent.parameters.push(addressParam)
  newGravatarEvent.parameters.push(displayNameParam)
  newGravatarEvent.parameters.push(imageUrlParam)

  return newGravatarEvent
}
```

We first have to create a test file in our project. This is an example of how that might look like:

```typescript
import { clearStore, test, assert } from 'matchstick-as/assembly/index'
import { Gravatar } from '../../generated/schema'
import { NewGravatar } from '../../generated/Gravity/Gravity'
import { createNewGravatarEvent, handleNewGravatars } from '../mappings/gravity'

test('Can call mappings with custom events', () => {
  // Create a test entity and save it in the store as initial state (optional)
  let gravatar = new Gravatar('gravatarId0')
  gravatar.save()

  // Create mock events
  let newGravatarEvent = createNewGravatarEvent(12345, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')
  let anotherGravatarEvent = createNewGravatarEvent(3546, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')

  // Call mapping functions passing the events we just created
  handleNewGravatars([newGravatarEvent, anotherGravatarEvent])

  // Assert the state of the store
  assert.fieldEquals('Gravatar', 'gravatarId0', 'id', 'gravatarId0')
  assert.fieldEquals('Gravatar', '12345', 'owner', '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7')
  assert.fieldEquals('Gravatar', '3546', 'displayName', 'cap')

  // Clear the store in order to start the next test off on a clean slate
  clearStore()
})

test('Next test', () => {
  //...
})
```

That's a lot to unpack! First off, an important thing to notice is that we're importing things from `matchstick-as`, our AssemblyScript helper library (distributed as an npm module). You can find the repository [here](https://github.com/LimeChain/matchstick-as). `matchstick-as` provides us with useful testing methods and also defines the `test()` function which we will use to build our test blocks. The rest of it is pretty straightforward - here's what happens:

- We're setting up our initial state and adding one custom Gravatar entity;
- We define two `NewGravatar` event objects along with their data, using the `createNewGravatarEvent()` function;
- We're calling out handler methods for those events - `handleNewGravatars()` and passing in the list of our custom events;
- We assert the state of the store. How does that work? - We're passing a unique combination of Entity type and id. Then we check a specific field on that Entity and assert that it has the value we expect it to have. We're doing this both for the initial Gravatar Entity we added to the store, as well as the two Gravatar entities that gets added when the handler function is called;
- And lastly - we're cleaning the store using `clearStore()` so that our next test can start with a fresh and empty store object. We can define as many test blocks as we want.

There we go - we've created our first test! 👏

Now in order to run our tests you simply need to run the following in your subgraph root folder:

`graph test Gravity`

And if all goes well you should be greeted with the following:

![Matchstick saying “All tests passed!”](/img/matchstick-tests-passed.png)

## Common test scenarios

### Hydrating the store with a certain state

Users are able to hydrate the store with a known set of entities. Here's an example to initialise the store with a Gravatar entity:

```typescript
let gravatar = new Gravatar('entryId')
gravatar.save()
```

### Calling a mapping function with an event

A user can create a custom event and pass it to a mapping function that is bound to the store:

```typescript
import { store } from 'matchstick-as/assembly/store'
import { NewGravatar } from '../../generated/Gravity/Gravity'
import { handleNewGravatars, createNewGravatarEvent } from './mapping'

let newGravatarEvent = createNewGravatarEvent(12345, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')

handleNewGravatar(newGravatarEvent)
```

### Calling all of the mappings with event fixtures

Users can call the mappings with test fixtures.

```typescript
import { NewGravatar } from '../../generated/Gravity/Gravity'
import { store } from 'matchstick-as/assembly/store'
import { handleNewGravatars, createNewGravatarEvent } from './mapping'

let newGravatarEvent = createNewGravatarEvent(12345, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')

let anotherGravatarEvent = createNewGravatarEvent(3546, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'cap', 'pac')

handleNewGravatars([newGravatarEvent, anotherGravatarEvent])
```

```
export function handleNewGravatars(events: NewGravatar[]): void {
    events.forEach(event => {
        handleNewGravatar(event);
    });
}
```

### Mocking contract calls

Users can mock contract calls:

```typescript
import { addMetadata, assert, createMockedFunction, clearStore, test } from 'matchstick-as/assembly/index'
import { Gravity } from '../../generated/Gravity/Gravity'
import { Address, BigInt, ethereum } from '@graphprotocol/graph-ts'

let contractAddress = Address.fromString('0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7')
let expectedResult = Address.fromString('0x90cBa2Bbb19ecc291A12066Fd8329D65FA1f1947')
let bigIntParam = BigInt.fromString('1234')
createMockedFunction(contractAddress, 'gravatarToOwner', 'gravatarToOwner(uint256):(address)')
  .withArgs([ethereum.Value.fromSignedBigInt(bigIntParam)])
  .returns([ethereum.Value.fromAddress(Address.fromString('0x90cBa2Bbb19ecc291A12066Fd8329D65FA1f1947'))])

let gravity = Gravity.bind(contractAddress)
let result = gravity.gravatarToOwner(bigIntParam)

assert.equals(ethereum.Value.fromAddress(expectedResult), ethereum.Value.fromAddress(result))
```

As demonstrated, in order to mock a contract call and hardcore a return value, the user must provide a contract address, function name, function signature, an array of arguments, and of course - the return value.

Users can also mock function reverts:

```typescript
let contractAddress = Address.fromString('0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7')
createMockedFunction(contractAddress, 'getGravatar', 'getGravatar(address):(string,string)')
  .withArgs([ethereum.Value.fromAddress(contractAddress)])
  .reverts()
```

### Mocking IPFS files (from matchstick 0.4.1)

Users can mock IPFS files by using `mockIpfsFile(hash, filePath)` function. The function accepts two arguments, the first one is the IPFS file hash/path and the second one is the path to a local file.

NOTE: When testing `ipfs.map/ipfs.mapJSON`, the callback function must be exported from the test file in order for matchstck to detect it, like the `processGravatar()` function in the test example bellow:

`.test.ts` file:

```typescript
import { assert, test, mockIpfsFile } from 'matchstick-as/assembly/index'
import { ipfs } from '@graphprotocol/graph-ts'
import { gravatarFromIpfs } from './utils'

// Export ipfs.map() callback in order for matchstck to detect it
export { processGravatar } from './utils'

test('ipfs.cat', () => {
  mockIpfsFile('ipfsCatfileHash', 'tests/ipfs/cat.json')

  assert.entityCount(GRAVATAR_ENTITY_TYPE, 0)

  gravatarFromIpfs()

  assert.entityCount(GRAVATAR_ENTITY_TYPE, 1)
  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '1', 'imageUrl', 'https://i.ytimg.com/vi/MELP46s8Cic/maxresdefault.jpg')

  clearStore()
})

test('ipfs.map', () => {
  mockIpfsFile('ipfsMapfileHash', 'tests/ipfs/map.json')

  assert.entityCount(GRAVATAR_ENTITY_TYPE, 0)

  ipfs.map('ipfsMapfileHash', 'processGravatar', Value.fromString('Gravatar'), ['json'])

  assert.entityCount(GRAVATAR_ENTITY_TYPE, 3)
  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '1', 'displayName', 'Gravatar1')
  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '2', 'displayName', 'Gravatar2')
  assert.fieldEquals(GRAVATAR_ENTITY_TYPE, '3', 'displayName', 'Gravatar3')
})
```

`utils.ts` file:

```typescript
import { Address, ethereum, JSONValue, Value, ipfs, json, Bytes } from "@graphprotocol/graph-ts"
import { Gravatar } from "../../generated/schema"

...

// ipfs.map callback
export function processGravatar(value: JSONValue, userData: Value): void {
  // See the JSONValue documentation for details on dealing
  // with JSON values
  let obj = value.toObject()
  let id = obj.get('id')

  if (!id) {
    return
  }

  // Callbacks can also created entities
  let gravatar = new Gravatar(id.toString())
  gravatar.displayName = userData.toString() + id.toString()
  gravatar.save()
}

// function that calls ipfs.cat
export function gravatarFromIpfs(): void {
  let rawData = ipfs.cat("ipfsCatfileHash")

  if (!rawData) {
    return
  }

  let jsonData = json.fromBytes(rawData as Bytes).toObject()

  let id = jsonData.get('id')
  let url = jsonData.get("imageUrl")

  if (!id || !url) {
    return
  }

  let gravatar = new Gravatar(id.toString())
  gravatar.imageUrl = url.toString()
  gravatar.save()
}
```

### Asserting the state of the store

Users are able to assert the final (or midway) state of the store through asserting entities. In order to do this, the user has to supply an Entity type, the specific ID of an Entity, a name of a field on that Entity, and the expected value of the field. Here's a quick example:

```typescript
import { assert } from 'matchstick-as/assembly/index'
import { Gravatar } from '../generated/schema'

let gravatar = new Gravatar('gravatarId0')
gravatar.save()

assert.fieldEquals('Gravatar', 'gravatarId0', 'id', 'gravatarId0')
```

Running the assert.fieldEquals() function will check for equality of the given field against the given expected value. The test will fail and an error message will be outputted if the values are **NOT** equal. Otherwise the test will pass successfully.

### Interacting with Event metadata

Users can use default transaction metadata, which could be returned as an ethereum.Event by using the `newMockEvent()` function. The following example shows how you can read/write to those fields on the Event object:

```typescript
// Read
let logType = newGravatarEvent.logType

// Write
let UPDATED_ADDRESS = '0xB16081F360e3847006dB660bae1c6d1b2e17eC2A'
newGravatarEvent.address = Address.fromString(UPDATED_ADDRESS)
```

### Asserting variable equality

```typescript
assert.equals(ethereum.Value.fromString("hello"); ethereum.Value.fromString("hello"));
```

### Asserting that an Entity is **not** in the store

Users can assert that an entity does not exist in the store. The function takes an entity type and an id. If the entity is in fact in the store, the test will fail with a relevant error message. Here's a quick example of how to use this functionality:

```typescript
assert.notInStore('Gravatar', '23')
```

### Printing the whole store, or single entities from it (for debug purposes)

You can print the whole store to the console using this helper function:

```typescript
import { logStore } from 'matchstick-as/assembly/store'

logStore()
```

As of version 0.6.0, `logStore` no longer prints derived fields, instead users can use the new `logEntity` function. Of course `logEntity` can be used to print any entity, not just ones that have derived fields. `logEntity` takes the entity type, entity id and a `showRelated` flag to indicate if users want to print the related derived entities.

```
import { logEntity } from 'matchstick-as/assembly/store'


logEntity("Gravatar", 23, true)
```

### Expected failure

Users can have expected test failures, using the shouldFail flag on the test() functions:

```typescript
test(
  'Should throw an error',
  () => {
    throw new Error()
  },
  true,
)
```

If the test is marked with shouldFail = true but DOES NOT fail, that will show up as an error in the logs and the test block will fail. Also, if it's marked with shouldFail = false (the default state), the test executor will crash.

### Logging

Having custom logs in the unit tests is exactly the same as logging in the mappings. The difference is that the log object needs to be imported from matchstick-as rather than graph-ts. Here's a simple example with all non-critical log types:

```typescript
import { test } from "matchstick-as/assembly/index";
import { log } from "matchstick-as/assembly/log";

test("Success", () => {
    log.success("Success!". []);
});
test("Error", () => {
    log.error("Error :( ", []);
});
test("Debug", () => {
    log.debug("Debugging...", []);
});
test("Info", () => {
    log.info("Info!", []);
});
test("Warning", () => {
    log.warning("Warning!", []);
});
```

Users can also simulate a critical failure, like so:

```typescript
test('Blow everything up', () => {
  log.critical('Boom!')
})
```

Logging critical errors will stop the execution of the tests and blow everything up. After all - we want to make sure you're code doesn't have critical logs in deployment, and you should notice right away if that were to happen.

### Testing derived fields

Testing derived fields is a feature which allows users to set a field on a certain entity and have another entity be updated automatically if it derives one of its fields from the first entity.

Before version `0.6.0` it was possible to get the derived entities by accessing them as entity fields/properties, like so:

```typescript
let entity = ExampleEntity.load('id')
let derivedEntity = entity.derived_entity
```

As of version `0.6.0`, this is done by using the `loadRelated` function of graph-node, the derived entities can be accessed the same way as in the handlers.

```typescript
test('Derived fields example test', () => {
  let mainAccount = GraphAccount.load('12')!

  assert.assertNull(mainAccount.get('nameSignalTransactions'))
  assert.assertNull(mainAccount.get('operatorOf'))

  let operatedAccount = GraphAccount.load('1')!
  operatedAccount.operators = [mainAccount.id]
  operatedAccount.save()

  mockNameSignalTransaction('1234', mainAccount.id)
  mockNameSignalTransaction('2', mainAccount.id)

  mainAccount = GraphAccount.load('12')!

  assert.assertNull(mainAccount.get('nameSignalTransactions'))
  assert.assertNull(mainAccount.get('operatorOf'))

  const nameSignalTransactions = mainAccount.nameSignalTransactions.load()
  const operatorsOfMainAccount = mainAccount.operatorOf.load()

  assert.i32Equals(2, nameSignalTransactions.length)
  assert.i32Equals(1, operatorsOfMainAccount.length)

  assert.stringEquals('1', operatorsOfMainAccount[0].id)

  mockNameSignalTransaction('2345', mainAccount.id)

  let nst = NameSignalTransaction.load('1234')!
  nst.signer = '11'
  nst.save()

  store.remove('NameSignalTransaction', '2')

  mainAccount = GraphAccount.load('12')!
  assert.i32Equals(1, mainAccount.nameSignalTransactions.load().length)
})
```

### Testing `loadInBlock`

As of version `0.6.0`, users can test `loadInBlock` by using the `mockInBlockStore`, it allows mocking entities in the block cache.

```typescript
import { afterAll, beforeAll, describe, mockInBlockStore, test } from 'matchstick-as'
import { Gravatar } from '../../generated/schema'

describe('loadInBlock', () => {
  beforeAll(() => {
    mockInBlockStore('Gravatar', 'gravatarId0', gravatar)
  })

  afterAll(() => {
    clearInBlockStore()
  })

  test('Can use entity.loadInBlock() to retrieve entity from cache store in the current block', () => {
    let retrievedGravatar = Gravatar.loadInBlock('gravatarId0')
    assert.stringEquals('gravatarId0', retrievedGravatar!.get('id')!.toString())
  })

  test("Returns null when calling entity.loadInBlock() if an entity doesn't exist in the current block", () => {
    let retrievedGravatar = Gravatar.loadInBlock('IDoNotExist')
    assert.assertNull(retrievedGravatar)
  })
})
```

### Testing dynamic data sources

Testing dynamic data sources can be be done by mocking the return value of the `context()`, `address()` and `network()` functions of the dataSource namespace. These functions currently return the following: `context()` - returns an empty entity (DataSourceContext), `address()` - returns `0x0000000000000000000000000000000000000000`, `network()` - returns `mainnet`. The `create(...)` and `createWithContext(...)` functions are mocked to do nothing so they don't need to be called in the tests at all. Changes to the return values can be done through the functions of the `dataSourceMock` namespace in `matchstick-as` (version 0.3.0+).

Example below:

First we have the following event handler (which has been intentionally repurposed to showcase datasource mocking):

```typescript
export function handleApproveTokenDestinations(event: ApproveTokenDestinations): void {
  let tokenLockWallet = TokenLockWallet.load(dataSource.address().toHexString())!
  if (dataSource.network() == 'rinkeby') {
    tokenLockWallet.tokenDestinationsApproved = true
  }
  let context = dataSource.context()
  if (context.get('contextVal')!.toI32() > 0) {
    tokenLockWallet.setBigInt('tokensReleased', BigInt.fromI32(context.get('contextVal')!.toI32()))
  }
  tokenLockWallet.save()
}
```

And then we have the test using one of the methods in the dataSourceMock namespace to set a new return value for all of the dataSource functions:

```typescript
import { assert, test, newMockEvent, dataSourceMock } from 'matchstick-as/assembly/index'
import { BigInt, DataSourceContext, Value } from '@graphprotocol/graph-ts'

import { handleApproveTokenDestinations } from '../../src/token-lock-wallet'
import { ApproveTokenDestinations } from '../../generated/templates/GraphTokenLockWallet/GraphTokenLockWallet'
import { TokenLockWallet } from '../../generated/schema'

test('Data source simple mocking example', () => {
  let addressString = '0xA16081F360e3847006dB660bae1c6d1b2e17eC2A'
  let address = Address.fromString(addressString)

  let wallet = new TokenLockWallet(address.toHexString())
  wallet.save()
  let context = new DataSourceContext()
  context.set('contextVal', Value.fromI32(325))
  dataSourceMock.setReturnValues(addressString, 'rinkeby', context)
  let event = changetype<ApproveTokenDestinations>(newMockEvent())

  assert.assertTrue(!wallet.tokenDestinationsApproved)

  handleApproveTokenDestinations(event)

  wallet = TokenLockWallet.load(address.toHexString())!
  assert.assertTrue(wallet.tokenDestinationsApproved)
  assert.bigIntEquals(wallet.tokensReleased, BigInt.fromI32(325))

  dataSourceMock.resetValues()
})
```

Notice that dataSourceMock.resetValues() is called at the end. That's because the values are remembered when they are changed and need to be reset if you want to go back to the default values.

### Testing dynamic data source creation

As of version `0.6.0`, it is possible to test if a new data source has been created from a template. This feature supports both ethereum/contract and file/ipfs templates. There are four functions for this:

- `assert.dataSourceCount(templateName, expectedCount)` can be used to assert the expected count of data sources from the specified template
- `assert.dataSourceExists(templateName, address/ipfsHash)` asserts that a data source with the specified identifier (could be a contract address or IPFS file hash) from a specified template was created
- `logDataSources(templateName)` prints all data sources from the specified template to the console for debugging purposes
- `readFile(path)` reads a JSON file that represents an IPFS file and returns the content as Bytes

#### Testing `ethereum/contract` templates

```typescript
test('ethereum/contract dataSource creation example', () => {
  // Assert there are no dataSources created from GraphTokenLockWallet template
  assert.dataSourceCount('GraphTokenLockWallet', 0)

  // Create a new GraphTokenLockWallet datasource with address 0xA16081F360e3847006dB660bae1c6d1b2e17eC2A
  GraphTokenLockWallet.create(Address.fromString('0xA16081F360e3847006dB660bae1c6d1b2e17eC2A'))

  // Assert the dataSource has been created
  assert.dataSourceCount('GraphTokenLockWallet', 1)

  // Add a second dataSource with context
  let context = new DataSourceContext()
  context.set('contextVal', Value.fromI32(325))

  GraphTokenLockWallet.createWithContext(Address.fromString('0xA16081F360e3847006dB660bae1c6d1b2e17eC2B'), context)

  // Assert there are now 2 dataSources
  assert.dataSourceCount('GraphTokenLockWallet', 2)

  // Assert that a dataSource with address "0xA16081F360e3847006dB660bae1c6d1b2e17eC2B" was created
  // Keep in mind that `Address` type is transformed to lower case when decoded, so you have to pass the address as all lower case when asserting if it exists
  assert.dataSourceExists('GraphTokenLockWallet', '0xA16081F360e3847006dB660bae1c6d1b2e17eC2B'.toLowerCase())

  logDataSources('GraphTokenLockWallet')
})
```

##### Example `logDataSource` output

```bash
🛠  {
  "0xa16081f360e3847006db660bae1c6d1b2e17ec2a": {
    "kind": "ethereum/contract",
    "name": "GraphTokenLockWallet",
    "address": "0xa16081f360e3847006db660bae1c6d1b2e17ec2a",
    "context": null
  },
  "0xa16081f360e3847006db660bae1c6d1b2e17ec2b": {
    "kind": "ethereum/contract",
    "name": "GraphTokenLockWallet",
    "address": "0xa16081f360e3847006db660bae1c6d1b2e17ec2b",
    "context": {
      "contextVal": {
        "type": "Int",
        "data": 325
      }
    }
  }
}
```

#### Testing `file/ipfs` templates

Similarly to contract dynamic data sources, users can test test file datas sources and their handlers

##### Example `subgraph.yaml`

```yaml
...
templates:
 - kind: file/ipfs
    name: GraphTokenLockMetadata
    network: mainnet
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      file: ./src/token-lock-wallet.ts
      handler: handleMetadata
      entities:
        - TokenLockMetadata
      abis:
        - name: GraphTokenLockWallet
          file: ./abis/GraphTokenLockWallet.json
```

##### Example `schema.graphql`

```graphql
"""
Token Lock Wallets which hold locked GRT
"""
type TokenLockMetadata @entity {
  "The address of the token lock wallet"
  id: ID!
  "Start time of the release schedule"
  startTime: BigInt!
  "End time of the release schedule"
  endTime: BigInt!
  "Number of periods between start time and end time"
  periods: BigInt!
  "Time when the releases start"
  releaseStartTime: BigInt!
}
```

##### Example `metadata.json`

```json
{
  "startTime": 1,
  "endTime": 1,
  "periods": 1,
  "releaseStartTime": 1
}
```

##### Example handler

```typescript
export function handleMetadata(content: Bytes): void {
  // dataSource.stringParams() returns the File DataSource CID
  // stringParam() will be mocked in the handler test
  // for more info https://thegraph.com/docs/en/developing/creating-a-subgraph/#create-a-new-handler-to-process-files
  let tokenMetadata = new TokenLockMetadata(dataSource.stringParam())
  const value = json.fromBytes(content).toObject()

  if (value) {
    const startTime = value.get('startTime')
    const endTime = value.get('endTime')
    const periods = value.get('periods')
    const releaseStartTime = value.get('releaseStartTime')

    if (startTime && endTime && periods && releaseStartTime) {
      tokenMetadata.startTime = startTime.toBigInt()
      tokenMetadata.endTime = endTime.toBigInt()
      tokenMetadata.periods = periods.toBigInt()
      tokenMetadata.releaseStartTime = releaseStartTime.toBigInt()
    }

    tokenMetadata.save()
  }
}
```

##### Example test

```typescript
import { assert, test, dataSourceMock, readFile } from 'matchstick-as'
import { Address, BigInt, Bytes, DataSourceContext, ipfs, json, store, Value } from '@graphprotocol/graph-ts'

import { handleMetadata } from '../../src/token-lock-wallet'
import { TokenLockMetadata } from '../../generated/schema'
import { GraphTokenLockMetadata } from '../../generated/templates'

test('file/ipfs dataSource creation example', () => {
  // Generate the dataSource CID from the ipfsHash + ipfs path file
  // For example QmaXzZhcYnsisuue5WRdQDH6FDvqkLQX1NckLqBYeYYEfm/example.json
  const ipfshash = 'QmaXzZhcYnsisuue5WRdQDH6FDvqkLQX1NckLqBYeYYEfm'
  const CID = `${ipfshash}/example.json`

  // Create a new dataSource using the generated CID
  GraphTokenLockMetadata.create(CID)

  // Assert the dataSource has been created
  assert.dataSourceCount('GraphTokenLockMetadata', 1)
  assert.dataSourceExists('GraphTokenLockMetadata', CID)
  logDataSources('GraphTokenLockMetadata')

  // Now we have to mock the dataSource metadata and specifically dataSource.stringParam()
  // dataSource.stringParams actually uses the value of dataSource.address(), so we will mock the address using dataSourceMock from  matchstick-as
  // First we will reset the values and then use dataSourceMock.setAddress() to set the CID
  dataSourceMock.resetValues()
  dataSourceMock.setAddress(CID)

  // Now we need to generate the Bytes to pass to the dataSource handler
  // For this case we introduced a new function readFile, that reads a local json and returns the content as Bytes
  const content = readFile(`path/to/metadata.json`)
  handleMetadata(content)

  // Now we will test if a TokenLockMetadata was created
  const metadata = TokenLockMetadata.load(CID)

  assert.bigIntEquals(metadata!.endTime, BigInt.fromI32(1))
  assert.bigIntEquals(metadata!.periods, BigInt.fromI32(1))
  assert.bigIntEquals(metadata!.releaseStartTime, BigInt.fromI32(1))
  assert.bigIntEquals(metadata!.startTime, BigInt.fromI32(1))
})
```

## Test Coverage

Using **Matchstick**, subgraph developers are able to run a script that will calculate the test coverage of the written unit tests.

The test coverage tool takes the compiled test `wasm` binaries and converts them to `wat` files, which can then be easily inspected to see whether or not the handlers defined in `subgraph.yaml` have been called. Since code coverage (and testing as whole) is in very early stages in AssemblyScript and WebAssembly, **Matchstick** cannot check for branch coverage. Instead we rely on the assertion that if a given handler has been called, the event/function for it have been properly mocked.

### Prerequisites

To run the test coverage functionality provided in **Matchstick**, there are a few things you need to prepare beforehand:

#### Export your handlers

In order for **Matchstick** to check which handlers are being run, those handlers need to be exported from the **test file**. So for instance in our example, in our gravity.test.ts file we have the following handler being imported:

```typescript
import { handleNewGravatar } from '../../src/gravity'
```

In order for that function to be visible (for it to be included in the `wat` file **by name**) we need to also export it, like this:

```typescript
export { handleNewGravatar }
```

### Usage

Once that's all set up, to run the test coverage tool, simply run:

```sh
graph test -- -c
```

You could also add a custom `coverage` command to your `package.json` file, like so:

```typescript
 "scripts": {
    /.../
    "coverage": "graph test -- -c"
  },
```

That will execute the coverage tool and you should see something like this in the terminal:

```sh
$ graph test -c
Skipping download/install step because binary already exists at /Users/petko/work/demo-subgraph/node_modules/binary-install-raw/bin/0.4.0

___  ___      _       _         _   _      _
|  \/  |     | |     | |       | | (_)    | |
| .  . | __ _| |_ ___| |__  ___| |_ _  ___| | __
| |\/| |/ _` | __/ __| '_ \/ __| __| |/ __| |/ /
| |  | | (_| | || (__| | | \__ \ |_| | (__|   <
\_|  |_/\__,_|\__\___|_| |_|___/\__|_|\___|_|\_\

Compiling...

Running in coverage report mode.
 ️
Reading generated test modules... 🔎️

Generating coverage report 📝

Handlers for source 'Gravity':
Handler 'handleNewGravatar' is tested.
Handler 'handleUpdatedGravatar' is not tested.
Handler 'handleCreateGravatar' is tested.
Test coverage: 66.7% (2/3 handlers).

Handlers for source 'GraphTokenLockWallet':
Handler 'handleTokensReleased' is not tested.
Handler 'handleTokensWithdrawn' is not tested.
Handler 'handleTokensRevoked' is not tested.
Handler 'handleManagerUpdated' is not tested.
Handler 'handleApproveTokenDestinations' is not tested.
Handler 'handleRevokeTokenDestinations' is not tested.
Test coverage: 0.0% (0/6 handlers).

Global test coverage: 22.2% (2/9 handlers).
```

### Test run time duration in the log output

The log output includes the test run duration. Here's an example:

`[Thu, 31 Mar 2022 13:54:54 +0300] Program executed in: 42.270ms.`

## Common compiler errors

> Critical: Could not create WasmInstance from valid module with context: unknown import: wasi_snapshot_preview1::fd_write has not been defined

This means you have used `console.log` in your code, which is not supported by AssemblyScript. Please consider using the [Logging API](/developing/graph-ts/api/#logging-api)

> ERROR TS2554: Expected ? arguments, but got ?.
>
> return new ethereum.Block(defaultAddressBytes, defaultAddressBytes, defaultAddressBytes, defaultAddress, defaultAddressBytes, defaultAddressBytes, defaultAddressBytes, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt, defaultBigInt);
>
> in ~lib/matchstick-as/assembly/defaults.ts(18,12)
>
> ERROR TS2554: Expected ? arguments, but got ?.
>
> return new ethereum.Transaction(defaultAddressBytes, defaultBigInt, defaultAddress, defaultAddress, defaultBigInt, defaultBigInt, defaultBigInt, defaultAddressBytes, defaultBigInt);
>
> in ~lib/matchstick-as/assembly/defaults.ts(24,12)

The mismatch in arguments is caused by mismatch in `graph-ts` and `matchstick-as`. The best way to fix issues like this one is to update everything to the latest released version.

## Feedback

If you have any questions, feedback, feature requests or just want to reach out, the best place would be The Graph Discord where we have a dedicated channel for Matchstick, called 🔥| unit-testing.
---
title: Creating a Subgraph
---

This detailed guide provides instructions to successfully create a subgraph.

A subgraph extracts data from a blockchain, processes it, and stores it for efficient querying via GraphQL.

![Defining a Subgraph](/img/defining-a-subgraph.png)

> In order to use your subgraph on The Graph's decentralized network, you will need to [create an API key](/deploying/subgraph-studio-faqs/#2-how-do-i-create-an-api-key) in [Subgraph Studio](https://thegraph.com/studio/apikeys/). It is recommended that you add signal to your subgraph with at least 3,000 GRT to attract 2-3 Indexers.

## Getting Started

### Install the Graph CLI

To build and deploy a subgraph, you will need the [Graph CLI](https://github.com/graphprotocol/graph-tooling/tree/main/packages/cli).

The Graph CLI is written in TypeScript, and you must have `node` and either `npm` or `yarn` installed to use it. Check for the [most recent](https://github.com/graphprotocol/graph-tooling/releases?q=%40graphprotocol%2Fgraph-cli&expanded=true) CLI version.

On your local machine, run one of the following commands:

#### Using [npm](https://www.npmjs.com/)

```bash
npm install -g @graphprotocol/graph-cli@latest
```

#### Using [yarn](https://yarnpkg.com/)

```bash
yarn global add @graphprotocol/graph-cli
```

- The `graph init` command can be used to set up a new subgraph project, either from an existing contract or from an example subgraph.

- This `graph init` command can also create a subgraph in Subgraph Studio by passing in `--product subgraph-studio`.

- If you already have a smart contract deployed to your preferred network, you can bootstrap a new subgraph from that contract to get started.

## Create a subgraph

### From an existing contract

The following command creates a subgraph that indexes all events of an existing contract:

```sh
graph init \
  --product subgraph-studio
  --from-contract <CONTRACT_ADDRESS> \
  [--network <ETHEREUM_NETWORK>] \
  [--abi <FILE>] \
  <SUBGRAPH_SLUG> [<DIRECTORY>]
```

- The command tries to retrieve the contract ABI from Etherscan.

  - The Graph CLI relies on a public RPC endpoint. While occasional failures are expected, retries typically resolve this issue. If failures persist, consider using a local ABI.

- If any of the optional arguments are missing, it guides you through an interactive form.

- The `<SUBGRAPH_SLUG>` is the ID of your subgraph in [Subgraph Studio](https://thegraph.com/studio/). It can be found on your subgraph details page.

### From an example subgraph

The following command initializes a new project from an example subgraph:

```sh
graph init --studio <SUBGRAPH_SLUG> --from-example=example-subgraph
```

- The [example subgraph](https://github.com/graphprotocol/example-subgraph) is based on the Gravity contract by Dani Grant, which manages user avatars and emits `NewGravatar` or `UpdateGravatar` events whenever avatars are created or updated.

- The subgraph handles these events by writing `Gravatar` entities to the Graph Node store and ensuring these are updated according to the events.

## Add new `dataSources` to an existing subgraph

Since `v0.31.0`, the Graph CLI supports adding new `dataSources` to an existing subgraph through the `graph add` command:

```sh
graph add <address> [<subgraph-manifest default: "./subgraph.yaml">]

Options:

      --abi <path>              Path to the contract ABI (default: download from Etherscan)
      --contract-name           Name of the contract (default: Contract)
      --merge-entities          Whether to merge entities with the same name (default: false)
      --network-file <path>     Networks config file path (default: "./networks.json")
```

### Specifics

The `graph add` command will fetch the ABI from Etherscan (unless an ABI path is specified with the `--abi` option) and creates a new `dataSource`, similar to how the `graph init` command creates a `dataSource` `--from-contract`, updating the schema and mappings accordingly. This allows you to index implementation contracts from their proxy contracts.

- The `--merge-entities` option identifies how the developer would like to handle `entity` and `event` name conflicts:

  - If `true`: the new `dataSource` should use existing `eventHandlers` & `entities`.

  - If `false`: a new `entity` & `event` handler should be created with `${dataSourceName}{EventName}`.

- The contract `address` will be written to the `networks.json` for the relevant network.

> Note: When using the interactive CLI, after successfully running `graph init`, you'll be prompted to add a new `dataSource`.

## Components of a subgraph

### The Subgraph Manifest

The subgraph manifest, `subgraph.yaml`, defines the smart contracts & network your subgraph will index, the events from these contracts to pay attention to, and how to map event data to entities that Graph Node stores and allows to query.

The **subgraph definition** consists of the following files:

- `subgraph.yaml`: Contains the subgraph manifest

- `schema.graphql`: A GraphQL schema defining the data stored for your subgraph and how to query it via GraphQL

- `mapping.ts`: [AssemblyScript Mappings](https://github.com/AssemblyScript/assemblyscript) code that translates event data into entities defined in your schema (e.g. `mapping.ts` in this guide)

A single subgraph can:

- Index data from multiple smart contracts (but not multiple networks).

- Index data from IPFS files using File Data Sources.

- Add an entry for each contract that requires indexing to the `dataSources` array.

The full specification for subgraph manifests can be found [here](https://github.com/graphprotocol/graph-node/blob/master/docs/subgraph-manifest.md).

For the example subgraph listed above, `subgraph.yaml` is:

```yaml
specVersion: 0.0.4
description: Gravatar for Ethereum
repository: https://github.com/graphprotocol/graph-tooling
schema:
  file: ./schema.graphql
indexerHints:
  prune: auto
dataSources:
  - kind: ethereum/contract
    name: Gravity
    network: mainnet
    source:
      address: '0x2E645469f354BB4F5c8a05B3b30A929361cf77eC'
      abi: Gravity
      startBlock: 6175244
      endBlock: 7175245
    context:
      foo:
        type: Bool
        data: true
      bar:
        type: String
        data: 'bar'
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      entities:
        - Gravatar
      abis:
        - name: Gravity
          file: ./abis/Gravity.json
      eventHandlers:
        - event: NewGravatar(uint256,address,string,string)
          handler: handleNewGravatar
        - event: UpdatedGravatar(uint256,address,string,string)
          handler: handleUpdatedGravatar
      callHandlers:
        - function: createGravatar(string,string)
          handler: handleCreateGravatar
      blockHandlers:
        - handler: handleBlock
        - handler: handleBlockWithCall
          filter:
            kind: call
      file: ./src/mapping.ts
```

The important entries to update for the manifest are:

- `specVersion`: a semver version that identifies the supported manifest structure and functionality for the subgraph. The latest version is `1.2.0`. See [specVersion releases](#specversion-releases) section to see more details on features & releases.

- `description`: a human-readable description of what the subgraph is. This description is displayed in Graph Explorer when the subgraph is deployed to Subgraph Studio.

- `repository`: the URL of the repository where the subgraph manifest can be found. This is also displayed in Graph Explorer.

- `features`: a list of all used [feature](#experimental-features) names.

- `indexerHints.prune`: Defines the retention of historical block data for a subgraph. See [prune](#prune) in [indexerHints](#indexer-hints) section.

- `dataSources.source`: the address of the smart contract the subgraph sources, and the ABI of the smart contract to use. The address is optional; omitting it allows to index matching events from all contracts.

- `dataSources.source.startBlock`: the optional number of the block that the data source starts indexing from. In most cases, we suggest using the block in which the contract was created.

- `dataSources.source.endBlock`: The optional number of the block that the data source stops indexing at, including that block. Minimum spec version required: `0.0.9`.

- `dataSources.context`: key-value pairs that can be used within subgraph mappings. Supports various data types like `Bool`, `String`, `Int`, `Int8`, `BigDecimal`, `Bytes`, `List`, and `BigInt`. Each variable needs to specify its `type` and `data`. These context variables are then accessible in the mapping files, offering more configurable options for subgraph development.

- `dataSources.mapping.entities`: the entities that the data source writes to the store. The schema for each entity is defined in the schema.graphql file.

- `dataSources.mapping.abis`: one or more named ABI files for the source contract as well as any other smart contracts that you interact with from within the mappings.

- `dataSources.mapping.eventHandlers`: lists the smart contract events this subgraph reacts to and the handlers in the mapping—./src/mapping.ts in the example—that transform these events into entities in the store.

- `dataSources.mapping.callHandlers`: lists the smart contract functions this subgraph reacts to and handlers in the mapping that transform the inputs and outputs to function calls into entities in the store.

- `dataSources.mapping.blockHandlers`: lists the blocks this subgraph reacts to and handlers in the mapping to run when a block is appended to the chain. Without a filter, the block handler will be run every block. An optional call-filter can be provided by adding a `filter` field with `kind: call` to the handler. This will only run the handler if the block contains at least one call to the data source contract.

A single subgraph can index data from multiple smart contracts. Add an entry for each contract from which data needs to be indexed to the `dataSources` array.

### Order of Triggering Handlers

The triggers for a data source within a block are ordered using the following process:

1.  Event and call triggers are first ordered by transaction index within the block.
2.  Event and call triggers within the same transaction are ordered using a convention: event triggers first then call triggers, each type respecting the order they are defined in the manifest.
3.  Block triggers are run after event and call triggers, in the order they are defined in the manifest.

These ordering rules are subject to change.

> **Note:** When new [dynamic data source](#data-source-templates-for-dynamically-created-contracts) are created, the handlers defined for dynamic data sources will only start processing after all existing data source handlers are processed, and will repeat in the same sequence whenever triggered.

### Indexed Argument Filters / Topic Filters

> **Requires**: [SpecVersion](#specversion-releases) >= `1.2.0`

Topic filters, also known as indexed argument filters, are a powerful feature in subgraphs that allow users to precisely filter blockchain events based on the values of their indexed arguments.

- These filters help isolate specific events of interest from the vast stream of events on the blockchain, allowing subgraphs to operate more efficiently by focusing only on relevant data.

- This is useful for creating personal subgraphs that track specific addresses and their interactions with various smart contracts on the blockchain.

#### How Topic Filters Work

When a smart contract emits an event, any arguments that are marked as indexed can be used as filters in a subgraph's manifest. This allows the subgraph to listen selectively for events that match these indexed arguments.

- The event's first indexed argument corresponds to `topic1`, the second to `topic2`, and so on, up to `topic3`, since the Ethereum Virtual Machine (EVM) allows up to three indexed arguments per event.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Token {
    // Event declaration with indexed parameters for addresses
    event Transfer(address indexed from, address indexed to, uint256 value);

    // Function to simulate transferring tokens
    function transfer(address to, uint256 value) public {
        // Emitting the Transfer event with from, to, and value
        emit Transfer(msg.sender, to, value);
    }
}
```

In this example:

- The `Transfer` event is used to log transactions of tokens between addresses.
- The `from` and `to` parameters are indexed, allowing event listeners to filter and monitor transfers involving specific addresses.
- The `transfer` function is a simple representation of a token transfer action, emitting the Transfer event whenever it is called.

#### Configuration in Subgraphs

Topic filters are defined directly within the event handler configuration in the subgraph manifest. Here is how they are configured:

```yaml
eventHandlers:
  - event: SomeEvent(indexed uint256, indexed address, indexed uint256)
    handler: handleSomeEvent
    topic1: ['0xValue1', '0xValue2']
    topic2: ['0xAddress1', '0xAddress2']
    topic3: ['0xValue3']
```

In this setup:

- `topic1` corresponds to the first indexed argument of the event, `topic2` to the second, and `topic3` to the third.
- Each topic can have one or more values, and an event is only processed if it matches one of the values in each specified topic.

##### Filter Logic

- Within a Single Topic: The logic functions as an OR condition. The event will be processed if it matches any one of the listed values in a given topic.
- Between Different Topics: The logic functions as an AND condition. An event must satisfy all specified conditions across different topics to trigger the associated handler.

#### Example 1: Tracking Direct Transfers from Address A to Address B

```yaml
eventHandlers:
  - event: Transfer(indexed address,indexed address,uint256)
    handler: handleDirectedTransfer
    topic1: ['0xAddressA'] # Sender Address
    topic2: ['0xAddressB'] # Receiver Address
```

In this configuration:

- `topic1` is configured to filter `Transfer` events where `0xAddressA` is the sender.
- `topic2` is configured to filter `Transfer` events where `0xAddressB` is the receiver.
- The subgraph will only index transactions that occur directly from `0xAddressA` to `0xAddressB`.

#### Example 2: Tracking Transactions in Either Direction Between Two or More Addresses

```yaml
eventHandlers:
  - event: Transfer(indexed address,indexed address,uint256)
    handler: handleTransferToOrFrom
    topic1: ['0xAddressA', '0xAddressB', '0xAddressC'] # Sender Address
    topic2: ['0xAddressB', '0xAddressC'] # Receiver Address
```

In this configuration:

- `topic1` is configured to filter `Transfer` events where `0xAddressA`, `0xAddressB`, `0xAddressC` is the sender.
- `topic2` is configured to filter `Transfer` events where `0xAddressB` and `0xAddressC` is the receiver.
- The subgraph will index transactions that occur in either direction between multiple addresses allowing for comprehensive monitoring of interactions involving all addresses.

## Declared eth_call

> **Requires**: [SpecVersion](#specversion-releases) >= `1.2.0`. Currently, `eth_calls` can only be declared for event handlers.

Declarative `eth_calls` are a valuable subgraph feature that allows `eth_calls` to be executed ahead of time, enabling `graph-node` to execute them in parallel.

This feature does the following:

- Significantly improves the performance of fetching data from the Ethereum blockchain by reducing the total time for multiple calls and optimizing the subgraph's overall efficiency.
- Allows faster data fetching, resulting in quicker query responses and a better user experience.
- Reduces wait times for applications that need to aggregate data from multiple Ethereum calls, making the data retrieval process more efficient.

### Key Concepts

- Declarative `eth_calls`: Ethereum calls that are defined to be executed in parallel rather than sequentially.
- Parallel Execution: Instead of waiting for one call to finish before starting the next, multiple calls can be initiated simultaneously.
- Time Efficiency: The total time taken for all the calls changes from the sum of the individual call times (sequential) to the time taken by the longest call (parallel).

### Scenario without Declarative `eth_calls`

Imagine you have a subgraph that needs to make three Ethereum calls to fetch data about a user's transactions, balance, and token holdings.

Traditionally, these calls might be made sequentially:

1.  Call 1 (Transactions): Takes 3 seconds
2.  Call 2 (Balance): Takes 2 seconds
3.  Call 3 (Token Holdings): Takes 4 seconds

Total time taken = 3 + 2 + 4 = 9 seconds

### Scenario with Declarative `eth_calls`

With this feature, you can declare these calls to be executed in parallel:

1.  Call 1 (Transactions): Takes 3 seconds
2.  Call 2 (Balance): Takes 2 seconds
3.  Call 3 (Token Holdings): Takes 4 seconds

Since these calls are executed in parallel, the total time taken is equal to the time taken by the longest call.

Total time taken = max (3, 2, 4) = 4 seconds

### How it Works

1.  Declarative Definition: In the subgraph manifest, you declare the Ethereum calls in a way that indicates they can be executed in parallel.
2.  Parallel Execution Engine: The Graph Node's execution engine recognizes these declarations and runs the calls simultaneously.
3.  Result Aggregation: Once all calls are complete, the results are aggregated and used by the subgraph for further processing.

### Example Configuration in Subgraph Manifest

Declared `eth_calls` can access the `event.address` of the underlying event as well as all the `event.params`.

`Subgraph.yaml` using `event.address`:

```yaml
eventHandlers:
event: Swap(indexed address,indexed address,int256,int256,uint160,uint128,int24)
handler: handleSwap
calls:
  global0X128: Pool[event.address].feeGrowthGlobal0X128()
  global1X128: Pool[event.address].feeGrowthGlobal1X128()
```

Details for the example above:

- `global0X128` is the declared `eth_call`.
- The text (`global0X128`) is the label for this `eth_call` which is used when logging errors.
- The text (`Pool[event.address].feeGrowthGlobal0X128()`) is the actual `eth_call` that will be executed, which is in the form of `Contract[address].function(arguments)`
- The `address` and `arguments` can be replaced with variables that will be available when the handler is executed.

`Subgraph.yaml` using `event.params`

```yaml
calls:
  - ERC20DecimalsToken0: ERC20[event.params.token0].decimals()
```

### SpecVersion Releases

| Version | Release notes |
| :-: | --- |
| 1.2.0 | Added support for [Indexed Argument Filtering](/#indexed-argument-filters--topic-filters) & declared `eth_call` |
| 1.1.0 | Supports [Timeseries & Aggregations](#timeseries-and-aggregations). Added support for type `Int8` for `id`. |
| 1.0.0 | Supports [`indexerHints`](/developing/creating-a-subgraph/#indexer-hints) feature to prune subgraphs |
| 0.0.9 | Supports `endBlock` feature |
| 0.0.8 | Added support for polling [Block Handlers](developing/creating-a-subgraph/#polling-filter) and [Initialisation Handlers](developing/creating-a-subgraph/#once-filter). |
| 0.0.7 | Added support for [File Data Sources](developing/creating-a-subgraph/#file-data-sources). |
| 0.0.6 | Supports fast [Proof of Indexing](/network/indexing/#what-is-a-proof-of-indexing-poi) calculation variant. |
| 0.0.5 | Added support for event handlers having access to transaction receipts. |
| 0.0.4 | Added support for managing subgraph features. |

### Getting The ABIs

The ABI file(s) must match your contract(s). There are a few ways to obtain ABI files:

- If you are building your own project, you will likely have access to your most current ABIs.
- If you are building a subgraph for a public project, you can download that project to your computer and get the ABI by using [`truffle compile`](https://truffleframework.com/docs/truffle/overview) or using solc to compile.
- You can also find the ABI on [Etherscan](https://etherscan.io/), but this isn't always reliable, as the ABI that is uploaded there may be out of date. Make sure you have the right ABI, otherwise running your subgraph will fail.

## The GraphQL Schema

The schema for your subgraph is in the file `schema.graphql`. GraphQL schemas are defined using the GraphQL interface definition language. If you've never written a GraphQL schema, it is recommended that you check out this primer on the GraphQL type system. Reference documentation for GraphQL schemas can be found in the [GraphQL API](/querying/graphql-api) section.

## Defining Entities

Before defining entities, it is important to take a step back and think about how your data is structured and linked. All queries will be made against the data model defined in the subgraph schema and the entities indexed by the subgraph. Because of this, it is good to define the subgraph schema in a way that matches the needs of your dapp. It may be useful to imagine entities as "objects containing data", rather than as events or functions.

With The Graph, you simply define entity types in `schema.graphql`, and Graph Node will generate top level fields for querying single instances and collections of that entity type. Each type that should be an entity is required to be annotated with an `@entity` directive. By default, entities are mutable, meaning that mappings can load existing entities, modify them and store a new version of that entity. Mutability comes at a price, and for entity types for which it is known that they will never be modified, for example, because they simply contain data extracted verbatim from the chain, it is recommended to mark them as immutable with `@entity(immutable: true)`. Mappings can make changes to immutable entities as long as those changes happen in the same block in which the entity was created. Immutable entities are much faster to write and to query, and should therefore be used whenever possible.

### Good Example

The `Gravatar` entity below is structured around a Gravatar object and is a good example of how an entity could be defined.

```graphql
type Gravatar @entity(immutable: true) {
  id: Bytes!
  owner: Bytes
  displayName: String
  imageUrl: String
  accepted: Boolean
}
```

### Bad Example

The example `GravatarAccepted` and `GravatarDeclined` entities below are based around events. It is not recommended to map events or function calls to entities 1:1.

```graphql
type GravatarAccepted @entity {
  id: Bytes!
  owner: Bytes
  displayName: String
  imageUrl: String
}

type GravatarDeclined @entity {
  id: Bytes!
  owner: Bytes
  displayName: String
  imageUrl: String
}
```

### Optional and Required Fields

Entity fields can be defined as required or optional. Required fields are indicated by the `!` in the schema. If a required field is not set in the mapping, you will receive this error when querying the field:

```
Null value resolved for non-null field 'name'
```

Each entity must have an `id` field, which must be of type `Bytes!` or `String!`. It is generally recommended to use `Bytes!`, unless the `id` contains human-readable text, since entities with `Bytes!` id's will be faster to write and query as those with a `String!` `id`. The `id` field serves as the primary key, and needs to be unique among all entities of the same type. For historical reasons, the type `ID!` is also accepted and is a synonym for `String!`.

For some entity types the `id` is constructed from the id's of two other entities; that is possible using `concat`, e.g., `let id = left.id.concat(right.id) ` to form the id from the id's of `left` and `right`. Similarly, to construct an id from the id of an existing entity and a counter `count`, `let id = left.id.concatI32(count)` can be used. The concatenation is guaranteed to produce unique id's as long as the length of `left` is the same for all such entities, for example, because `left.id` is an `Address`.

### Built-In Scalar Types

#### GraphQL Supported Scalars

We support the following scalars in our GraphQL API:

| Type | Description |
| --- | --- |
| `Bytes` | Byte array, represented as a hexadecimal string. Commonly used for Ethereum hashes and addresses. |
| `String` | Scalar for `string` values. Null characters are not supported and are automatically removed. |
| `Boolean` | Scalar for `boolean` values. |
| `Int` | The GraphQL spec defines `Int` to be a signed 32-bit integer. |
| `Int8` | An 8-byte signed integer, also known as a 64-bit signed integer, can store values in the range from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807. Prefer using this to represent `i64` from ethereum. |
| `BigInt` | Large integers. Used for Ethereum's `uint32`, `int64`, `uint64`, ..., `uint256` types. Note: Everything below `uint32`, such as `int32`, `uint24` or `int8` is represented as `i32`. |
| `BigDecimal` | `BigDecimal` High precision decimals represented as a significand and an exponent. The exponent range is from −6143 to +6144. Rounded to 34 significant digits. |
| `Timestamp` | It is an `i64` value in microseconds. Commonly used for `timestamp` fields for timeseries and aggregations. |

#### Enums

You can also create enums within a schema. Enums have the following syntax:

```graphql
enum TokenStatus {
  OriginalOwner
  SecondOwner
  ThirdOwner
}
```

Once the enum is defined in the schema, you can use the string representation of the enum value to set an enum field on an entity. For example, you can set the `tokenStatus` to `SecondOwner` by first defining your entity and subsequently setting the field with `entity.tokenStatus = "SecondOwner"`. The example below demonstrates what the Token entity would look like with an enum field:

More detail on writing enums can be found in the [GraphQL documentation](https://graphql.org/learn/schema/).

#### Entity Relationships

An entity may have a relationship to one or more other entities in your schema. These relationships may be traversed in your queries. Relationships in The Graph are unidirectional. It is possible to simulate bidirectional relationships by defining a unidirectional relationship on either "end" of the relationship.

Relationships are defined on entities just like any other field except that the type specified is that of another entity.

#### One-To-One Relationships

Define a `Transaction` entity type with an optional one-to-one relationship with a `TransactionReceipt` entity type:

```graphql
type Transaction @entity(immutable: true) {
  id: Bytes!
  transactionReceipt: TransactionReceipt
}

type TransactionReceipt @entity(immutable: true) {
  id: Bytes!
  transaction: Transaction
}
```

#### One-To-Many Relationships

Define a `TokenBalance` entity type with a required one-to-many relationship with a Token entity type:

```graphql
type Token @entity(immutable: true) {
  id: Bytes!
}

type TokenBalance @entity {
  id: Bytes!
  amount: Int!
  token: Token!
}
```

#### Reverse Lookups

Reverse lookups can be defined on an entity through the `@derivedFrom` field. This creates a virtual field on the entity that may be queried but cannot be set manually through the mappings API. Rather, it is derived from the relationship defined on the other entity. For such relationships, it rarely makes sense to store both sides of the relationship, and both indexing and query performance will be better when only one side is stored and the other is derived.

For one-to-many relationships, the relationship should always be stored on the 'one' side, and the 'many' side should always be derived. Storing the relationship this way, rather than storing an array of entities on the 'many' side, will result in dramatically better performance for both indexing and querying the subgraph. In general, storing arrays of entities should be avoided as much as is practical.

#### Example

We can make the balances for a token accessible from the token by deriving a `tokenBalances` field:

```graphql
type Token @entity(immutable: true) {
  id: Bytes!
  tokenBalances: [TokenBalance!]! @derivedFrom(field: "token")
}

type TokenBalance @entity {
  id: Bytes!
  amount: Int!
  token: Token!
}
```

#### Many-To-Many Relationships

For many-to-many relationships, such as users that each may belong to any number of organizations, the most straightforward, but generally not the most performant, way to model the relationship is as an array in each of the two entities involved. If the relationship is symmetric, only one side of the relationship needs to be stored and the other side can be derived.

#### Example

Define a reverse lookup from a `User` entity type to an `Organization` entity type. In the example below, this is achieved by looking up the `members` attribute from within the `Organization` entity. In queries, the `organizations` field on `User` will be resolved by finding all `Organization` entities that include the user's ID.

```graphql
type Organization @entity {
  id: Bytes!
  name: String!
  members: [User!]!
}

type User @entity {
  id: Bytes!
  name: String!
  organizations: [Organization!]! @derivedFrom(field: "members")
}
```

A more performant way to store this relationship is through a mapping table that has one entry for each `User` / `Organization` pair with a schema like

```graphql
type Organization @entity {
  id: Bytes!
  name: String!
  members: [UserOrganization!]! @derivedFrom(field: "organization")
}

type User @entity {
  id: Bytes!
  name: String!
  organizations: [UserOrganization!] @derivedFrom(field: "user")
}

type UserOrganization @entity {
  id: Bytes! # Set to `user.id.concat(organization.id)`
  user: User!
  organization: Organization!
}
```

This approach requires that queries descend into one additional level to retrieve, for example, the organizations for users:

```graphql
query usersWithOrganizations {
  users {
    organizations {
      # this is a UserOrganization entity
      organization {
        name
      }
    }
  }
}
```

This more elaborate way of storing many-to-many relationships will result in less data stored for the subgraph, and therefore to a subgraph that is often dramatically faster to index and to query.

#### Adding comments to the schema

As per GraphQL spec, comments can be added above schema entity attributes using the hash symbol `#`. This is illustrated in the example below:

```graphql
type MyFirstEntity @entity {
  # unique identifier and primary key of the entity
  id: Bytes!
  address: Bytes!
}
```

## Defining Fulltext Search Fields

Fulltext search queries filter and rank entities based on a text search input. Fulltext queries are able to return matches for similar words by processing the query text input into stems before comparing them to the indexed text data.

A fulltext query definition includes the query name, the language dictionary used to process the text fields, the ranking algorithm used to order the results, and the fields included in the search. Each fulltext query may span multiple fields, but all included fields must be from a single entity type.

To add a fulltext query, include a `_Schema_` type with a fulltext directive in the GraphQL schema.

```graphql
type _Schema_
  @fulltext(
    name: "bandSearch"
    language: en
    algorithm: rank
    include: [{ entity: "Band", fields: [{ name: "name" }, { name: "description" }, { name: "bio" }] }]
  )

type Band @entity {
  id: Bytes!
  name: String!
  description: String!
  bio: String
  wallet: Address
  labels: [Label!]!
  discography: [Album!]!
  members: [Musician!]!
}
```

The example `bandSearch` field can be used in queries to filter `Band` entities based on the text documents in the `name`, `description`, and `bio` fields. Jump to [GraphQL API - Queries](/querying/graphql-api#queries) for a description of the fulltext search API and more example usage.

```graphql
query {
  bandSearch(text: "breaks & electro & detroit") {
    id
    name
    description
    wallet
  }
}
```

> **[Feature Management](#experimental-features):** From `specVersion` `0.0.4` and onwards, `fullTextSearch` must be declared under the `features` section in the subgraph manifest.

### Languages supported

Choosing a different language will have a definitive, though sometimes subtle, effect on the fulltext search API. Fields covered by a fulltext query field are examined in the context of the chosen language, so the lexemes produced by analysis and search queries vary from language to language. For example: when using the supported Turkish dictionary "token" is stemmed to "toke" while, of course, the English dictionary will stem it to "token".

Supported language dictionaries:

| Code   | Dictionary |
| ------ | ---------- |
| simple | General    |
| da     | Danish     |
| nl     | Dutch      |
| en     | English    |
| fi     | Finnish    |
| fr     | French     |
| de     | German     |
| hu     | Hungarian  |
| it     | Italian    |
| no     | Norwegian  |
| pt     | Portuguese |
| ro     | Romanian   |
| ru     | Russian    |
| es     | Spanish    |
| sv     | Swedish    |
| tr     | Turkish    |

### Ranking Algorithms

Supported algorithms for ordering results:

| Algorithm     | Description                                                             |
| ------------- | ----------------------------------------------------------------------- |
| rank          | Use the match quality (0-1) of the fulltext query to order the results. |
| proximityRank | Similar to rank but also includes the proximity of the matches.         |

## Writing Mappings

The mappings take data from a particular source and transform it into entities that are defined within your schema. Mappings are written in a subset of [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html) called [AssemblyScript](https://github.com/AssemblyScript/assemblyscript/wiki) which can be compiled to WASM ([WebAssembly](https://webassembly.org/)). AssemblyScript is stricter than normal TypeScript, yet provides a familiar syntax.

For each event handler that is defined in `subgraph.yaml` under `mapping.eventHandlers`, create an exported function of the same name. Each handler must accept a single parameter called `event` with a type corresponding to the name of the event which is being handled.

In the example subgraph, `src/mapping.ts` contains handlers for the `NewGravatar` and `UpdatedGravatar` events:

```javascript
import { NewGravatar, UpdatedGravatar } from '../generated/Gravity/Gravity'
import { Gravatar } from '../generated/schema'

export function handleNewGravatar(event: NewGravatar): void {
  let gravatar = new Gravatar(event.params.id)
  gravatar.owner = event.params.owner
  gravatar.displayName = event.params.displayName
  gravatar.imageUrl = event.params.imageUrl
  gravatar.save()
}

export function handleUpdatedGravatar(event: UpdatedGravatar): void {
  let id = event.params.id
  let gravatar = Gravatar.load(id)
  if (gravatar == null) {
    gravatar = new Gravatar(id)
  }
  gravatar.owner = event.params.owner
  gravatar.displayName = event.params.displayName
  gravatar.imageUrl = event.params.imageUrl
  gravatar.save()
}
```

The first handler takes a `NewGravatar` event and creates a new `Gravatar` entity with `new Gravatar(event.params.id.toHex())`, populating the entity fields using the corresponding event parameters. This entity instance is represented by the variable `gravatar`, with an id value of `event.params.id.toHex()`.

The second handler tries to load the existing `Gravatar` from the Graph Node store. If it does not exist yet, it is created on-demand. The entity is then updated to match the new event parameters before it is saved back to the store using `gravatar.save()`.

### Recommended IDs for Creating New Entities

It is highly recommended to use `Bytes` as the type for `id` fields, and only use `String` for attributes that truly contain human-readable text, like the name of a token. Below are some recommended `id` values to consider when creating new entities.

- `transfer.id = event.transaction.hash`

- `let id = event.transaction.hash.concatI32(event.logIndex.toI32())`

- For entities that store aggregated data, for e.g, daily trade volumes, the `id` usually contains the day number. Here, using a `Bytes` as the `id` is beneficial. Determining the `id` would look like

```typescript
let dayID = event.block.timestamp.toI32() / 86400
let id = Bytes.fromI32(dayID)
```

- Convert constant addresses to `Bytes`.

`const id = Bytes.fromHexString('0xdead...beef')`

There is a [Graph Typescript Library](https://github.com/graphprotocol/graph-tooling/tree/main/packages/ts) which contains utilities for interacting with the Graph Node store and conveniences for handling smart contract data and entities. It can be imported into `mapping.ts` from `@graphprotocol/graph-ts`.

### Handling of entities with identical IDs

When creating and saving a new entity, if an entity with the same ID already exists, the properties of the new entity are always preferred during the merge process. This means that the existing entity will be updated with the values from the new entity.

If a null value is intentionally set for a field in the new entity with the same ID, the existing entity will be updated with the null value.

If no value is set for a field in the new entity with the same ID, the field will result in null as well.

## Code Generation

In order to make it easy and type-safe to work with smart contracts, events and entities, the Graph CLI can generate AssemblyScript types from the subgraph's GraphQL schema and the contract ABIs included in the data sources.

This is done with

```sh
graph codegen [--output-dir <OUTPUT_DIR>] [<MANIFEST>]
```

but in most cases, subgraphs are already preconfigured via `package.json` to allow you to simply run one of the following to achieve the same:

```sh
# Yarn
yarn codegen

# NPM
npm run codegen
```

This will generate an AssemblyScript class for every smart contract in the ABI files mentioned in `subgraph.yaml`, allowing you to bind these contracts to specific addresses in the mappings and call read-only contract methods against the block being processed. It will also generate a class for every contract event to provide easy access to event parameters, as well as the block and transaction the event originated from. All of these types are written to `<OUTPUT_DIR>/<DATA_SOURCE_NAME>/<ABI_NAME>.ts`. In the example subgraph, this would be `generated/Gravity/Gravity.ts`, allowing mappings to import these types with.

```javascript
import {
  // The contract class:
  Gravity,
  // The events classes:
  NewGravatar,
  UpdatedGravatar,
} from '../generated/Gravity/Gravity'
```

In addition to this, one class is generated for each entity type in the subgraph's GraphQL schema. These classes provide type-safe entity loading, read and write access to entity fields as well as a `save()` method to write entities to store. All entity classes are written to `<OUTPUT_DIR>/schema.ts`, allowing mappings to import them with

```javascript
import { Gravatar } from '../generated/schema'
```

> **Note:** The code generation must be performed again after every change to the GraphQL schema or the ABIs included in the manifest. It must also be performed at least once before building or deploying the subgraph.

Code generation does not check your mapping code in `src/mapping.ts`. If you want to check that before trying to deploy your subgraph to Graph Explorer, you can run `yarn build` and fix any syntax errors that the TypeScript compiler might find.

## Data Source Templates

A common pattern in EVM-compatible smart contracts is the use of registry or factory contracts, where one contract creates, manages, or references an arbitrary number of other contracts that each have their own state and events.

The addresses of these sub-contracts may or may not be known upfront and many of these contracts may be created and/or added over time. This is why, in such cases, defining a single data source or a fixed number of data sources is impossible and a more dynamic approach is needed: _data source templates_.

### Data Source for the Main Contract

First, you define a regular data source for the main contract. The snippet below shows a simplified example data source for the [Uniswap](https://uniswap.org) exchange factory contract. Note the `NewExchange(address,address)` event handler. This is emitted when a new exchange contract is created on-chain by the factory contract.

```yaml
dataSources:
  - kind: ethereum/contract
    name: Factory
    network: mainnet
    source:
      address: '0xc0a47dFe034B400B47bDaD5FecDa2621de6c4d95'
      abi: Factory
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      file: ./src/mappings/factory.ts
      entities:
        - Directory
      abis:
        - name: Factory
          file: ./abis/factory.json
      eventHandlers:
        - event: NewExchange(address,address)
          handler: handleNewExchange
```

### Data Source Templates for Dynamically Created Contracts

Then, you add _data source templates_ to the manifest. These are identical to regular data sources, except that they lack a pre-defined contract address under `source`. Typically, you would define one template for each type of sub-contract managed or referenced by the parent contract.

```yaml
dataSources:
  - kind: ethereum/contract
    name: Factory
    # ... other source fields for the main contract ...
templates:
  - name: Exchange
    kind: ethereum/contract
    network: mainnet
    source:
      abi: Exchange
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      file: ./src/mappings/exchange.ts
      entities:
        - Exchange
      abis:
        - name: Exchange
          file: ./abis/exchange.json
      eventHandlers:
        - event: TokenPurchase(address,uint256,uint256)
          handler: handleTokenPurchase
        - event: EthPurchase(address,uint256,uint256)
          handler: handleEthPurchase
        - event: AddLiquidity(address,uint256,uint256)
          handler: handleAddLiquidity
        - event: RemoveLiquidity(address,uint256,uint256)
          handler: handleRemoveLiquidity
```

### Instantiating a Data Source Template

In the final step, you update your main contract mapping to create a dynamic data source instance from one of the templates. In this example, you would change the main contract mapping to import the `Exchange` template and call the `Exchange.create(address)` method on it to start indexing the new exchange contract.

```typescript
import { Exchange } from '../generated/templates'

export function handleNewExchange(event: NewExchange): void {
  // Start indexing the exchange; `event.params.exchange` is the
  // address of the new exchange contract
  Exchange.create(event.params.exchange)
}
```

> **Note:** A new data source will only process the calls and events for the block in which it was created and all following blocks, but will not process historical data, i.e., data that is contained in prior blocks.
>
> If prior blocks contain data relevant to the new data source, it is best to index that data by reading the current state of the contract and creating entities representing that state at the time the new data source is created.

### Data Source Context

Data source contexts allow passing extra configuration when instantiating a template. In our example, let's say exchanges are associated with a particular trading pair, which is included in the `NewExchange` event. That information can be passed into the instantiated data source, like so:

```typescript
import { Exchange } from '../generated/templates'

export function handleNewExchange(event: NewExchange): void {
  let context = new DataSourceContext()
  context.setString('tradingPair', event.params.tradingPair)
  Exchange.createWithContext(event.params.exchange, context)
}
```

Inside a mapping of the `Exchange` template, the context can then be accessed:

```typescript
import { dataSource } from '@graphprotocol/graph-ts'

let context = dataSource.context()
let tradingPair = context.getString('tradingPair')
```

There are setters and getters like `setString` and `getString` for all value types.

## Start Blocks

The `startBlock` is an optional setting that allows you to define from which block in the chain the data source will start indexing. Setting the start block allows the data source to skip potentially millions of blocks that are irrelevant. Typically, a subgraph developer will set `startBlock` to the block in which the smart contract of the data source was created.

```yaml
dataSources:
  - kind: ethereum/contract
    name: ExampleSource
    network: mainnet
    source:
      address: '0xc0a47dFe034B400B47bDaD5FecDa2621de6c4d95'
      abi: ExampleContract
      startBlock: 6627917
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      file: ./src/mappings/factory.ts
      entities:
        - User
      abis:
        - name: ExampleContract
          file: ./abis/ExampleContract.json
      eventHandlers:
        - event: NewEvent(address,address)
          handler: handleNewEvent
```

> **Note:** The contract creation block can be quickly looked up on Etherscan:
>
> 1.  Search for the contract by entering its address in the search bar.
> 2.  Click on the creation transaction hash in the `Contract Creator` section.
> 3.  Load the transaction details page where you'll find the start block for that contract.

## Indexer Hints

The `indexerHints` setting in a subgraph's manifest provides directives for indexers on processing and managing a subgraph. It influences operational decisions across data handling, indexing strategies, and optimizations. Presently, it features the `prune` option for managing historical data retention or pruning.

> This feature is available from `specVersion: 1.0.0`

### Prune

`indexerHints.prune`: Defines the retention of historical block data for a subgraph. Options include:

1.  `"never"`: No pruning of historical data; retains the entire history.
2.  `"auto"`: Retains the minimum necessary history as set by the indexer, optimizing query performance.
3.  A specific number: Sets a custom limit on the number of historical blocks to retain.

```
 indexerHints:
  prune: auto
```

> The term "history" in this context of subgraphs is about storing data that reflects the old states of mutable entities.

History as of a given block is required for:

- [Time travel queries](/querying/graphql-api/#time-travel-queries), which enable querying the past states of these entities at specific blocks throughout the subgraph's history
- Using the subgraph as a [graft base](/developing/creating-a-subgraph/#grafting-onto-existing-subgraphs) in another subgraph, at that block
- Rewinding the subgraph back to that block

If historical data as of the block has been pruned, the above capabilities will not be available.

> Using `"auto"` is generally recommended as it maximizes query performance and is sufficient for most users who do not require access to extensive historical data.

For subgraphs leveraging [time travel queries](/querying/graphql-api/#time-travel-queries), it's advisable to either set a specific number of blocks for historical data retention or use `prune: never` to keep all historical entity states. Below are examples of how to configure both options in your subgraph's settings:

To retain a specific amount of historical data:

```
 indexerHints:
  prune: 1000 # Replace 1000 with the desired number of blocks to retain
```

To preserve the complete history of entity states:

```
indexerHints:
  prune: never
```

## Event Handlers

Event handlers in a subgraph react to specific events emitted by smart contracts on the blockchain and trigger handlers defined in the subgraph's manifest. This enables subgraphs to process and store event data according to defined logic.

### Defining an Event Handler

An event handler is declared within a data source in the subgraph's YAML configuration. It specifies which events to listen for and the corresponding function to execute when those events are detected.

```yaml
dataSources:
  - kind: ethereum/contract
    name: Gravity
    network: dev
    source:
      address: '0x731a10897d267e19b34503ad902d0a29173ba4b1'
      abi: Gravity
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      entities:
        - Gravatar
        - Transaction
      abis:
        - name: Gravity
          file: ./abis/Gravity.json
      eventHandlers:
        - event: Approval(address,address,uint256)
          handler: handleApproval
        - event: Transfer(address,address,uint256)
          handler: handleTransfer
          topic1: ['0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045', '0xc8dA6BF26964aF9D7eEd9e03E53415D37aA96325'] # Optional topic filter which filters only events with the specified topic.
```

## Call Handlers

While events provide an effective way to collect relevant changes to the state of a contract, many contracts avoid generating logs to optimize gas costs. In these cases, a subgraph can subscribe to calls made to the data source contract. This is achieved by defining call handlers referencing the function signature and the mapping handler that will process calls to this function. To process these calls, the mapping handler will receive an `ethereum.Call` as an argument with the typed inputs to and outputs from the call. Calls made at any depth in a transaction's call chain will trigger the mapping, allowing activity with the data source contract through proxy contracts to be captured.

Call handlers will only trigger in one of two cases: when the function specified is called by an account other than the contract itself or when it is marked as external in Solidity and called as part of another function in the same contract.

> **Note:** Call handlers currently depend on the Parity tracing API. Certain networks, such as BNB chain and Arbitrum, does not support this API. If a subgraph indexing one of these networks contain one or more call handlers, it will not start syncing. Subgraph developers should instead use event handlers. These are far more performant than call handlers, and are supported on every evm network.

### Defining a Call Handler

To define a call handler in your manifest, simply add a `callHandlers` array under the data source you would like to subscribe to.

```yaml
dataSources:
  - kind: ethereum/contract
    name: Gravity
    network: mainnet
    source:
      address: '0x731a10897d267e19b34503ad902d0a29173ba4b1'
      abi: Gravity
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      entities:
        - Gravatar
        - Transaction
      abis:
        - name: Gravity
          file: ./abis/Gravity.json
      callHandlers:
        - function: createGravatar(string,string)
          handler: handleCreateGravatar
```

The `function` is the normalized function signature to filter calls by. The `handler` property is the name of the function in your mapping you would like to execute when the target function is called in the data source contract.

### Mapping Function

Each call handler takes a single parameter that has a type corresponding to the name of the called function. In the example subgraph above, the mapping contains a handler for when the `createGravatar` function is called and receives a `CreateGravatarCall` parameter as an argument:

```typescript
import { CreateGravatarCall } from '../generated/Gravity/Gravity'
import { Transaction } from '../generated/schema'

export function handleCreateGravatar(call: CreateGravatarCall): void {
  let id = call.transaction.hash
  let transaction = new Transaction(id)
  transaction.displayName = call.inputs._displayName
  transaction.imageUrl = call.inputs._imageUrl
  transaction.save()
}
```

The `handleCreateGravatar` function takes a new `CreateGravatarCall` which is a subclass of `ethereum.Call`, provided by `@graphprotocol/graph-ts`, that includes the typed inputs and outputs of the call. The `CreateGravatarCall` type is generated for you when you run `graph codegen`.

## Block Handlers

In addition to subscribing to contract events or function calls, a subgraph may want to update its data as new blocks are appended to the chain. To achieve this a subgraph can run a function after every block or after blocks that match a pre-defined filter.

### Supported Filters

#### Call Filter

```yaml
filter:
  kind: call
```

_The defined handler will be called once for every block which contains a call to the contract (data source) the handler is defined under._

> **Note:** The `call` filter currently depend on the Parity tracing API. Certain networks, such as BNB chain and Arbitrum, does not support this API. If a subgraph indexing one of these networks contain one or more block handlers with a `call` filter, it will not start syncing.

The absence of a filter for a block handler will ensure that the handler is called every block. A data source can only contain one block handler for each filter type.

```yaml
dataSources:
  - kind: ethereum/contract
    name: Gravity
    network: dev
    source:
      address: '0x731a10897d267e19b34503ad902d0a29173ba4b1'
      abi: Gravity
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      entities:
        - Gravatar
        - Transaction
      abis:
        - name: Gravity
          file: ./abis/Gravity.json
      blockHandlers:
        - handler: handleBlock
        - handler: handleBlockWithCallToContract
          filter:
            kind: call
```

#### Polling Filter

> **Requires `specVersion` >= 0.0.8**

> **Note:** Polling filters are only available on dataSources of `kind: ethereum`.

```yaml
blockHandlers:
  - handler: handleBlock
    filter:
      kind: polling
      every: 10
```

The defined handler will be called once for every `n` blocks, where `n` is the value provided in the `every` field. This configuration allows the subgraph to perform specific operations at regular block intervals.

#### Once Filter

> **Requires `specVersion` >= 0.0.8**

> **Note:** Once filters are only available on dataSources of `kind: ethereum`.

```yaml
blockHandlers:
  - handler: handleOnce
    filter:
      kind: once
```

The defined handler with the once filter will be called only once before all other handlers run. This configuration allows the subgraph to use the handler as an initialization handler, performing specific tasks at the start of indexing.

```ts
export function handleOnce(block: ethereum.Block): void {
  let data = new InitialData(Bytes.fromUTF8('initial'))
  data.data = 'Setup data here'
  data.save()
}
```

### Mapping Function

The mapping function will receive an `ethereum.Block` as its only argument. Like mapping functions for events, this function can access existing subgraph entities in the store, call smart contracts and create or update entities.

```typescript
import { ethereum } from '@graphprotocol/graph-ts'

export function handleBlock(block: ethereum.Block): void {
  let id = block.hash
  let entity = new Block(id)
  entity.save()
}
```

## Anonymous Events

If you need to process anonymous events in Solidity, that can be achieved by providing the topic 0 of the event, as in the example:

```yaml
eventHandlers:
  - event: LogNote(bytes4,address,bytes32,bytes32,uint256,bytes)
    topic0: '0x644843f351d3fba4abcd60109eaff9f54bac8fb8ccf0bab941009c21df21cf31'
    handler: handleGive
```

An event will only be triggered when both the signature and topic 0 match. By default, `topic0` is equal to the hash of the event signature.

## Transaction Receipts in Event Handlers

Starting from `specVersion` `0.0.5` and `apiVersion` `0.0.7`, event handlers can have access to the receipt for the transaction which emitted them.

To do so, event handlers must be declared in the subgraph manifest with the new `receipt: true` key, which is optional and defaults to false.

```yaml
eventHandlers:
  - event: NewGravatar(uint256,address,string,string)
    handler: handleNewGravatar
    receipt: true
```

Inside the handler function, the receipt can be accessed in the `Event.receipt` field. When the `receipt` key is set to `false` or omitted in the manifest, a `null` value will be returned instead.

## Experimental features

Starting from `specVersion` `0.0.4`, subgraph features must be explicitly declared in the `features` section at the top level of the manifest file, using their `camelCase` name, as listed in the table below:

| Feature                                              | Name             |
| ---------------------------------------------------- | ---------------- |
| [Non-fatal errors](#non-fatal-errors)                | `nonFatalErrors` |
| [Full-text Search](#defining-fulltext-search-fields) | `fullTextSearch` |
| [Grafting](#grafting-onto-existing-subgraphs)        | `grafting`       |

For instance, if a subgraph uses the **Full-Text Search** and the **Non-fatal Errors** features, the `features` field in the manifest should be:

```yaml
specVersion: 0.0.4
description: Gravatar for Ethereum
features:
  - fullTextSearch
  - nonFatalErrors
dataSources: ...
```

Note that using a feature without declaring it will incur a **validation error** during subgraph deployment, but no errors will occur if a feature is declared but not used.

### Timeseries and Aggregations

Timeseries and aggregations enable your subgraph to track statistics like daily average price, hourly total transfers, etc.

This feature introduces two new types of subgraph entity. Timeseries entities record data points with timestamps. Aggregation entities perform pre-declared calculations on the Timeseries data points on an hourly or daily basis, then store the results for easy access via GraphQL.

#### Example Schema

```graphql
type Data @entity(timeseries: true) {
  id: Int8!
  timestamp: Timestamp!
  price: BigDecimal!
}

type Stats @aggregation(intervals: ["hour", "day"], source: "Data") {
  id: Int8!
  timestamp: Timestamp!
  sum: BigDecimal! @aggregate(fn: "sum", arg: "price")
}
```

### Defining Timeseries and Aggregations

Timeseries entities are defined with `@entity(timeseries: true)` in schema.graphql. Every timeseries entity must have a unique ID of the int8 type, a timestamp of the Timestamp type, and include data that will be used for calculation by aggregation entities. These Timeseries entities can be saved in regular trigger handlers, and act as the “raw data” for the Aggregation entities.

Aggregation entities are defined with `@aggregation` in schema.graphql. Every aggregation entity defines the source from which it will gather data (which must be a Timeseries entity), sets the intervals (e.g., hour, day), and specifies the aggregation function it will use (e.g., sum, count, min, max, first, last). Aggregation entities are automatically calculated on the basis of the specified source at the end of the required interval.

#### Available Aggregation Intervals

- `hour`: sets the timeseries period every hour, on the hour.
- `day`: sets the timeseries period every day, starting and ending at 00:00.

#### Available Aggregation Functions

- `sum`: Total of all values.
- `count`: Number of values.
- `min`: Minimum value.
- `max`: Maximum value.
- `first`: First value in the period.
- `last`: Last value in the period.

#### Example Aggregations Query

```graphql
{
  stats(interval: "hour", where: { timestamp_gt: 1704085200 }) {
    id
    timestamp
    sum
  }
}
```

Note:

To use Timeseries and Aggregations, a subgraph must have a spec version ≥1.1.0. Note that this feature might undergo significant changes that could affect backward compatibility.

[Read more](https://github.com/graphprotocol/graph-node/blob/master/docs/aggregations.md) about Timeseries and Aggregations.

### Non-fatal errors

Indexing errors on already synced subgraphs will, by default, cause the subgraph to fail and stop syncing. Subgraphs can alternatively be configured to continue syncing in the presence of errors, by ignoring the changes made by the handler which provoked the error. This gives subgraph authors time to correct their subgraphs while queries continue to be served against the latest block, though the results might be inconsistent due to the bug that caused the error. Note that some errors are still always fatal. To be non-fatal, the error must be known to be deterministic.

> **Note:** The Graph Network does not yet support non-fatal errors, and developers should not deploy subgraphs using that functionality to the network via the Studio.

Enabling non-fatal errors requires setting the following feature flag on the subgraph manifest:

```yaml
specVersion: 0.0.4
description: Gravatar for Ethereum
features:
    - nonFatalErrors
    ...
```

The query must also opt-in to querying data with potential inconsistencies through the `subgraphError` argument. It is also recommended to query `_meta` to check if the subgraph has skipped over errors, as in the example:

```graphql
foos(first: 100, subgraphError: allow) {
  id
}

_meta {
  hasIndexingErrors
}
```

If the subgraph encounters an error, that query will return both the data and a graphql error with the message `"indexing_error"`, as in this example response:

```graphql
"data": {
    "foos": [
        {
          "id": "0xdead"
        }
    ],
    "_meta": {
        "hasIndexingErrors": true
    }
},
"errors": [
    {
        "message": "indexing_error"
    }
]
```

### Grafting onto Existing Subgraphs

> **Note:** it is not recommended to use grafting when initially upgrading to The Graph Network. Learn more [here](/cookbook/grafting/#important-note-on-grafting-when-upgrading-to-the-network).

When a subgraph is first deployed, it starts indexing events at the genesis block of the corresponding chain (or at the `startBlock` defined with each data source) In some circumstances; it is beneficial to reuse the data from an existing subgraph and start indexing at a much later block. This mode of indexing is called _Grafting_. Grafting is, for example, useful during development to get past simple errors in the mappings quickly or to temporarily get an existing subgraph working again after it has failed.

A subgraph is grafted onto a base subgraph when the subgraph manifest in `subgraph.yaml` contains a `graft` block at the top-level:

```yaml
description: ...
graft:
  base: Qm... # Subgraph ID of base subgraph
  block: 7345624 # Block number
```

When a subgraph whose manifest contains a `graft` block is deployed, Graph Node will copy the data of the `base` subgraph up to and including the given `block` and then continue indexing the new subgraph from that block on. The base subgraph must exist on the target Graph Node instance and must have indexed up to at least the given block. Because of this restriction, grafting should only be used during development or during an emergency to speed up producing an equivalent non-grafted subgraph.

Because grafting copies rather than indexes base data, it is much quicker to get the subgraph to the desired block than indexing from scratch, though the initial data copy can still take several hours for very large subgraphs. While the grafted subgraph is being initialized, the Graph Node will log information about the entity types that have already been copied.

The grafted subgraph can use a GraphQL schema that is not identical to the one of the base subgraph, but merely compatible with it. It has to be a valid subgraph schema in its own right, but may deviate from the base subgraph's schema in the following ways:

- It adds or removes entity types
- It removes attributes from entity types
- It adds nullable attributes to entity types
- It turns non-nullable attributes into nullable attributes
- It adds values to enums
- It adds or removes interfaces
- It changes for which entity types an interface is implemented

> **[Feature Management](#experimental-features):** `grafting` must be declared under `features` in the subgraph manifest.

## IPFS/Arweave File Data Sources

File data sources are a new subgraph functionality for accessing off-chain data during indexing in a robust, extendable way. File data sources support fetching files from IPFS and from Arweave.

> This also lays the groundwork for deterministic indexing of off-chain data, as well as the potential introduction of arbitrary HTTP-sourced data.

### Overview

Rather than fetching files "in line" during handler execution, this introduces templates which can be spawned as new data sources for a given file identifier. These new data sources fetch the files, retrying if they are unsuccessful, running a dedicated handler when the file is found.

This is similar to the [existing data source templates](/developing/creating-a-subgraph/#data-source-templates), which are used to dynamically create new chain-based data sources.

> This replaces the existing `ipfs.cat` API

### Upgrade guide

#### Update `graph-ts` and `graph-cli`

File data sources requires graph-ts >=0.29.0 and graph-cli >=0.33.1

#### Add a new entity type which will be updated when files are found

File data sources cannot access or update chain-based entities, but must update file specific entities.

This may mean splitting out fields from existing entities into separate entities, linked together.

Original combined entity:

```graphql
type Token @entity {
  id: ID!
  tokenID: BigInt!
  tokenURI: String!
  externalURL: String!
  ipfsURI: String!
  image: String!
  name: String!
  description: String!
  type: String!
  updatedAtTimestamp: BigInt
  owner: User!
}
```

New, split entity:

```graphql
type Token @entity {
  id: ID!
  tokenID: BigInt!
  tokenURI: String!
  ipfsURI: TokenMetadata
  updatedAtTimestamp: BigInt
  owner: String!
}

type TokenMetadata @entity {
  id: ID!
  image: String!
  externalURL: String!
  name: String!
  description: String!
}
```

If the relationship is 1:1 between the parent entity and the resulting file data source entity, the simplest pattern is to link the parent entity to a resulting file entity by using the IPFS CID as the lookup. Get in touch on Discord if you are having difficulty modelling your new file-based entities!

> You can use [nested filters](/querying/graphql-api/#example-for-nested-entity-filtering) to filter parent entities on the basis of these nested entities.

#### Add a new templated data source with `kind: file/ipfs` or `kind: file/arweave`

This is the data source which will be spawned when a file of interest is identified.

```yaml
templates:
  - name: TokenMetadata
    kind: file/ipfs
    mapping:
      apiVersion: 0.0.7
      language: wasm/assemblyscript
      file: ./src/mapping.ts
      handler: handleMetadata
      entities:
        - TokenMetadata
      abis:
        - name: Token
          file: ./abis/Token.json
```

> Currently `abis` are required, though it is not possible to call contracts from within file data sources

The file data source must specifically mention all the entity types which it will interact with under `entities`. See [limitations](#limitations) for more details.

#### Create a new handler to process files

This handler should accept one `Bytes` parameter, which will be the contents of the file, when it is found, which can then be processed. This will often be a JSON file, which can be processed with `graph-ts` helpers ([documentation](/developing/graph-ts/api/#json-api)).

The CID of the file as a readable string can be accessed via the `dataSource` as follows:

```typescript
const cid = dataSource.stringParam()
```

Example handler:

```typescript
import { json, Bytes, dataSource } from '@graphprotocol/graph-ts'
import { TokenMetadata } from '../generated/schema'

export function handleMetadata(content: Bytes): void {
  let tokenMetadata = new TokenMetadata(dataSource.stringParam())
  const value = json.fromBytes(content).toObject()
  if (value) {
    const image = value.get('image')
    const name = value.get('name')
    const description = value.get('description')
    const externalURL = value.get('external_url')

    if (name && image && description && externalURL) {
      tokenMetadata.name = name.toString()
      tokenMetadata.image = image.toString()
      tokenMetadata.externalURL = externalURL.toString()
      tokenMetadata.description = description.toString()
    }

    tokenMetadata.save()
  }
}
```

#### Spawn file data sources when required

You can now create file data sources during execution of chain-based handlers:

- Import the template from the auto-generated `templates`
- call `TemplateName.create(cid: string)` from within a mapping, where the cid is a valid content identifier for IPFS or Arweave

For IPFS, Graph Node supports [v0 and v1 content identifiers](https://docs.ipfs.tech/concepts/content-addressing/), and content identifers with directories (e.g. `bafyreighykzv2we26wfrbzkcdw37sbrby4upq7ae3aqobbq7i4er3tnxci/metadata.json`).

For Arweave, as of version 0.33.0 Graph Node can fetch files stored on Arweave based on their [transaction ID](https://docs.arweave.org/developers/arweave-node-server/http-api#transactions) from an Arweave gateway ([example file](https://bdxujjl5ev5eerd5ouhhs6o4kjrs4g6hqstzlci5pf6vhxezkgaa.arweave.net/CO9EpX0lekJEfXUOeXncUmMuG8eEp5WJHXl9U9yZUYA)). Arweave supports transactions uploaded via Irys (previously Bundlr), and Graph Node can also fetch files based on [Irys manifests](https://docs.irys.xyz/overview/gateways#indexing).

Example:

```typescript
import { TokenMetadata as TokenMetadataTemplate } from '../generated/templates'

const ipfshash = 'QmaXzZhcYnsisuue5WRdQDH6FDvqkLQX1NckLqBYeYYEfm'
//This example code is for a Crypto coven subgraph. The above ipfs hash is a directory with token metadata for all crypto coven NFTs.

export function handleTransfer(event: TransferEvent): void {
  let token = Token.load(event.params.tokenId.toString())
  if (!token) {
    token = new Token(event.params.tokenId.toString())
    token.tokenID = event.params.tokenId

    token.tokenURI = '/' + event.params.tokenId.toString() + '.json'
    const tokenIpfsHash = ipfshash + token.tokenURI
    //This creates a path to the metadata for a single Crypto coven NFT. It concats the directory with "/" + filename + ".json"

    token.ipfsURI = tokenIpfsHash

    TokenMetadataTemplate.create(tokenIpfsHash)
  }

  token.updatedAtTimestamp = event.block.timestamp
  token.owner = event.params.to.toHexString()
  token.save()
}
```

This will create a new file data source, which will poll Graph Node's configured IPFS or Arweave endpoint, retrying if it is not found. When the file is found, the file data source handler will be executed.

This example is using the CID as the lookup between the parent `Token` entity and the resulting `TokenMetadata` entity.

> Previously, this is the point at which a subgraph developer would have called `ipfs.cat(CID)` to fetch the file

Congratulations, you are using file data sources!

#### Deploying your subgraphs

You can now `build` and `deploy` your subgraph to any Graph Node >=v0.30.0-rc.0.

#### Limitations

File data source handlers and entities are isolated from other subgraph entities, ensuring that they are deterministic when executed, and ensuring no contamination of chain-based data sources. To be specific:

- Entities created by File Data Sources are immutable, and cannot be updated
- File Data Source handlers cannot access entities from other file data sources
- Entities associated with File Data Sources cannot be accessed by chain-based handlers

> While this constraint should not be problematic for most use-cases, it may introduce complexity for some. Please get in touch via Discord if you are having issues modelling your file-based data in a subgraph!

Additionally, it is not possible to create data sources from a file data source, be it an onchain data source or another file data source. This restriction may be lifted in the future.

#### Best practices

If you are linking NFT metadata to corresponding tokens, use the metadata's IPFS hash to reference a Metadata entity from the Token entity. Save the Metadata entity using the IPFS hash as an ID.

You can use [DataSource context](/developing/graph-ts/api/#entity-and-datasourcecontext) when creating File Data Sources to pass extra information which will be available to the File Data Source handler.

If you have entities which are refreshed multiple times, create unique file-based entities using the IPFS hash & the entity ID, and reference them using a derived field in the chain-based entity.

> We are working to improve the above recommendation, so queries only return the "most recent" version

#### Known issues

File data sources currently require ABIs, even though ABIs are not used ([issue](https://github.com/graphprotocol/graph-cli/issues/961)). Workaround is to add any ABI.

Handlers for File Data Sources cannot be in files which import `eth_call` contract bindings, failing with "unknown import: `ethereum::ethereum.call` has not been defined" ([issue](https://github.com/graphprotocol/graph-node/issues/4309)). Workaround is to create file data source handlers in a dedicated file.

#### Examples

[Crypto Coven Subgraph migration](https://github.com/azf20/cryptocoven-api/tree/file-data-sources-refactor)

#### References

[GIP File Data Sources](https://forum.thegraph.com/t/gip-file-data-sources/2721)
---
title: Common AssemblyScript Issues
---

There are certain [AssemblyScript](https://github.com/AssemblyScript/assemblyscript) issues that are common to run into during subgraph development. They range in debug difficulty, however, being aware of them may help. The following is a non-exhaustive list of these issues:

- `Private` class variables are not enforced in [AssembyScript](https://www.assemblyscript.org/status.html#language-features). There is no way to protect class variables from being directly changed from the class object.
- Scope is not inherited into [closure functions](https://www.assemblyscript.org/status.html#on-closures), i.e. variables declared outside of closure functions cannot be used. Explanation in [Developer Highlights #3](https://www.youtube.com/watch?v=1-8AW-lVfrA&t=3243s).
import { RemoteContent } from 'nextra/data'
import { buildDynamicMDX } from 'nextra/remote'
import { buildGetStaticProps } from '@/src/buildGetStaticProps'
import { remarkReplaceLinks } from '@/src/remarkReplaceLinks'
import { Mermaid } from 'nextra/components'
import { visit } from 'unist-util-visit'
import json from '@/remote-files/graph-ts.json'

export const getStaticPaths = () => ({
  fallback: false,
  paths: json.filePaths.map((filePath) => ({
    params: {
      slug: filePath.replace(/\.mdx?/, '').split('/'),
    },
  })),
})

export const getStaticProps = buildGetStaticProps(__filename, async ({ params }) => {
  const { filePaths, user, repo, branch, docsPath } = json
  const paths = params?.slug?.join('/')
  const foundPath = filePaths.find((filePath) => filePath.startsWith(paths))
  const baseURL = `https://raw.githubusercontent.com/${user}/${repo}/${branch}/${docsPath}${foundPath}`
  const response = await fetch(baseURL)
  const content = await response.text()
  const mdx = await buildDynamicMDX(content, {
    mdxOptions: {
      format: 'md',
      remarkPlugins: [
        () => (tree, _file) => {
          visit(tree, 'link', (node) => {
            if (node.url.startsWith('../')) {
              node.url = node.url.replace('../', `https://github.com/${user}/${repo}/tree/${branch}/`)
            }
          })
        },
        [remarkReplaceLinks, { foundPath, basePath: '/developing/graph-ts/' }],
      ],
    },
    codeHighlight: false,
  })
  return {
    props: {
      ...mdx,
      hideLocaleSwitcher: true,
      remoteFilePath: `https://github.com/${user}/${repo}/tree/${branch}/${docsPath}${foundPath}`,
    },
  }
})

<RemoteContent components={{ Mermaid }} />
---
title: AssemblyScript API
---

> Note: If you created a subgraph prior to `graph-cli`/`graph-ts` version `0.22.0`, then you're using an older version of AssemblyScript. It is recommended to review the [`Migration Guide`](/release-notes/assemblyscript-migration-guide).

Learn what built-in APIs can be used when writing subgraph mappings. There are two kinds of APIs available out of the box:

- The [Graph TypeScript library](https://github.com/graphprotocol/graph-tooling/tree/main/packages/ts) (`graph-ts`)
- Code generated from subgraph files by `graph codegen`

You can also add other libraries as dependencies, as long as they are compatible with [AssemblyScript](https://github.com/AssemblyScript/assemblyscript).

Since language mappings are written in AssemblyScript, it is useful to review the language and standard library features from the [AssemblyScript wiki](https://github.com/AssemblyScript/assemblyscript/wiki).

## API Reference

The `@graphprotocol/graph-ts` library provides the following APIs:

- An `ethereum` API for working with Ethereum smart contracts, events, blocks, transactions, and Ethereum values.
- A `store` API to load and save entities from and to the Graph Node store.
- A `log` API to log messages to the Graph Node output and Graph Explorer.
- An `ipfs` API to load files from IPFS.
- A `json` API to parse JSON data.
- A `crypto` API to use cryptographic functions.
- Low-level primitives to translate between different type systems such as Ethereum, JSON, GraphQL and AssemblyScript.

### Versions

The `apiVersion` in the subgraph manifest specifies the mapping API version which is run by Graph Node for a given subgraph.

| Version | Release notes |
| :-: | --- |
| 0.0.9 | Adds new host functions [`eth_get_balance`](#balance-of-an-address) & [`hasCode`](#check-if-an-address-is-a-contract-or-eoa) |
| 0.0.8 | Adds validation for existence of fields in the schema when saving an entity. |
| 0.0.7 | Added `TransactionReceipt` and `Log` classes to the Ethereum types<br />Added `receipt` field to the Ethereum Event object |
| 0.0.6 | Added `nonce` field to the Ethereum Transaction object<br />Added `baseFeePerGas` to the Ethereum Block object |
| 0.0.5 | AssemblyScript upgraded to version 0.19.10 (this includes breaking changes, please see the [`Migration Guide`](/release-notes/assemblyscript-migration-guide))<br />`ethereum.transaction.gasUsed` renamed to `ethereum.transaction.gasLimit` |
| 0.0.4 | Added `functionSignature` field to the Ethereum SmartContractCall object |
| 0.0.3 | Added `from` field to the Ethereum Call object<br />`etherem.call.address` renamed to `ethereum.call.to` |
| 0.0.2 | Added `input` field to the Ethereum Transaction object |

### Built-in Types

Documentation on the base types built into AssemblyScript can be found in the [AssemblyScript wiki](https://www.assemblyscript.org/types.html).

The following additional types are provided by `@graphprotocol/graph-ts`.

#### ByteArray

```typescript
import { ByteArray } from '@graphprotocol/graph-ts'
```

`ByteArray` represents an array of `u8`.

_Construction_

- `fromI32(x: i32): ByteArray` - Decomposes `x` into bytes.
- `fromHexString(hex: string): ByteArray` - Input length must be even. Prefixing with `0x` is optional.

_Type conversions_

- `toHexString(): string` - Converts to a hex string prefixed with `0x`.
- `toString(): string` - Interprets the bytes as a UTF-8 string.
- `toBase58(): string` - Encodes the bytes into a base58 string.
- `toU32(): u32` - Interprets the bytes as a little-endian `u32`. Throws in case of overflow.
- `toI32(): i32` - Interprets the byte array as a little-endian `i32`. Throws in case of overflow.

_Operators_

- `equals(y: ByteArray): bool` – can be written as `x == y`.
- `concat(other: ByteArray) : ByteArray` - return a new `ByteArray` consisting of `this` directly followed by `other`
- `concatI32(other: i32) : ByteArray` - return a new `ByteArray` consisting of `this` directly followed by the byte representation of `other`

#### BigDecimal

```typescript
import { BigDecimal } from '@graphprotocol/graph-ts'
```

`BigDecimal` is used to represent arbitrary precision decimals.

> Note: [Internally](https://github.com/graphprotocol/graph-node/blob/master/graph/src/data/store/scalar/bigdecimal.rs) `BigDecimal` is stored in [IEEE-754 decimal128 floating-point format](https://en.wikipedia.org/wiki/Decimal128_floating-point_format), which supports 34 decimal digits of significand. This makes `BigDecimal` unsuitable for representing fixed-point types that can span wider than 34 digits, such as a Solidity [`ufixed256x18`](https://docs.soliditylang.org/en/latest/types.html#fixed-point-numbers) or equivalent.

_Construction_

- `constructor(bigInt: BigInt)` – creates a `BigDecimal` from an `BigInt`.
- `static fromString(s: string): BigDecimal` – parses from a decimal string.

_Type conversions_

- `toString(): string` – prints to a decimal string.

_Math_

- `plus(y: BigDecimal): BigDecimal` – can be written as `x + y`.
- `minus(y: BigDecimal): BigDecimal` – can be written as `x - y`.
- `times(y: BigDecimal): BigDecimal` – can be written as `x * y`.
- `div(y: BigDecimal): BigDecimal` – can be written as `x / y`.
- `equals(y: BigDecimal): bool` – can be written as `x == y`.
- `notEqual(y: BigDecimal): bool` – can be written as `x != y`.
- `lt(y: BigDecimal): bool` – can be written as `x < y`.
- `le(y: BigDecimal): bool` – can be written as `x <= y`.
- `gt(y: BigDecimal): bool` – can be written as `x > y`.
- `ge(y: BigDecimal): bool` – can be written as `x >= y`.
- `neg(): BigDecimal` - can be written as `-x`.

#### BigInt

```typescript
import { BigInt } from '@graphprotocol/graph-ts'
```

`BigInt` is used to represent big integers. This includes Ethereum values of type `uint32` to `uint256` and `int64` to `int256`. Everything below `uint32`, such as `int32`, `uint24` or `int8` is represented as `i32`.

The `BigInt` class has the following API:

_Construction_

- `BigInt.fromI32(x: i32): BigInt` – creates a `BigInt` from an `i32`.
- `BigInt.fromString(s: string): BigInt`– Parses a `BigInt` from a string.
- `BigInt.fromUnsignedBytes(x: Bytes): BigInt` – Interprets `bytes` as an unsigned, little-endian integer. If your input is big-endian, call `.reverse()` first.
- `BigInt.fromSignedBytes(x: Bytes): BigInt` – Interprets `bytes` as a signed, little-endian integer. If your input is big-endian, call `.reverse()` first.

  _Type conversions_

- `x.toHex(): string` – turns `BigInt` into a string of hexadecimal characters.
- `x.toString(): string` – turns `BigInt` into a decimal number string.
- `x.toI32(): i32` – returns the `BigInt` as an `i32`; fails if the value does not fit into `i32`. It's a good idea to first check `x.isI32()`.
- `x.toBigDecimal(): BigDecimal` - converts into a decimal with no fractional part.

_Math_

- `x.plus(y: BigInt): BigInt` – can be written as `x + y`.
- `x.minus(y: BigInt): BigInt` – can be written as `x - y`.
- `x.times(y: BigInt): BigInt` – can be written as `x * y`.
- `x.div(y: BigInt): BigInt` – can be written as `x / y`.
- `x.mod(y: BigInt): BigInt` – can be written as `x % y`.
- `x.equals(y: BigInt): bool` – can be written as `x == y`.
- `x.notEqual(y: BigInt): bool` – can be written as `x != y`.
- `x.lt(y: BigInt): bool` – can be written as `x < y`.
- `x.le(y: BigInt): bool` – can be written as `x <= y`.
- `x.gt(y: BigInt): bool` – can be written as `x > y`.
- `x.ge(y: BigInt): bool` – can be written as `x >= y`.
- `x.neg(): BigInt` – can be written as `-x`.
- `x.divDecimal(y: BigDecimal): BigDecimal` – divides by a decimal, giving a decimal result.
- `x.isZero(): bool` – Convenience for checking if the number is zero.
- `x.isI32(): bool` – Check if the number fits in an `i32`.
- `x.abs(): BigInt` – Absolute value.
- `x.pow(exp: u8): BigInt` – Exponentiation.
- `bitOr(x: BigInt, y: BigInt): BigInt` – can be written as `x | y`.
- `bitAnd(x: BigInt, y: BigInt): BigInt` – can be written as `x & y`.
- `leftShift(x: BigInt, bits: u8): BigInt` – can be written as `x << y`.
- `rightShift(x: BigInt, bits: u8): BigInt` – can be written as `x >> y`.

#### TypedMap

```typescript
import { TypedMap } from '@graphprotocol/graph-ts'
```

`TypedMap` can be used to store key-value pairs. See [this example](https://github.com/graphprotocol/aragon-subgraph/blob/29dd38680c5e5104d9fdc2f90e740298c67e4a31/individual-dao-subgraph/mappings/constants.ts#L51).

The `TypedMap` class has the following API:

- `new TypedMap<K, V>()` – creates an empty map with keys of type `K` and values of type `V`
- `map.set(key: K, value: V): void` – sets the value of `key` to `value`
- `map.getEntry(key: K): TypedMapEntry<K, V> | null` – returns the key-value pair for a `key` or `null` if the `key` does not exist in the map
- `map.get(key: K): V | null` – returns the value for a `key` or `null` if the `key` does not exist in the map
- `map.isSet(key: K): bool` – returns `true` if the `key` exists in the map and `false` if it does not

#### Bytes

```typescript
import { Bytes } from '@graphprotocol/graph-ts'
```

`Bytes` is used to represent arbitrary-length arrays of bytes. This includes Ethereum values of type `bytes`, `bytes32`, etc.

The `Bytes` class extends AssemblyScript's [Uint8Array](https://github.com/AssemblyScript/assemblyscript/blob/3b1852bc376ae799d9ebca888e6413afac7b572f/std/assembly/typedarray.ts#L64) and this supports all the `Uint8Array` functionality, plus the following new methods:

_Construction_

- `fromHexString(hex: string) : Bytes` - Convert the string `hex` which must consist of an even number of hexadecimal digits to a `ByteArray`. The string `hex` can optionally start with `0x`
- `fromI32(i: i32) : Bytes` - Convert `i` to an array of bytes

_Type conversions_

- `b.toHex()` – returns a hexadecimal string representing the bytes in the array
- `b.toString()` – converts the bytes in the array to a string of unicode characters
- `b.toBase58()` – turns an Ethereum Bytes value to base58 encoding (used for IPFS hashes)

_Operators_

- `b.concat(other: Bytes) : Bytes` - - return new `Bytes` consisting of `this` directly followed by `other`
- `b.concatI32(other: i32) : ByteArray` - return new `Bytes` consisting of `this` directly follow by the byte representation of `other`

#### Address

```typescript
import { Address } from '@graphprotocol/graph-ts'
```

`Address` extends `Bytes` to represent Ethereum `address` values.

It adds the following method on top of the `Bytes` API:

- `Address.fromString(s: string): Address` – creates an `Address` from a hexadecimal string
- `Address.fromBytes(b: Bytes): Address` – create an `Address` from `b` which must be exactly 20 bytes long. Passing in a value with fewer or more bytes will result in an error

### Store API

```typescript
import { store } from '@graphprotocol/graph-ts'
```

The `store` API allows to load, save and remove entities from and to the Graph Node store.

Entities written to the store map one-to-one to the `@entity` types defined in the subgraph's GraphQL schema. To make working with these entities convenient, the `graph codegen` command provided by the [Graph CLI](https://github.com/graphprotocol/graph-tooling/tree/main/packages/cli) generates entity classes, which are subclasses of the built-in `Entity` type, with property getters and setters for the fields in the schema as well as methods to load and save these entities.

#### Creating entities

The following is a common pattern for creating entities from Ethereum events.

```typescript
// Import the Transfer event class generated from the ERC20 ABI
import { Transfer as TransferEvent } from '../generated/ERC20/ERC20'

// Import the Transfer entity type generated from the GraphQL schema
import { Transfer } from '../generated/schema'

// Transfer event handler
export function handleTransfer(event: TransferEvent): void {
  // Create a Transfer entity, using the transaction hash as the entity ID
  let id = event.transaction.hash
  let transfer = new Transfer(id)

  // Set properties on the entity, using the event parameters
  transfer.from = event.params.from
  transfer.to = event.params.to
  transfer.amount = event.params.amount

  // Save the entity to the store
  transfer.save()
}
```

When a `Transfer` event is encountered while processing the chain, it is passed to the `handleTransfer` event handler using the generated `Transfer` type (aliased to `TransferEvent` here to avoid a naming conflict with the entity type). This type allows accessing data such as the event's parent transaction and its parameters.

Each entity must have a unique ID to avoid collisions with other entities. It is fairly common for event parameters to include a unique identifier that can be used.

> Note: Using the transaction hash as the ID assumes that no other events in the same transaction create entities with this hash as the ID.

#### Loading entities from the store

If an entity already exists, it can be loaded from the store with the following:

```typescript
let id = event.transaction.hash // or however the ID is constructed
let transfer = Transfer.load(id)
if (transfer == null) {
  transfer = new Transfer(id)
}

// Use the Transfer entity as before
```

As the entity may not exist in the store yet, the `load` method returns a value of type `Transfer | null`. It may be necessary to check for the `null` case before using the value.

> Note: Loading entities is only necessary if the changes made in the mapping depend on the previous data of an entity. See the next section for the two ways of updating existing entities.

#### Looking up entities created withing a block

As of `graph-node` v0.31.0, `@graphprotocol/graph-ts` v0.30.0 and `@graphprotocol/graph-cli` v0.49.0 the `loadInBlock` method is available on all entity types.

The store API facilitates the retrieval of entities that were created or updated in the current block. A typical situation for this is that one handler creates a transaction from some on-chain event, and a later handler wants to access this transaction if it exists.

- In the case where the transaction does not exist, the subgraph will have to go to the database simply to find out that the entity does not exist. If the subgraph author already knows that the entity must have been created in the same block, using `loadInBlock` avoids this database roundtrip.
- For some subgraphs, these missed lookups can contribute significantly to the indexing time.

```typescript
let id = event.transaction.hash // or however the ID is constructed
let transfer = Transfer.loadInBlock(id)
if (transfer == null) {
  transfer = new Transfer(id)
}

// Use the Transfer entity as before
```

> Note: If there is no entity created in the given block, `loadInBlock` will return `null` even if there is an entity with the given ID in the store.

#### Looking up derived entities

As of `graph-node` v0.31.0, `@graphprotocol/graph-ts` v0.31.0 and `@graphprotocol/graph-cli` v0.51.0 the `loadRelated` method is available.

This enables loading derived entity fields from within an event handler. For example, given the following schema:

```graphql
type Token @entity {
  id: ID!
  holder: Holder!
  color: String
}

type Holder @entity {
  id: ID!
  tokens: [Token!]! @derivedFrom(field: "holder")
}
```

The following code will load the `Token` entity that the `Holder` entity was derived from:

```typescript
let holder = Holder.load('test-id')
// Load the Token entities associated with a given holder
let tokens = holder.tokens.load()
```

#### Updating existing entities

There are two ways to update an existing entity:

1. Load the entity with e.g. `Transfer.load(id)`, set properties on the entity, then `.save()` it back to the store.
2. Simply create the entity with e.g. `new Transfer(id)`, set properties on the entity, then `.save()` it to the store. If the entity already exists, the changes are merged into it.

Changing properties is straight forward in most cases, thanks to the generated property setters:

```typescript
let transfer = new Transfer(id)
transfer.from = ...
transfer.to = ...
transfer.amount = ...
```

It is also possible to unset properties with one of the following two instructions:

```typescript
transfer.from.unset()
transfer.from = null
```

This only works with optional properties, i.e. properties that are declared without a `!` in GraphQL. Two examples would be `owner: Bytes` or `amount: BigInt`.

Updating array properties is a little more involved, as the getting an array from an entity creates a copy of that array. This means array properties have to be set again explicitly after changing the array. The following assumes `entity` has a `numbers: [BigInt!]!` field.

```typescript
// This won't work
entity.numbers.push(BigInt.fromI32(1))
entity.save()

// This will work
let numbers = entity.numbers
numbers.push(BigInt.fromI32(1))
entity.numbers = numbers
entity.save()
```

#### Removing entities from the store

There is currently no way to remove an entity via the generated types. Instead, removing an entity requires passing the name of the entity type and the entity ID to `store.remove`:

```typescript
import { store } from '@graphprotocol/graph-ts'
...
let id = event.transaction.hash
store.remove('Transfer', id)
```

### Ethereum API

The Ethereum API provides access to smart contracts, public state variables, contract functions, events, transactions, blocks and the encoding/decoding Ethereum data.

#### Support for Ethereum Types

As with entities, `graph codegen` generates classes for all smart contracts and events used in a subgraph. For this, the contract ABIs need to be part of the data source in the subgraph manifest. Typically, the ABI files are stored in an `abis/` folder.

With the generated classes, conversions between Ethereum types and the [built-in types](#built-in-types) take place behind the scenes so that subgraph authors do not have to worry about them.

The following example illustrates this. Given a subgraph schema like

```graphql
type Transfer @entity {
  id: Bytes!
  from: Bytes!
  to: Bytes!
  amount: BigInt!
}
```

and a `Transfer(address,address,uint256)` event signature on Ethereum, the `from`, `to` and `amount` values of type `address`, `address` and `uint256` are converted to `Address` and `BigInt`, allowing them to be passed on to the `Bytes!` and `BigInt!` properties of the `Transfer` entity:

```typescript
let id = event.transaction.hash
let transfer = new Transfer(id)
transfer.from = event.params.from
transfer.to = event.params.to
transfer.amount = event.params.amount
transfer.save()
```

#### Events and Block/Transaction Data

Ethereum events passed to event handlers, such as the `Transfer` event in the previous examples, not only provide access to the event parameters but also to their parent transaction and the block they are part of. The following data can be obtained from `event` instances (these classes are a part of the `ethereum` module in `graph-ts`):

```typescript
class Event {
  address: Address
  logIndex: BigInt
  transactionLogIndex: BigInt
  logType: string | null
  block: Block
  transaction: Transaction
  parameters: Array<EventParam>
  receipt: TransactionReceipt | null
}

class Block {
  hash: Bytes
  parentHash: Bytes
  unclesHash: Bytes
  author: Address
  stateRoot: Bytes
  transactionsRoot: Bytes
  receiptsRoot: Bytes
  number: BigInt
  gasUsed: BigInt
  gasLimit: BigInt
  timestamp: BigInt
  difficulty: BigInt
  totalDifficulty: BigInt
  size: BigInt | null
  baseFeePerGas: BigInt | null
}

class Transaction {
  hash: Bytes
  index: BigInt
  from: Address
  to: Address | null
  value: BigInt
  gasLimit: BigInt
  gasPrice: BigInt
  input: Bytes
  nonce: BigInt
}

class TransactionReceipt {
  transactionHash: Bytes
  transactionIndex: BigInt
  blockHash: Bytes
  blockNumber: BigInt
  cumulativeGasUsed: BigInt
  gasUsed: BigInt
  contractAddress: Address
  logs: Array<Log>
  status: BigInt
  root: Bytes
  logsBloom: Bytes
}

class Log {
  address: Address
  topics: Array<Bytes>
  data: Bytes
  blockHash: Bytes
  blockNumber: Bytes
  transactionHash: Bytes
  transactionIndex: BigInt
  logIndex: BigInt
  transactionLogIndex: BigInt
  logType: string
  removed: bool | null
}
```

#### Access to Smart Contract State

The code generated by `graph codegen` also includes classes for the smart contracts used in the subgraph. These can be used to access public state variables and call functions of the contract at the current block.

A common pattern is to access the contract from which an event originates. This is achieved with the following code:

```typescript
// Import the generated contract class and generated Transfer event class
import { ERC20Contract, Transfer as TransferEvent } from '../generated/ERC20Contract/ERC20Contract'
// Import the generated entity class
import { Transfer } from '../generated/schema'

export function handleTransfer(event: TransferEvent) {
  // Bind the contract to the address that emitted the event
  let contract = ERC20Contract.bind(event.address)

  // Access state variables and functions by calling them
  let erc20Symbol = contract.symbol()
}
```

`Transfer` is aliased to `TransferEvent` here to avoid a naming conflict with the entity type

As long as the `ERC20Contract` on Ethereum has a public read-only function called `symbol`, it can be called with `.symbol()`. For public state variables a method with the same name is created automatically.

Any other contract that is part of the subgraph can be imported from the generated code and can be bound to a valid address.

#### Handling Reverted Calls

If the read-only methods of your contract may revert, then you should handle that by calling the generated contract method prefixed with `try_`.

- For example, the Gravity contract exposes the `gravatarToOwner` method. This code would be able to handle a revert in that method:

```typescript
let gravity = Gravity.bind(event.address)
let callResult = gravity.try_gravatarToOwner(gravatar)
if (callResult.reverted) {
  log.info('getGravatar reverted', [])
} else {
  let owner = callResult.value
}
```

> Note: A Graph node connected to a Geth or Infura client may not detect all reverts. If you rely on this, we recommend using a Graph Node connected to a Parity client.

#### Encoding/Decoding ABI

Data can be encoded and decoded according to Ethereum's ABI encoding format using the `encode` and `decode` functions in the `ethereum` module.

```typescript
import { Address, BigInt, ethereum } from '@graphprotocol/graph-ts'

let tupleArray: Array<ethereum.Value> = [
  ethereum.Value.fromAddress(Address.fromString('0x0000000000000000000000000000000000000420')),
  ethereum.Value.fromUnsignedBigInt(BigInt.fromI32(62)),
]

let tuple = tupleArray as ethereum.Tuple

let encoded = ethereum.encode(ethereum.Value.fromTuple(tuple))!

let decoded = ethereum.decode('(address,uint256)', encoded)
```

For more information:

- [ABI Spec](https://docs.soliditylang.org/en/v0.7.4/abi-spec.html#types)
- Encoding/decoding [Rust library/CLI](https://github.com/rust-ethereum/ethabi)
- More [complex example](https://github.com/graphprotocol/graph-node/blob/08da7cb46ddc8c09f448c5ea4b210c9021ea05ad/tests/integration-tests/host-exports/src/mapping.ts#L86).

#### Balance of an Address

The native token balance of an address can be retrieved using the `ethereum` module. This feature is available from `apiVersion: 0.0.9` which is defined `subgraph.yaml`. The `getBalance()` retrieves the balance of the specified address as of the end of the block in which the event is triggered.

```typescript
import { ethereum } from '@graphprotocol/graph-ts'

let address = Address.fromString('0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045')
let balance = ethereum.getBalance(address) // returns balance in BigInt
```

#### Check if an Address is a Contract or EOA

To check whether an address is a smart contract address or an externally owned address (EOA), use the `hasCode()` function from the `ethereum` module which will return `boolean`. This feature is available from `apiVersion: 0.0.9` which is defined `subgraph.yaml`.

```typescript
import { ethereum } from '@graphprotocol/graph-ts'

let contractAddr = Address.fromString('0x2E645469f354BB4F5c8a05B3b30A929361cf77eC')
let isContract = ethereum.hasCode(contractAddr).inner // returns true

let eoa = Address.fromString('0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045')
let isContract = ethereum.hasCode(eoa).inner // returns false
```

### Logging API

```typescript
import { log } from '@graphprotocol/graph-ts'
```

The `log` API allows subgraphs to log information to the Graph Node standard output as well as Graph Explorer. Messages can be logged using different log levels. A basic format string syntax is provided to compose log messages from argument.

The `log` API includes the following functions:

- `log.debug(fmt: string, args: Array<string>): void` - logs a debug message.
- `log.info(fmt: string, args: Array<string>): void` - logs an informational message.
- `log.warning(fmt: string, args: Array<string>): void` - logs a warning.
- `log.error(fmt: string, args: Array<string>): void` - logs an error message.
- `log.critical(fmt: string, args: Array<string>): void` – logs a critical message _and_ terminates the subgraph.

The `log` API takes a format string and an array of string values. It then replaces placeholders with the string values from the array. The first `{}` placeholder gets replaced by the first value in the array, the second `{}` placeholder gets replaced by the second value and so on.

```typescript
log.info('Message to be displayed: {}, {}, {}', [value.toString(), anotherValue.toString(), 'already a string'])
```

#### Logging one or more values

##### Logging a single value

In the example below, the string value "A" is passed into an array to become`['A']` before being logged:

```typescript
let myValue = 'A'

export function handleSomeEvent(event: SomeEvent): void {
  // Displays : "My value is: A"
  log.info('My value is: {}', [myValue])
}
```

##### Logging a single entry from an existing array

In the example below, only the first value of the argument array is logged, despite the array containing three values.

```typescript
let myArray = ['A', 'B', 'C']

export function handleSomeEvent(event: SomeEvent): void {
  // Displays : "My value is: A"  (Even though three values are passed to `log.info`)
  log.info('My value is: {}', myArray)
}
```

#### Logging multiple entries from an existing array

Each entry in the arguments array requires its own placeholder `{}` in the log message string. The below example contains three placeholders `{}` in the log message. Because of this, all three values in `myArray` are logged.

```typescript
let myArray = ['A', 'B', 'C']

export function handleSomeEvent(event: SomeEvent): void {
  // Displays : "My first value is: A, second value is: B, third value is: C"
  log.info('My first value is: {}, second value is: {}, third value is: {}', myArray)
}
```

##### Logging a specific entry from an existing array

To display a specific value in the array, the indexed value must be provided.

```typescript
export function handleSomeEvent(event: SomeEvent): void {
  // Displays : "My third value is C"
  log.info('My third value is: {}', [myArray[2]])
}
```

##### Logging event information

The example below logs the block number, block hash and transaction hash from an event:

```typescript
import { log } from '@graphprotocol/graph-ts'

export function handleSomeEvent(event: SomeEvent): void {
  log.debug('Block number: {}, block hash: {}, transaction hash: {}', [
    event.block.number.toString(), // "47596000"
    event.block.hash.toHexString(), // "0x..."
    event.transaction.hash.toHexString(), // "0x..."
  ])
}
```

### IPFS API

```typescript
import { ipfs } from '@graphprotocol/graph-ts'
```

Smart contracts occasionally anchor IPFS files on chain. This allows mappings to obtain the IPFS hashes from the contract and read the corresponding files from IPFS. The file data will be returned as `Bytes`, which usually requires further processing, e.g. with the `json` API documented later on this page.

Given an IPFS hash or path, reading a file from IPFS is done as follows:

```typescript
// Put this inside an event handler in the mapping
let hash = 'QmTkzDwWqPbnAh5YiV5VwcTLnGdwSNsNTn2aDxdXBFca7D'
let data = ipfs.cat(hash)

// Paths like `QmTkzDwWqPbnAh5YiV5VwcTLnGdwSNsNTn2aDxdXBFca7D/Makefile`
// that include files in directories are also supported
let path = 'QmTkzDwWqPbnAh5YiV5VwcTLnGdwSNsNTn2aDxdXBFca7D/Makefile'
let data = ipfs.cat(path)
```

**Note:** `ipfs.cat` is not deterministic at the moment. If the file cannot be retrieved over the IPFS network before the request times out, it will return `null`. Due to this, it's always worth checking the result for `null`.

It is also possible to process larger files in a streaming fashion with `ipfs.map`. The function expects the hash or path for an IPFS file, the name of a callback, and flags to modify its behavior:

```typescript
import { JSONValue, Value } from '@graphprotocol/graph-ts'

export function processItem(value: JSONValue, userData: Value): void {
  // See the JSONValue documentation for details on dealing
  // with JSON values
  let obj = value.toObject()
  let id = obj.get('id')
  let title = obj.get('title')

  if (!id || !title) {
    return
  }

  // Callbacks can also created entities
  let newItem = new Item(id)
  newItem.title = title.toString()
  newitem.parent = userData.toString() // Set parent to "parentId"
  newitem.save()
}

// Put this inside an event handler in the mapping
ipfs.map('Qm...', 'processItem', Value.fromString('parentId'), ['json'])

// Alternatively, use `ipfs.mapJSON`
ipfs.mapJSON('Qm...', 'processItem', Value.fromString('parentId'))
```

The only flag currently supported is `json`, which must be passed to `ipfs.map`. With the `json` flag, the IPFS file must consist of a series of JSON values, one value per line. The call to `ipfs.map` will read each line in the file, deserialize it into a `JSONValue` and call the callback for each of them. The callback can then use entity operations to store data from the `JSONValue`. Entity changes are stored only when the handler that called `ipfs.map` finishes successfully; in the meantime, they are kept in memory, and the size of the file that `ipfs.map` can process is therefore limited.

On success, `ipfs.map` returns `void`. If any invocation of the callback causes an error, the handler that invoked `ipfs.map` is aborted, and the subgraph is marked as failed.

### Crypto API

```typescript
import { crypto } from '@graphprotocol/graph-ts'
```

The `crypto` API makes a cryptographic functions available for use in mappings. Right now, there is only one:

- `crypto.keccak256(input: ByteArray): ByteArray`

### JSON API

```typescript
import { json, JSONValueKind } from '@graphprotocol/graph-ts'
```

JSON data can be parsed using the `json` API:

- `json.fromBytes(data: Bytes): JSONValue` – parses JSON data from a `Bytes` array interpreted as a valid UTF-8 sequence
- `json.try_fromBytes(data: Bytes): Result<JSONValue, boolean>` – safe version of `json.fromBytes`, it returns an error variant if the parsing failed
- `json.fromString(data: string): JSONValue` – parses JSON data from a valid UTF-8 `String`
- `json.try_fromString(data: string): Result<JSONValue, boolean>` – safe version of `json.fromString`, it returns an error variant if the parsing failed

The `JSONValue` class provides a way to pull values out of an arbitrary JSON document. Since JSON values can be booleans, numbers, arrays and more, `JSONValue` comes with a `kind` property to check the type of a value:

```typescript
let value = json.fromBytes(...)
if (value.kind == JSONValueKind.BOOL) {
  ...
}
```

In addition, there is a method to check if the value is `null`:

- `value.isNull(): boolean`

When the type of a value is certain, it can be converted to a [built-in type](#built-in-types) using one of the following methods:

- `value.toBool(): boolean`
- `value.toI64(): i64`
- `value.toF64(): f64`
- `value.toBigInt(): BigInt`
- `value.toString(): string`
- `value.toArray(): Array<JSONValue>` - (and then convert `JSONValue` with one of the 5 methods above)

### Type Conversions Reference

| Source(s)            | Destination          | Conversion function          |
| -------------------- | -------------------- | ---------------------------- |
| Address              | Bytes                | none                         |
| Address              | String               | s.toHexString()              |
| BigDecimal           | String               | s.toString()                 |
| BigInt               | BigDecimal           | s.toBigDecimal()             |
| BigInt               | String (hexadecimal) | s.toHexString() or s.toHex() |
| BigInt               | String (unicode)     | s.toString()                 |
| BigInt               | i32                  | s.toI32()                    |
| Boolean              | Boolean              | none                         |
| Bytes (signed)       | BigInt               | BigInt.fromSignedBytes(s)    |
| Bytes (unsigned)     | BigInt               | BigInt.fromUnsignedBytes(s)  |
| Bytes                | String (hexadecimal) | s.toHexString() or s.toHex() |
| Bytes                | String (unicode)     | s.toString()                 |
| Bytes                | String (base58)      | s.toBase58()                 |
| Bytes                | i32                  | s.toI32()                    |
| Bytes                | u32                  | s.toU32()                    |
| Bytes                | JSON                 | json.fromBytes(s)            |
| int8                 | i32                  | none                         |
| int32                | i32                  | none                         |
| int32                | BigInt               | BigInt.fromI32(s)            |
| uint24               | i32                  | none                         |
| int64 - int256       | BigInt               | none                         |
| uint32 - uint256     | BigInt               | none                         |
| JSON                 | boolean              | s.toBool()                   |
| JSON                 | i64                  | s.toI64()                    |
| JSON                 | u64                  | s.toU64()                    |
| JSON                 | f64                  | s.toF64()                    |
| JSON                 | BigInt               | s.toBigInt()                 |
| JSON                 | string               | s.toString()                 |
| JSON                 | Array                | s.toArray()                  |
| JSON                 | Object               | s.toObject()                 |
| String               | Address              | Address.fromString(s)        |
| Bytes                | Address              | Address.fromBytes(s)         |
| String               | BigInt               | BigInt.fromString(s)         |
| String               | BigDecimal           | BigDecimal.fromString(s)     |
| String (hexadecimal) | Bytes                | ByteArray.fromHexString(s)   |
| String (UTF-8)       | Bytes                | ByteArray.fromUTF8(s)        |

### Data Source Metadata

You can inspect the contract address, network and context of the data source that invoked the handler through the `dataSource` namespace:

- `dataSource.address(): Address`
- `dataSource.network(): string`
- `dataSource.context(): DataSourceContext`

### Entity and DataSourceContext

The base `Entity` class and the child `DataSourceContext` class have helpers to dynamically set and get fields:

- `setString(key: string, value: string): void`
- `setI32(key: string, value: i32): void`
- `setBigInt(key: string, value: BigInt): void`
- `setBytes(key: string, value: Bytes): void`
- `setBoolean(key: string, value: bool): void`
- `setBigDecimal(key, value: BigDecimal): void`
- `getString(key: string): string`
- `getI32(key: string): i32`
- `getBigInt(key: string): BigInt`
- `getBytes(key: string): Bytes`
- `getBoolean(key: string): boolean`
- `getBigDecimal(key: string): BigDecimal`

### DataSourceContext in Manifest

The `context` section within `dataSources` allows you to define key-value pairs that are accessible within your subgraph mappings. The available types are `Bool`, `String`, `Int`, `Int8`, `BigDecimal`, `Bytes`, `List`, and `BigInt`.

Here is a YAML example illustrating the usage of various types in the `context` section:

```yaml
dataSources:
  - kind: ethereum/contract
    name: ContractName
    network: mainnet
    context:
      bool_example:
        type: Bool
        data: true
      string_example:
        type: String
        data: 'hello'
      int_example:
        type: Int
        data: 42
      int8_example:
        type: Int8
        data: 127
      big_decimal_example:
        type: BigDecimal
        data: '10.99'
      bytes_example:
        type: Bytes
        data: '0x68656c6c6f'
      list_example:
        type: List
        data:
          - type: Int
            data: 1
          - type: Int
            data: 2
          - type: Int
            data: 3
      big_int_example:
        type: BigInt
        data: '1000000000000000000000000'
```

- `Bool`: Specifies a Boolean value (`true` or `false`).
- `String`: Specifies a String value.
- `Int`: Specifies a 32-bit integer.
- `Int8`: Specifies an 8-bit integer.
- `BigDecimal`: Specifies a decimal number. Must be quoted.
- `Bytes`: Specifies a hexadecimal string.
- `List`: Specifies a list of items. Each item needs to specify its type and data.
- `BigInt`: Specifies a large integer value. Must be quoted due to its large size.

This context is then accessible in your subgraph mapping files, enabling more dynamic and configurable subgraphs.
---
title: Developer FAQs
---

This page summarizes some of the most common questions for developers building on The Graph.

## Subgraph Related

### 1. What is a subgraph?

A subgraph is a custom API built on blockchain data. Subgraphs are queried using the GraphQL query language and are deployed to a Graph Node using The Graph CLI. Once deployed and published to The Graph's decentralized network, Indexers process subgraphs and make them available for subgraph consumers to query.

### 2. What is the first step to create a subgraph?

To successfully create a subgraph, you will need to install The Graph CLI. Review the [Quick Start](/quick-start/) to get started. For detailed information, see [Creating a Subgraph](/developing/creating-a-subgraph/).

### 3. Can I still create a subgraph if my smart contracts don't have events?

It is highly recommended that you structure your smart contracts to have events associated with data you are interested in querying. Event handlers in the subgraph are triggered by contract events and are the fastest way to retrieve useful data.

If the contracts you work with do not contain events, your subgraph can use call and block handlers to trigger indexing. However, this is not recommended, as performance will be significantly slower.

### 4. Can I change the GitHub account associated with my subgraph?

No. Once a subgraph is created, the associated GitHub account cannot be changed. Please make sure to carefully consider this before creating your subgraph.

### 5. How do I update a subgraph on mainnet?

You can deploy a new version of your subgraph to Subgraph Studio using the CLI. This action maintains your subgraph private, but once you’re happy with it, you can publish to Graph Explorer. This will create a new version of your subgraph that Curators can start signaling on.

### 6. Is it possible to duplicate a subgraph to another account or endpoint without redeploying?

You have to redeploy the subgraph, but if the subgraph ID (IPFS hash) doesn't change, it won't have to sync from the beginning.

### 7. How do I call a contract function or access a public state variable from my subgraph mappings?

Take a look at `Access to smart contract` state inside the section [AssemblyScript API](/developing/graph-ts/api/#access-to-smart-contract-state).

### 8. Can I import `ethers.js` or other JS libraries into my subgraph mappings?

Not currently, as mappings are written in AssemblyScript.

One possible alternative solution to this is to store raw data in entities and perform logic that requires JS libraries on the client.

### 9. When listening to multiple contracts, is it possible to select the contract order to listen to events?

Within a subgraph, the events are always processed in the order they appear in the blocks, regardless of whether that is across multiple contracts or not.

### 10. How are templates different from data sources?

Templates allow you to create data sources quickly, while your subgraph is indexing. Your contract might spawn new contracts as people interact with it. Since you know the shape of those contracts (ABI, events, etc.) upfront, you can define how you want to index them in a template. When they are spawned, your subgraph will create a dynamic data source by supplying the contract address.

Check out the "Instantiating a data source template" section on: [Data Source Templates](/developing/creating-a-subgraph#data-source-templates).

### 11. Is it possible to set up a subgraph using `graph init` from `graph-cli` with two contracts? Or should I manually add another dataSource in `subgraph.yaml` after running `graph init`?

Yes. On `graph init` command itself you can add multiple dataSources by entering contracts one after the other.

You can also use `graph add` command to add a new dataSource.

### 12. In what order are the event, block, and call handlers triggered for a data source?

Event and call handlers are first ordered by transaction index within the block. Event and call handlers within the same transaction are ordered using a convention: event handlers first then call handlers, each type respecting the order they are defined in the manifest. Block handlers are run after event and call handlers, in the order they are defined in the manifest. Also these ordering rules are subject to change.

When new dynamic data source are created, the handlers defined for dynamic data sources will only start processing after all existing data source handlers are processed, and will repeat in the same sequence whenever triggered.

### 13. How do I make sure I'm using the latest version of graph-node for my local deployments?

You can run the following command:

```sh
docker pull graphprotocol/graph-node:latest
```

> Note: docker / docker-compose will always use whatever graph-node version was pulled the first time you ran it, so make sure you're up to date with the latest version of graph-node.

### 14. What is the recommended way to build "autogenerated" ids for an entity when handling events?

If only one entity is created during the event and if there's nothing better available, then the transaction hash + log index would be unique. You can obfuscate these by converting that to Bytes and then piping it through `crypto.keccak256` but this won't make it more unique.

### 15. Can I delete my subgraph?

It is not possible to delete subgraphs once they are created. However, you can [transfer and deprecate your subgraph](/managing/transfer-and-deprecate-a-subgraph/).

## Network Related

### 16. What networks are supported by The Graph?

You can find the list of the supported networks [here](/developing/supported-networks).

### 17. Is it possible to differentiate between networks (mainnet, Sepolia, local) within event handlers?

Yes. You can do this by importing `graph-ts` as per the example below:

```javascript
import { dataSource } from '@graphprotocol/graph-ts'

dataSource.network()
dataSource.address()
```

### 18. Do you support block and call handlers on Sepolia?

Yes. Sepolia supports block handlers, call handlers and event handlers. It should be noted that event handlers are far more performant than the other two handlers, and they are supported on every EVM-compatible network.

## Indexing & Querying Related

### 19. Is it possible to specify what block to start indexing on?

Yes. `dataSources.source.startBlock` in the `subgraph.yaml` file specifies the number of the block that the dataSource starts indexing from. In most cases, we suggest using the block where the contract was created: [Start blocks](/developing/creating-a-subgraph#start-blocks)

### 20. What are some tips to increase the performance of indexing? My subgraph is taking a very long time to sync

Yes, you should take a look at the optional start block feature to start indexing from the block where the contract was deployed: [Start blocks](/developing/creating-a-subgraph#start-blocks)

### 21. Is there a way to query the subgraph directly to determine the latest block number it has indexed?

Yes! Try the following command, substituting "organization/subgraphName" with the organization under it is published and the name of your subgraph:

```sh
curl -X POST -d '{ "query": "{indexingStatusForCurrentVersion(subgraphName: \"organization/subgraphName\") { chains { latestBlock { hash number }}}}"}' https://api.thegraph.com/index-node/graphql
```

### 22. Is there a limit to how many objects The Graph can return per query?

By default, query responses are limited to 100 items per collection. If you want to receive more, you can go up to 1000 items per collection and beyond that, you can paginate with:

```graphql
someCollection(first: 1000, skip: <number>) { ... }
```

### 23. If my dapp frontend uses The Graph for querying, do I need to write my query key into the frontend directly? What if we pay query fees for users – will malicious users cause our query fees to be very high?

Currently, the recommended approach for a dapp is to add the key to the frontend and expose it to end users. That said, you can limit that key to a hostname, like _yourdapp.io_ and subgraph. The gateway is currently being run by Edge & Node. Part of the responsibility of a gateway is to monitor for abusive behavior and block traffic from malicious clients.

## Miscellaneous

### 24. Is it possible to use Apollo Federation on top of graph-node?

Federation is not supported yet. At the moment, you can use schema stitching, either on the client or via a proxy service.

### 25. I want to contribute or add a GitHub issue. Where can I find the open source repositories?

- [graph-node](https://github.com/graphprotocol/graph-node)
- [graph-tooling](https://github.com/graphprotocol/graph-tooling)
- [graph-docs](https://github.com/graphprotocol/docs)
- [graph-client](https://github.com/graphprotocol/graph-client)
---
title: Quick Start
---

Learn how to easily publish and query a [subgraph](/developing/developer-faqs/#1-what-is-a-subgraph) on The Graph.

## Prerequisites for this guide

- A crypto wallet
- A smart contract address on one of the [supported networks](/developing/supported-networks/)

## Step-by-step

### 1. Install the Graph CLI

You must have [Node.js](https://nodejs.org/) and a package manager of your choice (`npm`, `yarn` or `pnpm`) installed to use the Graph CLI. Check for the [most recent](https://github.com/graphprotocol/graph-tooling/releases?q=%40graphprotocol%2Fgraph-cli&expanded=true) CLI version.

On your local machine, run one of the following commands:

Using [npm](https://www.npmjs.com/):

```sh
npm install -g @graphprotocol/graph-cli@latest
```

Using [yarn](https://yarnpkg.com/):

```sh
yarn global add @graphprotocol/graph-cli
```

### 2. Create your subgraph

If your contract has events, the `init` command will automatically create a scaffold of a subgraph.

#### Create via Graph CLI

Use the following command to create a subgraph in Subgraph Studio using the CLI:

```sh
graph init --product subgraph-studio
```

#### Create via Subgraph Studio

Subgraph Studio lets you create, manage, deploy, and publish subgraphs, as well as create and manage API keys.

1.  Go to [Subgraph Studio](https://thegraph.com/studio/) and connect your wallet.
2.  Click "Create a Subgraph". It is recommended to name the subgraph in Title Case: "Subgraph Name Chain Name".

For additional information on subgraph creation and the Graph CLI, see [Creating a Subgraph](/developing/creating-a-subgraph).

### 3. Initialize your subgraph

#### From an existing contract

The following command initializes your subgraph from an existing contract:

```sh
graph init --studio <SUBGRAPH_SLUG>
```

> Note: If your contract was verified on Etherscan, then the ABI will automatically be created in the CLI.

You can find commands for your specific subgraph on the subgraph page in [Subgraph Studio](https://thegraph.com/studio/).

When you initialize your subgraph, the CLI will ask you for the following information:

- Protocol: Choose the protocol your subgraph will be indexing data from.
- Subgraph slug: Create a name for your subgraph. Your subgraph slug is an identifier for your subgraph.
- Directory to create the subgraph in: Choose your local directory.
- Ethereum network (optional): You may need to specify which EVM-compatible network your subgraph will be indexing data from.
- Contract address: Locate the smart contract address you’d like to query data from.
- ABI: If the ABI is not auto-populated, you will need to input it manually as a JSON file.
- Start Block: You should input the start block to optimize subgraph indexing of blockchain data. Locate the start block by finding the block where your contract was deployed.
- Contract Name: Input the name of your contract.
- Index contract events as entities: It is suggested that you set this to true, as it will automatically add mappings to your subgraph for every emitted event.
- Add another contract (optional): You can add another contract.

See the following screenshot for an example for what to expect when initializing your subgraph:

![Subgraph command](/img/subgraph-init-example.png)

### 4. Write your subgraph

The `init` command in the previous step creates a scaffold subgraph that you can use as a starting point to build your subgraph.

When making changes to the subgraph, you will mainly work with three files:

- Manifest (`subgraph.yaml`) - defines what data sources your subgraph will index.
- Schema (`schema.graphql`) - defines what data you wish to retrieve from the subgraph.
- AssemblyScript Mappings (`mapping.ts`) - translates data from your data sources to the entities defined in the schema.

For a detailed breakdown on how to write your subgraph, check out [Creating a Subgraph](/developing/creating-a-subgraph/).

### 5. Deploy your subgraph

Remember, deploying is not the same as publishing.

- When you deploy a subgraph, you push it to [Subgraph Studio](https://thegraph.com/studio/), where you can test, stage and review it.
- When you publish a subgraph, you are publishing it onchain to the decentralized network.

1.  Once your subgraph is written, run the following commands:

    ```sh
    graph codegen
    graph build
    ```

2.  Authenticate and deploy your subgraph. The deploy key can be found on the subgraph's page in Subgraph Studio.

![Deploy key](/img/subgraph-studio-deploy-key.jpg)

    ```sh

    graph auth --studio <DEPLOY_KEY>

    graph deploy --studio <SUBGRAPH_SLUG>
    ```

- The CLI will ask for a version label.
  - It's strongly recommended to use [semantic versioning](https://semver.org/), e.g. `0.0.1`. That said, you can choose any string for the version such as: `v1`, `version1`, `asdf`, etc.

### 6. Review your subgraph

If you’d like to examine your subgraph before publishing it to the network, you can use [Subgraph Studio](https://thegraph.com/studio/) to do the following:

- Run a sample query.
- Analyze your subgraph in the dashboard to check information.
- Check the logs on the dashboard to see if there are any errors with your subgraph. The logs of an operational subgraph will look like this:

  ![Subgraph logs](/img/subgraph-logs-image.png)

### 7. Publish your subgraph to The Graph Network

Publishing a subgraph to the decentralized network makes it available for [Curators](/network/curating/) to begin curating it and [Indexers](/network/indexing/) to begin indexing it.

#### Publishing with Subgraph Studio

1.  To publish your subgraph, click the Publish button in the dashboard.
2.  Select the network to which you would like to publish your subgraph.

#### Publishing from the CLI

As of version 0.73.0, you can also publish your subgraph with the Graph CLI.

1.  Open the `graph-cli`.
2.  Use the following commands:

    ```sh
    graph codegen && graph build
    ```

    Then,

    ```sh
    graph publish
    ```

3.  A window will open, allowing you to connect your wallet, add metadata, and deploy your finalized subgraph to a network of your choice.

![cli-ui](/img/cli-ui.png)

To customize your deployment, see [Publishing a Subgraph](/publishing/publishing-a-subgraph/).

#### Adding signal to your subgraph

1.  To attract indexers to query your subgraph, you should add GRT curation signal to it.

    - This action improves quality of service, reduces latency, and enhances network redundancy and availability for your subgraph.

2.  If eligible for indexing rewards, Indexers receive GRT rewards based on the signaled amount.

    - It’s recommended to curate at least 3,000 GRT to attract 3 Indexers. Check reward eligibility based on subgraph feature usage and supported networks.

To learn more about curation, read [Curating](/network/curating/).

To save on gas costs, you can curate your subgraph in the same transaction you publish it by selecting this option:

![Subgraph publish](/img/publish-and-signal-tx.png)

### 8. Query your subgraph

Now, you can query your subgraph by sending GraphQL queries to its Query URL, which you can find by clicking the Query button.

For more information about querying data from your subgraph, read [Querying The Graph](/querying/querying-the-graph/).
---
title: L2 Transfer Tools Guide
---

The Graph has made it easy to move to L2 on Arbitrum One. For each protocol participant, there are a set of L2 Transfer Tools to make transferring to L2 seamless for all network participants. These tools will require you to follow a specific set of steps depending on what you are transferring.

Some frequent questions about these tools are answered in the [L2 Transfer Tools FAQ](/arbitrum/l2-transfer-tools-faq). The FAQs contain in-depth explanations of how to use the tools, how they work, and things to keep in mind when using them.

## How to transfer your subgraph to Arbitrum (L2)

<VideoEmbed youtube="R8_vz4lx2Co" />

## Benefits of transferring your subgraphs

The Graph's community and core devs have [been preparing](https://forum.thegraph.com/t/gip-0031-arbitrum-grt-bridge/3305) to move to Arbitrum over the past year. Arbitrum, a layer 2 or "L2" blockchain, inherits the security from Ethereum but provides drastically lower gas fees.

When you publish or upgrade your subgraph to The Graph Network, you're interacting with smart contracts on the protocol and this requires paying for gas using ETH. By moving your subgraphs to Arbitrum, any future updates to your subgraph will require much lower gas fees. The lower fees, and the fact that curation bonding curves on L2 are flat, also make it easier for other Curators to curate on your subgraph, increasing the rewards for Indexers on your subgraph. This lower-cost environment also makes it cheaper for Indexers to index and serve your subgraph. Indexing rewards will be increasing on Arbitrum and decreasing on Ethereum mainnet over the coming months, so more and more Indexers will be transferring their stake and setting up their operations on L2.

## Understanding what happens with signal, your L1 subgraph and query URLs

Transferring a subgraph to Arbitrum uses the Arbitrum GRT bridge, which in turn uses the native Arbitrum bridge, to send the subgraph to L2. The "transfer" will deprecate the subgraph on mainnet and send the information to re-create the subgraph on L2 using the bridge. It will also include the subgraph owner's signaled GRT, which must be more than zero for the bridge to accept the transfer.

When you choose to transfer the subgraph, this will convert all of the subgraph's curation signal to GRT. This is equivalent to "deprecating" the subgraph on mainnet. The GRT corresponding to your curation will be sent to L2 together with the subgraph, where they will be used to mint signal on your behalf.

Other Curators can choose whether to withdraw their fraction of GRT, or also transfer it to L2 to mint signal on the same subgraph. If a subgraph owner does not transfer their subgraph to L2 and manually deprecates it via a contract call, then Curators will be notified and will be able to withdraw their curation.

As soon as the subgraph is transferred, since all curation is converted to GRT, Indexers will no longer receive rewards for indexing the subgraph. However, there will be Indexers that will 1) keep serving transferred subgraphs for 24 hours, and 2) immediately start indexing the subgraph on L2. Since these Indexers already have the subgraph indexed, there should be no need to wait for the subgraph to sync, and it will be possible to query the L2 subgraph almost immediately.

Queries to the L2 subgraph will need to be done to a different URL (on `arbitrum-gateway.thegraph.com`), but the L1 URL will continue working for at least 48 hours. After that, the L1 gateway will forward queries to the L2 gateway (for some time), but this will add latency so it is recommended to switch all your queries to the new URL as soon as possible.

## Choosing your L2 wallet

When you published your subgraph on mainnet, you used a connected wallet to create the subgraph, and this wallet owns the NFT that represents this subgraph and allows you to publish updates.

When transferring the subgraph to Arbitrum, you can choose a different wallet that will own this subgraph NFT on L2.

If you're using a "regular" wallet like MetaMask (an Externally Owned Account or EOA, i.e. a wallet that is not a smart contract), then this is optional and it is recommended to keep the same owner address as in L1.

If you're using a smart contract wallet, like a multisig (e.g. a Safe), then choosing a different L2 wallet address is mandatory, as it is most likely that this account only exists on mainnet and you will not be able to make transactions on Arbitrum using this wallet. If you want to keep using a smart contract wallet or multisig, create a new wallet on Arbitrum and use its address as the L2 owner of your subgraph.

**It is very important to use a wallet address that you control, and that can make transactions on Arbitrum. Otherwise, the subgraph will be lost and cannot be recovered.**

## Preparing for the transfer: bridging some ETH

Transferring the subgraph involves sending a transaction through the bridge, and then executing another transaction on Arbitrum. The first transaction uses ETH on mainnet, and includes some ETH to pay for gas when the message is received on L2. However, if this gas is insufficient, you will have to retry the transaction and pay for the gas directly on L2 (this is "Step 3: Confirming the transfer" below). This step **must be executed within 7 days of starting the transfer**. Moreover, the second transaction ("Step 4: Finishing the transfer on L2") will be done directly on Arbitrum. For these reasons, you will need some ETH on an Arbitrum wallet. If you're using a multisig or smart contract account, the ETH will need to be in the regular (EOA) wallet that you are using to execute the transactions, not on the multisig wallet itself.

You can buy ETH on some exchanges and withdraw it directly to Arbitrum, or you can use the Arbitrum bridge to send ETH from a mainnet wallet to L2: [bridge.arbitrum.io](http://bridge.arbitrum.io). Since gas fees on Arbitrum are lower, you should only need a small amount. It is recommended that you start at a low threshold (0.e.g. 01 ETH) for your transaction to be approved.

## Finding the subgraph Transfer Tool

You can find the L2 Transfer Tool when you're looking at your subgraph's page on Subgraph Studio:

![transfer tool](/img/L2-transfer-tool1.png)

It is also available on Explorer if you're connected with the wallet that owns a subgraph and on that subgraph's page on Explorer:

![Transferring to L2](/img/transferToL2.png)

Clicking on the Transfer to L2 button will open the transfer tool where you can start the transfer process.

## Step 1: Starting the transfer

Before starting the transfer, you must decide which address will own the subgraph on L2 (see "Choosing your L2 wallet" above), and it is strongly recommend having some ETH for gas already bridged on Arbitrum (see "Preparing for the transfer: bridging some ETH" above).

Also please note transferring the subgraph requires having a nonzero amount of signal on the subgraph with the same account that owns the subgraph; if you haven't signaled on the subgraph you will have to add a bit of curation (adding a small amount like 1 GRT would suffice).

After opening the Transfer Tool, you will be able to input the L2 wallet address into the "Receiving wallet address" field - **make sure you've entered the correct address here**. Clicking on Transfer Subgraph will prompt you to execute the transaction on your wallet (note some ETH value is included to pay for L2 gas); this will initiate the transfer and deprecate your L1 subgraph (see "Understanding what happens with signal, your L1 subgraph and query URLs" above for more details on what goes on behind the scenes).

If you execute this step, **make sure you proceed until completing step 3 in less than 7 days, or the subgraph and your signal GRT will be lost.** This is due to how L1-L2 messaging works on Arbitrum: messages that are sent through the bridge are "retry-able tickets" that must be executed within 7 days, and the initial execution might need a retry if there are spikes in the gas price on Arbitrum.

![Start the transfer to L2](/img/startTransferL2.png)

## Step 2: Waiting for the subgraph to get to L2

After you start the transfer, the message that sends your L1 subgraph to L2 must propagate through the Arbitrum bridge. This takes approximately 20 minutes (the bridge waits for the mainnet block containing the transaction to be "safe" from potential chain reorgs).

Once this wait time is over, Arbitrum will attempt to auto-execute the transfer on the L2 contracts.

![Wait screen](/img/screenshotOfWaitScreenL2.png)

## Step 3: Confirming the transfer

In most cases, this step will auto-execute as the L2 gas included in step 1 should be sufficient to execute the transaction that receives the subgraph on the Arbitrum contracts. In some cases, however, it is possible that a spike in gas prices on Arbitrum causes this auto-execution to fail. In this case, the "ticket" that sends your subgraph to L2 will be pending and require a retry within 7 days.

If this is the case, you will need to connect using an L2 wallet that has some ETH on Arbitrum, switch your wallet network to Arbitrum, and click on "Confirm Transfer" to retry the transaction.

![Confirm the transfer to L2](/img/confirmTransferToL2.png)

## Step 4: Finishing the transfer on L2

At this point, your subgraph and GRT have been received on Arbitrum, but the subgraph is not published yet. You will need to connect using the L2 wallet that you chose as the receiving wallet, switch your wallet network to Arbitrum, and click "Publish Subgraph."

![Publish the subgraph](/img/publishSubgraphL2TransferTools.png)

![Wait for the subgraph to be published](/img/waitForSubgraphToPublishL2TransferTools.png)

This will publish the subgraph so that Indexers that are operating on Arbitrum can start serving it. It will also mint curation signal using the GRT that were transferred from L1.

## Step 5: Updating the query URL

Your subgraph has been successfully transferred to Arbitrum! To query the subgraph, the new URL will be :

`https://arbitrum-gateway.thegraph.com/api/[api-key]/subgraphs/id/[l2-subgraph-id]`

Note that the subgraph ID on Arbitrum will be a different than the one you had on mainnet, but you can always find it on Explorer or Studio. As mentioned above (see "Understanding what happens with signal, your L1 subgraph and query URLs") the old L1 URL will be supported for a short while, but you should switch your queries to the new address as soon as the subgraph has been synced on L2.

## How to transfer your curation to Arbitrum (L2)

## Understanding what happens to curation on subgraph transfers to L2

When the owner of a subgraph transfers a subgraph to Arbitrum, all of the subgraph's signal is converted to GRT at the same time. This applies to "auto-migrated" signal, i.e. signal that is not specific to a subgraph version or deployment but that follows the latest version of a subgraph.

This conversion from signal to GRT is the same as what would happen if the subgraph owner deprecated the subgraph in L1. When the subgraph is deprecated or transferred, all curation signal is "burned" simultaneously (using the curation bonding curve) and the resulting GRT is held by the GNS smart contract (that is the contract that handles subgraph upgrades and auto-migrated signal). Each Curator on that subgraph therefore has a claim to that GRT proportional to the amount of shares they had for the subgraph.

A fraction of these GRT corresponding to the subgraph owner is sent to L2 together with the subgraph.

At this point, the curated GRT will not accrue any more query fees, so Curators can choose to withdraw their GRT or transfer it to the same subgraph on L2, where it can be used to mint new curation signal. There is no rush to do this as the GRT can be help indefinitely and everybody gets an amount proportional to their shares, irrespective of when they do it.

## Choosing your L2 wallet

If you decide to transfer your curated GRT to L2, you can choose a different wallet that will own the curation signal on L2.

If you're using a "regular" wallet like Metamask (an Externally Owned Account or EOA, i.e. a wallet that is not a smart contract), then this is optional and it is recommended to keep the same Curator address as in L1.

If you're using a smart contract wallet, like a multisig (e.g. a Safe), then choosing a different L2 wallet address is mandatory, as it is most likely that this account only exists on mainnet and you will not be able to make transactions on Arbitrum using this wallet. If you want to keep using a smart contract wallet or multisig, create a new wallet on Arbitrum and use its address as the L2 receiving wallet address.

**It is very important to use a wallet address that you control, and that can make transactions on Arbitrum, as otherwise the curation will be lost and cannot be recovered.**

## Sending curation to L2: Step 1

Before starting the transfer, you must decide which address will own the curation on L2 (see "Choosing your L2 wallet" above), and it is recommended having some ETH for gas already bridged on Arbitrum in case you need to retry the execution of the message on L2. You can buy ETH on some exchanges and withdraw it directly to Arbitrum, or you can use the Arbitrum bridge to send ETH from a mainnet wallet to L2: [bridge.arbitrum.io](http://bridge.arbitrum.io) - since gas fees on Arbitrum are so low, you should only need a small amount, e.g. 0.01 ETH will probably be more than enough.

If a subgraph that you curate to has been transferred to L2, you will see a message on Explorer telling you that you're curating to a transferred subgraph.

When looking at the subgraph page, you can choose to withdraw or transfer the curation. Clicking on "Transfer Signal to Arbitrum" will open the transfer tool.

![Transfer signal](/img/transferSignalL2TransferTools.png)

After opening the Transfer Tool, you may be prompted to add some ETH to your wallet if you don't have any. Then you will be able to input the L2 wallet address into the "Receiving wallet address" field - **make sure you've entered the correct address here**. Clicking on Transfer Signal will prompt you to execute the transaction on your wallet (note some ETH value is included to pay for L2 gas); this will initiate the transfer.

If you execute this step, **make sure you proceed until completing step 3 in less than 7 days, or your signal GRT will be lost.** This is due to how L1-L2 messaging works on Arbitrum: messages that are sent through the bridge are "retryable tickets" that must be executed within 7 days, and the initial execution might need a retry if there are spikes in the gas price on Arbitrum.

## Sending curation to L2: step 2

Starting the transfer:

![Send signal to L2](/img/sendingCurationToL2Step2First.png)

After you start the transfer, the message that sends your L1 curation to L2 must propagate through the Arbitrum bridge. This takes approximately 20 minutes (the bridge waits for the mainnet block containing the transaction to be "safe" from potential chain reorgs).

Once this wait time is over, Arbitrum will attempt to auto-execute the transfer on the L2 contracts.

![Sending curation signal to L2](/img/sendingCurationToL2Step2Second.png)

## Sending curation to L2: step 3

In most cases, this step will auto-execute as the L2 gas included in step 1 should be sufficient to execute the transaction that receives the curation on the Arbitrum contracts. In some cases, however, it is possible that a spike in gas prices on Arbitrum causes this auto-execution to fail. In this case, the "ticket" that sends your curation to L2 will be pending and require a retry within 7 days.

If this is the case, you will need to connect using an L2 wallet that has some ETH on Arbitrum, switch your wallet network to Arbitrum, and click on "Confirm Transfer" to retry the transaction.

![Send signal to L2](/img/L2TransferToolsFinalCurationImage.png)

## Withdrawing your curation on L1

If you prefer not to send your GRT to L2, or you'd rather bridge the GRT manually, you can withdraw your curated GRT on L1. On the banner on the subgraph page, choose "Withdraw Signal" and confirm the transaction; the GRT will be sent to your Curator address.
---
title: L2 Transfer Tools FAQ
---

## General

### What are L2 Transfer Tools?

The Graph has made it 26x cheaper for contributors to participate in the network by deploying the protocol to Arbitrum One. The L2 Transfer Tools were created by core devs to make it easy to move to L2.

For each network participant, a set of L2 Transfer Tools are available to make the experience seamless when moving to L2, avoiding thawing periods or having to manually withdraw and bridge GRT.

These tools will require you to follow a specific set of steps depending on what your role is within The Graph and what you are transferring to L2.

### Can I use the same wallet I use on Ethereum mainnet?

If you are using an [EOA](https://ethereum.org/en/developers/docs/accounts/#types-of-account) wallet you can use the same address. If your Ethereum mainnet wallet is a contract (e.g. a multisig) then you must specify an [Arbitrum wallet address](/arbitrum/arbitrum-faq/#what-do-i-need-to-do-to-use-the-graph-on-l2) where your transfer will be sent. Please check the address carefully as any transfers to an incorrect address can result in permanent loss. If you'd like to use a multisig on L2, make sure you deploy a multisig contract on Arbitrum One.

Wallets on EVM blockchains like Ethereum and Arbitrum are a pair of keys (public and private), that you create without any need to interact with the blockchain. So any wallet that was created for Ethereum will also work on Arbitrum without having to do anything else.

The exception is with smart contract wallets like multisigs: these are smart contracts that are deployed separately on each chain, and get their address when they are deployed. If a multisig was deployed to Ethereum, it won't exist with the same address on Arbitrum. A new multisig must be created first on Arbitrum, and may get a different address.

### What happens if I don’t finish my transfer in 7 days?

The L2 Transfer Tools use Arbitrum’s native mechanism to send messages from L1 to L2. This mechanism is called a “retryable ticket” and is used by all native token bridges, including the Arbitrum GRT bridge. You can read more about retryable tickets in the [Arbitrum docs](https://docs.arbitrum.io/arbos/l1-to-l2-messaging).

When you transfer your assets (subgraph, stake, delegation or curation) to L2, a message is sent through the Arbitrum GRT bridge which creates a retryable ticket in L2. The transfer tool includes some ETH value in the transaction, that is used to 1) pay to create the ticket and 2) pay for the gas to execute the ticket in L2. However, because gas prices might vary in the time until the ticket is ready to execute in L2, it is possible that this auto-execution attempt fails. When that happens, the Arbitrum bridge will keep the retryable ticket alive for up to 7 days, and anyone can retry “redeeming” the ticket (which requires a wallet with some ETH bridged to Arbitrum).

This is what we call the “Confirm” step in all the transfer tools - it will run automatically in most cases, as the auto-execution is most often successful, but it is important that you check back to make sure it went through. If it doesn’t succeed and there are no successful retries in 7 days, the Arbitrum bridge will discard the ticket, and your assets (subgraph, stake, delegation or curation) will be lost and can’t be recovered. The Graph core devs have a monitoring system in place to detect these situations and try to redeem the tickets before it’s too late, but it is ultimately your responsibility to ensure your transfer is completed in time. If you’re having trouble confirming your transaction, please reach out using [this form](https://noteforms.com/forms/notionform-l2-transfer-tooling-issues-0ogqfu?notionforms=1&utm_source=notionforms) and core devs will be there help you.

### I started my delegation/stake/curation transfer and I'm not sure if it made it through to L2, how can I confirm that it was transferred correctly?

If you don't see a banner on your profile asking you to finish the transfer, then it's likely the transaction made it safely to L2 and no more action is needed. If in doubt, you can check if Explorer shows your delegation, stake or curation on Arbitrum One.

If you have the L1 transaction hash (which you can find by looking at the recent transactions in your wallet), you can also confirm if the "retryable ticket" that carried the message to L2 was redeemed here: https://retryable-dashboard.arbitrum.io/ - if the auto-redeem failed, you can also connect your wallet there and redeem it. Rest assured that core devs are also monitoring for messages that get stuck, and will attempt to redeem them before they expire.

## Subgraph Transfer

### How do I transfer my subgraph?

<VideoEmbed youtube="R8_vz4lx2Co" />

To transfer your subgraph, you will need to complete the following steps:

1.  Initiate the transfer on Ethereum mainnet

2.  Wait 20 minutes for confirmation

3.  Confirm subgraph transfer on Arbitrum\*

4.  Finish publishing subgraph on Arbitrum

5.  Update Query URL (recommended)

\*Note that you must confirm the transfer within 7 days otherwise your subgraph may be lost. In most cases, this step will run automatically, but a manual confirmation may be needed if there is a gas price spike on Arbitrum. If there are any issues during this process, there will be resources to help: contact support at support@thegraph.com or on [Discord](https://discord.gg/graphprotocol).

### Where should I initiate my transfer from?

You can initiate your transfer from the [Subgraph Studio](https://thegraph.com/studio/), [Explorer,](https://thegraph.com/explorer) or any subgraph details page. Click the "Transfer Subgraph" button in the subgraph details page to start the transfer.

### How long do I need to wait until my subgraph is transferred

The transfer time takes approximately 20 minutes. The Arbitrum bridge is working in the background to complete the bridge transfer automatically. In some cases, gas costs may spike and you will need to confirm the transaction again.

### Will my subgraph still be discoverable after I transfer it to L2?

Your subgraph will only be discoverable on the network it is published to. For example, if your subgraph is on Arbitrum One, then you can only find it in Explorer on Arbitrum One and will not be able to find it on Ethereum. Please ensure that you have Arbitrum One selected in the network switcher at the top of the page to ensure you are on the correct network.  After the transfer, the L1 subgraph will appear as deprecated.

### Does my subgraph need to be published to transfer it?

To take advantage of the subgraph transfer tool, your subgraph must be already published to Ethereum mainnet and must have some curation signal owned by the wallet that owns the subgraph. If your subgraph is not published, it is recommended you simply publish directly on Arbitrum One - the associated gas fees will be considerably lower. If you want to transfer a published subgraph but the owner account hasn't curated any signal on it, you can signal a small amount (e.g. 1 GRT) from that account; make sure to choose "auto-migrating" signal.

### What happens to the Ethereum mainnet version of my subgraph after I transfer to Arbitrum?

After transferring your subgraph to Arbitrum, the Ethereum mainnet version will be deprecated. We recommend you update your query URL within 48 hours. However, there is a grace period in place that keeps your mainnet URL functioning so that any third-party dapp support can be updated.

### After I transfer, do I also need to re-publish on Arbitrum?

After the 20 minute transfer window, you will need to confirm the transfer with a transaction in the UI to finish the transfer, but the transfer tool will guide you through this. Your L1 endpoint will continue to be supported during the transfer window and a grace period after. It is encouraged that you update your endpoint when convenient for you.

### Will my endpoint experience downtime while re-publishing?

It is unlikely, but possible to experience a brief downtime depending on which Indexers are supporting the subgraph on L1 and whether they keep indexing it until the subgraph is fully supported on L2.

### Is publishing and versioning the same on L2 as Ethereum Ethereum mainnet?

Yes. Select Arbitrum One as your published network when publishing in Subgraph Studio. In the Studio, the latest endpoint will be available which points to the latest updated version of the subgraph.

### Will my subgraph's curation move with my subgraph?

If you've chosen auto-migrating signal, 100% of your own curation will move with your subgraph to Arbitrum One. All of the subgraph's curation signal will be converted to GRT at the time of the transfer, and the GRT corresponding to your curation signal will be used to mint signal on the L2 subgraph.

Other Curators can choose whether to withdraw their fraction of GRT, or also transfer it to L2 to mint signal on the same subgraph.

### Can I move my subgraph back to Ethereum mainnet after I transfer?

Once transferred, your Ethereum mainnet version of this subgraph will be deprecated. If you would like to move back to mainnet, you will need to redeploy and publish back to mainnet. However, transferring back to Ethereum mainnet is strongly discouraged as indexing rewards will eventually be distributed entirely on Arbitrum One.

### Why do I need bridged ETH to complete my transfer?

Gas fees on Arbitrum One are paid using bridged ETH (i.e. ETH that has been bridged to Arbitrum One). However, the gas fees are significantly lower when compared to Ethereum mainnet.

## Delegation

### How do I transfer my delegation?

<VideoEmbed youtube="CAAQCKw5eV4" />

To transfer your delegation, you will need to complete the following steps:

1. Initiate delegation transfer on Ethereum mainnet
2. Wait 20 minutes for confirmation
3. Confirm delegation transfer on Arbitrum

\*\*\*\*You must confirm the transaction to complete the delegation transfer on Arbitrum. This step must be completed within 7 days or the delegation could be lost. In most cases, this step will run automatically, but a manual confirmation may be needed if there is a gas price spike on Arbitrum. If there are any issues during this process, there will be resources to help: contact support at support@thegraph.com or on [Discord](https://discord.gg/graphprotocol).

### What happens to my rewards if I initiate a transfer with an open allocation on Ethereum mainnet?

If the Indexer to whom you're delegating is still operating on L1, when you transfer to Arbitrum you will forfeit any delegation rewards from open allocations on Ethereum mainnet. This means that you will lose the rewards from, at most, the last 28-day period. If you time the transfer right after the Indexer has closed allocations you can make sure this is the least amount possible. If you have a communication channel with your Indexer(s), consider discussing with them to find the best time to do your transfer.

### What happens if the Indexer I currently delegate to isn't on Arbitrum One?

The L2 transfer tool will only be enabled if the Indexer you have delegated to has transferred their own stake to Arbitrum.

### Do Delegators have the option to delegate to another Indexer?

If you wish to delegate to another Indexer, you can transfer to the same Indexer on Arbitrum, then undelegate and wait for the thawing period. After this, you can select another active Indexer to delegate to.

### What if I can't find the Indexer I'm delegating to on L2?

The L2 transfer tool will automatically detect the Indexer you previously delegated to.

### Will I be able to mix and match or 'spread' my delegation across new or several Indexers instead of the prior Indexer?

The L2 transfer tool will always move your delegation to the same Indexer you delegated to previously. Once you have moved to L2, you can undelegate, wait for the thawing period, and decide if you'd like to split up your delegation.

### Am I subject to the cooldown period or can I withdraw immediately after using the L2 delegation transfer tool?

The transfer tool allows you to immediately move to L2. If you would like to undelegate you will have to wait for the thawing period. However, if an Indexer has transferred all of their stake to L2, you can withdraw on Ethereum mainnet immediately.

### Can my rewards be negatively impacted if I do not transfer my delegation?

It is anticipated that all network participation will move to Arbitrum One in the future.

### How long does it take to complete the transfer of my delegation to L2?

A 20-minute confirmation is required for delegation transfer. Please note that after the 20-minute period, you must come back and complete step 3 of the transfer process within 7 days. If you fail to do this, then your delegation may be lost. Note that in most cases the transfer tool will complete this step for you automatically. In case of a failed auto-attempt, you will need to complete it manually. If any issues arise during this process, don't worry, we'll be here to help: contact us at support@thegraph.com or on [Discord](https://discord.gg/graphprotocol).

### Can I transfer my delegation if I'm using a GRT vesting contract/token lock wallet?

Yes! The process is a bit different because vesting contracts can't forward the ETH needed to pay for the L2 gas, so you need to deposit it beforehand. If your vesting contract is not fully vested, you will also have to first initialize a counterpart vesting contract on L2 and will only be able to transfer the delegation to this L2 vesting contract. The UI on Explorer can guide you through this process when you've connected to Explorer using the vesting lock wallet.

### Does my Arbitrum vesting contract allow releasing GRT just like on mainnet?

No, the vesting contract that is created on Arbitrum will not allow releasing any GRT until the end of the vesting timeline, i.e. until your contract is fully vested. This is to prevent double spending, as otherwise it would be possible to release the same amounts on both layers.

If you'd like to release GRT from the vesting contract, you can transfer them back to the L1 vesting contract using Explorer: in your Arbitrum One profile, you will see a banner saying you can transfer GRT back to the mainnet vesting contract. This requires a transaction on Arbitrum One, waiting 7 days, and a final transaction on mainnet, as it uses the same native bridging mechanism from the GRT bridge.

### Is there any delegation tax?

No. Received tokens on L2 are delegated to the specified Indexer on behalf of the specified Delegator without charging a delegation tax.

### Will my unrealized rewards be transferred when I transfer my delegation?

​Yes! The only rewards that can't be transferred are the ones for open allocations, as those won't exist until the Indexer closes the allocations (usually every 28 days). If you've been delegating for a while, this is likely only a small fraction of rewards.

At the smart contract level, unrealized rewards are already part of your delegation balance, so they will be transferred when you transfer your delegation to L2. ​

### Is moving delegations to L2 mandatory? Is there a deadline?

​Moving delegation to L2 is not mandatory, but indexing rewards are increasing on L2 following the timeline described in [GIP-0052](https://forum.thegraph.com/t/gip-0052-timeline-and-requirements-to-increase-rewards-in-l2/4193). Eventually, if the Council keeps approving the increases, all rewards will be distributed in L2 and there will be no indexing rewards for Indexers and Delegators on L1. ​

### If I am delegating to an Indexer that has already transferred stake to L2, do I stop receiving rewards on L1?

​Many Indexers are transferring stake gradually so Indexers on L1 will still be earning rewards and fees on L1, which are then shared with Delegators. Once an Indexer has transferred all of their stake, then they will stop operating on L1, so Delegators will not receive any more rewards unless they transfer to L2.

Eventually, if the Council keeps approving the indexing rewards increases in L2, all rewards will be distributed on L2 and there will be no indexing rewards for Indexers and Delegators on L1. ​

### I don't see a button to transfer my delegation. Why is that?

​Your Indexer has probably not used the L2 transfer tools to transfer stake yet.

If you can contact the Indexer, you can encourage them to use the L2 Transfer Tools so that Delegators can transfer delegations to their L2 Indexer address. ​

### My Indexer is also on Arbitrum, but I don't see a button to transfer the delegation in my profile. Why is that?

​It is possible that the Indexer has set up operations on L2, but hasn't used the L2 transfer tools to transfer stake. The L1 smart contracts will therefore not know about the Indexer's L2 address. If you can contact the Indexer, you can encourage them to use the transfer tool so that Delegators can transfer delegations to their L2 Indexer address. ​

### Can I transfer my delegation to L2 if I have started the undelegating process and haven't withdrawn it yet?

​No. If your delegation is thawing, you have to wait the 28 days and withdraw it.

The tokens that are being undelegated are "locked" and therefore cannot be transferred to L2.

## Curation Signal

### How do I transfer my curation?

To transfer your curation, you will need to complete the following steps:

1.  Initiate signal transfer on Ethereum mainnet

2.  Specify an L2 Curator address\*

3.  Wait 20 minutes for confirmation

\*If necessary - i.e. you are using a contract address.

### How will I know if the subgraph I curated has moved to L2?

When viewing the subgraph details page, a banner will notify you that this subgraph has been transferred. You can follow the prompt to transfer your curation. You can also find this information on the subgraph details page of any subgraph that has moved.

### What if I do not wish to move my curation to L2?

When a subgraph is deprecated you have the option to withdraw your signal. Similarly, if a subgraph has moved to L2, you can choose to withdraw your signal in Ethereum mainnet or send the signal to L2.

### How do I know my curation successfully transferred?

Signal details will be accessible via Explorer approximately 20 minutes after the L2 transfer tool is initiated.

### Can I transfer my curation on more than one subgraph at a time?

There is no bulk transfer option at this time.

## Indexer Stake

### How do I transfer my stake to Arbitrum?

> Disclaimer: If you are currently unstaking any portion of your GRT on your Indexer, you will not be able to use L2 Transfer Tools.

<VideoEmbed youtube="5lTq_V4YbWc" />

To transfer your stake, you will need to complete the following steps:

1.  Initiate stake transfer on Ethereum mainnet

2.  Wait 20 minutes for confirmation

3.  Confirm stake transfer on Arbitrum

\*Note that you must confirm the transfer within 7 days otherwise your stake may be lost. In most cases, this step will run automatically, but a manual confirmation may be needed if there is a gas price spike on Arbitrum. If there are any issues during this process, there will be resources to help: contact support at support@thegraph.com or on [Discord](https://discord.gg/graphprotocol).

### Will all of my stake transfer?

You can choose how much of your stake to transfer. If you choose to transfer all of your stake at once, you will need to close any open allocations first.

If you plan on transferring parts of your stake over multiple transactions, you must always specify the same beneficiary address.

Note: You must meet the minimum stake requirements on L2 the first time you use the transfer tool. Indexers must send the minimum 100k GRT (when calling this function the first time). If leaving a portion of stake on L1, it must also be over the 100k GRT minimum and be sufficient (together with your delegations) to cover your open allocations.

### How much time do I have to confirm my stake transfer to Arbitrum?

\*\*\* You must confirm your transaction to complete the stake transfer on Arbitrum. This step must be completed within 7 days or stake could be lost.

### What if I have open allocations?

If you are not sending all of your stake, the L2 transfer tool will validate that at least the minimum 100k GRT remains in Ethereum mainnet and your remaining stake and delegation is enough to cover any open allocations. You may need to close open allocations if your GRT balance does not cover the minimums + open allocations.

### Using the transfer tools, is it necessary to wait 28 days to unstake on Ethereum mainnet before transferring?

No, you can transfer your stake to L2 immediately, there's no need to unstake and wait before using the transfer tool. The 28-day wait only applies if you'd like to withdraw the stake back to your wallet, on Ethereum mainnet or L2.

### How long will it take to transfer my stake?

It will take approximately 20 minutes for the L2 transfer tool to complete transferring your stake.

### Do I have to index on Arbitrum before I transfer my stake?

You can effectively transfer your stake first before setting up indexing, but you will not be able to claim any rewards on L2 until you allocate to subgraphs on L2, index them, and present POIs.

### Can Delegators move their delegation before I move my indexing stake?

No, in order for Delegators to transfer their delegated GRT to Arbitrum, the Indexer they are delegating to must be active on L2.

### Can I transfer my stake if I'm using a GRT vesting contract / token lock wallet?

Yes! The process is a bit different, because vesting contracts can't forward the ETH needed to pay for the L2 gas, so you need to deposit it beforehand. If your vesting contract is not fully vested, you will also have to first initialize a counterpart vesting contract on L2 and will only be able to transfer the stake to this L2 vesting contract. The UI on Explorer can guide you through this process when you've connected to Explorer using the vesting lock wallet.

### I already have stake on L2. Do I still need to send 100k GRT when I use the transfer tools the first time?

​Yes. The L1 smart contracts will not be aware of your L2 stake, so they will require you to transfer at least 100k GRT when you transfer for the first time. ​

### Can I transfer my stake to L2 if I am in the process of unstaking GRT?

​No. If any fraction of your stake is thawing, you have to wait the 28 days and withdraw it before you can transfer stake. The tokens that are being staked are "locked" and will prevent any transfers or stake to L2.

## Vesting Contract Transfer

### How do I transfer my vesting contract?

To transfer your vesting, you will need to complete the following steps:

1.  Initiate the vesting transfer on Ethereum mainnet

2.  Wait 20 minutes for confirmation

3.  Confirm vesting transfer on Arbitrum

### How do I transfer my vesting contract if I am only partially vested?

<VideoEmbed youtube="URPOb2c6o2Y" />

1.  Deposit some ETH into the transfer tool contract (UI can help estimate a reasonable amount)

2.  Send some locked GRT through the transfer tool contract, to L2 to initialize the L2 vesting lock. This will also set their L2 beneficiary address.

3.  Send their stake/delegation to L2 through the "locked" transfer tool functions in the L1Staking contract.

4.  Withdraw any remaining ETH from the transfer tool contract

### How do I transfer my vesting contract if I am fully vested?

<VideoEmbed youtube="DuZNYPNe1S0" />

For those that are fully vested, the process is similar:

1.  Deposit some ETH into the transfer tool contract (UI can help estimate a reasonable amount)

2.  Set your L2 address with a call to the transfer tool contract

3.  Send your stake/delegation to L2 through the "locked" transfer tool functions in the L1 Staking contract.

4.  Withdraw any remaining ETH from the transfer tool contract

### Can I transfer my vesting contract to Arbitrum?

You can transfer your vesting contract's GRT balance to a vesting contract in L2. This is a prerequisite for transferring stake or delegation from your vesting contract to L2. The vesting contract must hold a nonzero amount of GRT (you can transfer a small amount like 1 GRT to it if needed).

When you transfer GRT from your L1 vesting contract to L2, you can choose the amount to send and you can do this as many times as you like. The L2 vesting contract will be initialized the first time you transfer GRT.

The transfers are done using a Transfer Tool that will be visible on your Explorer profile when you connect with the vesting contract account.

Please note that you will not be able to release/withdraw GRT from the L2 vesting contract until the end of your vesting timeline when your contract is fully vested. If you need to release GRT before then, you can transfer the GRT back to the L1 vesting contract using another transfer tool that is available for that purpose.

If you haven't transferred any vesting contract balance to L2, and your vesting contract is fully vested, you should not transfer your vesting contract to L2. Instead, you can use the transfer tools to set an L2 wallet address, and directly transfer your stake or delegation to this regular wallet on L2.

### I'm using my vesting contract to stake on mainnet. Can I transfer my stake to Arbitrum?

Yes, but if your contract is still vesting, you can only transfer the stake so that it is owned by your L2 vesting contract. You must first initialize this L2 contract by transferring some GRT balance using the vesting contract transfer tool on Explorer. If your contract is fully vested, you can transfer your stake to any address in L2, but you must set it beforehand and deposit some ETH for the L2 transfer tool to pay for L2 gas.

### I'm using my vesting contract to delegate on mainnet. Can I transfer my delegations to Arbitrum?

Yes, but if your contract is still vesting, you can only transfer the delegation so that it is owned by your L2 vesting contract. You must first initialize this L2 contract by transferring some GRT balance using the vesting contract transfer tool on Explorer. If your contract is fully vested, you can transfer your delegation to any address in L2, but you must set it beforehand and deposit some ETH for the L2 transfer tool to pay for L2 gas.

### Can I specify a different beneficiary for my vesting contract on L2?

Yes, the first time you transfer a balance and set up your L2 vesting contract, you can specify an L2 beneficiary. Make sure this beneficiary is a wallet that can perform transactions on Arbitrum One, i.e. it must be an EOA or a multisig deployed to Arbitrum One.

If your contract is fully vested, you will not set up a vesting contract on L2; instead, you will set an L2 wallet address and this will be the receiving wallet for your stake or delegation on Arbitrum.

### My contract is fully vested. Can I transfer my stake or delegation to another address that is not an L2 vesting contract?

Yes. If you haven't transferred any vesting contract balance to L2, and your vesting contract is fully vested, you should not transfer your vesting contract to L2. Instead, you can use the transfer tools to set an L2 wallet address, and directly transfer your stake or delegation to this regular wallet on L2.

This allows you to transfer your stake or delegation to any L2 address.

### My vesting contract is still vesting. How do I transfer my vesting contract balance to L2?

These steps only apply if your contract is still vesting, or if you've used this process before when your contract was still vesting.

To transfer your vesting contract to L2, you will send any GRT balance to L2 using the transfer tools, which will initialize your L2 vesting contract:

1.  Deposit some ETH into the transfer tool contract (this will be used to pay for L2 gas)

2.  Revoke protocol access to the vesting contract (needed for the next step)

3.  Give protocol access to the vesting contract (will allow your contract to interact with the transfer tool)

4.  Specify an L2 beneficiary address\* and initiate the balance transfer on Ethereum mainnet

5.  Wait 20 minutes for confirmation

6.  Confirm the balance transfer on L2

\*If necessary - i.e. you are using a contract address.

\*\*\*\*You must confirm your transaction to complete the balance transfer on Arbitrum. This step must be completed within 7 days or the balance could be lost. In most cases, this step will run automatically, but a manual confirmation may be needed if there is a gas price spike on Arbitrum. If there are any issues during this process, there will be resources to help: contact support at support@thegraph.com or on [Discord](https://discord.gg/graphprotocol).

### My vesting contract shows 0 GRT so I cannot transfer it, why is this and how do I fix it?

​To initialize your L2 vesting contract, you need to transfer a nonzero amount of GRT to L2. This is required by the Arbitrum GRT bridge that is used by the L2 Transfer Tools. The GRT must come from the vesting contract's balance, so it does not include staked or delegated GRT.

If you've staked or delegated all your GRT from the vesting contract, you can manually send a small amount like 1 GRT to the vesting contract address from anywhere else (e.g. from another wallet, or an exchange). ​

### I am using a vesting contract to stake or delegate, but I don't see a button to transfer my stake or delegation to L2, what do I do?

​If your vesting contract hasn't finished vesting, you need to first create an L2 vesting contract that will receive your stake or delegation on L2. This vesting contract will not allow releasing tokens in L2 until the end of the vesting timeline, but will allow you to transfer GRT back to the L1 vesting contract to be released there.

When connected with the vesting contract on Explorer, you should see a button to initialize your L2 vesting contract. Follow that process first, and you will then see the buttons to transfer your stake or delegation in your profile. ​

### If I initialize my L2 vesting contract, will this also transfer my delegation to L2 automatically?

​No, initializing your L2 vesting contract is a prerequisite for transferring stake or delegation from the vesting contract, but you still need to transfer these separately.

You will see a banner on your profile prompting you to transfer your stake or delegation after you have initialized your L2 vesting contract.

### Can I move my vesting contract back to L1?

There is no need to do so because your vesting contract is still in L1. When you use the transfer tools, you just create a new contract in L2 that is connected with your L1 vesting contract, and you can send GRT back and forth between the two.

### Why do I need to move my vesting contract to begin with?

You need to set up an L2 vesting contract so that this account can own your stake or delegation on L2. Otherwise, there'd be no way for you to transfer the stake/delegation to L2 without "escaping" the vesting contract.

### What happens if I try to cash out my contract when it is only partially vested? Is this possible?

This is not a possibility. You can move funds back to L1 and withdraw them there.

### What if I don't want to move my vesting contract to L2?

You can keep staking/delegating on L1. Over time, you may want to consider moving to L2 to enable rewards there as the protocol scales on Arbitrum. Note that these transfer tools are for vesting contracts that are allowed to stake and delegate in the protocol. If your contract does not allow staking or delegating, or is revocable, then there is no transfer tool available. You will still be able to withdraw your GRT from L1 when available.
---
title: Arbitrum FAQ
---

Click [here](#billing-on-arbitrum-faqs) if you would like to skip to the Arbitrum Billing FAQs.

## Why did The Graph implement an L2 Solution?

By scaling The Graph on L2, network participants can now benefit from:

- Upwards of 26x savings on gas fees

- Faster transaction speed

- Security inherited from Ethereum

Scaling the protocol smart contracts onto L2 allows network participants to interact more frequently at a reduced cost in gas fees. For example, Indexers can open and close allocations more frequently to index a greater number of subgraphs. Developers can deploy and update subgraphs more easily, and Delegators can delegate GRT more frequently. Curators can add or remove signal to a larger number of subgraphs–actions previously considered too cost-prohibitive to perform frequently due to gas.

The Graph community decided to move forward with Arbitrum last year after the outcome of the [GIP-0031](https://forum.thegraph.com/t/gip-0031-arbitrum-grt-bridge/3305) discussion.

## What do I need to do to use The Graph on L2?

The Graph’s billing system accepts GRT on Arbitrum, and users will need ETH on Arbitrum to pay their gas. While The Graph protocol started on Ethereum Mainnet, all activity, including the billing contracts, is now on Arbitrum One.

Consequently, to pay for queries, you need GRT on Arbitrum. Here are a few different ways to achieve this:

- If you already have GRT on Ethereum, you can bridge it to Arbitrum. You can do this via the GRT bridging option provided in Subgraph Studio or by using one of the following bridges:

  - [The Arbitrum Bridge](https://bridge.arbitrum.io/?l2ChainId=42161)
  - [TransferTo](https://transferto.xyz/swap)

- If you have other assets on Arbitrum, you can swap them for GRT through a swapping protocol like Uniswap.
- Alternatively, you can acquire GRT directly on Arbitrum through a decentralized exchange.

Once you have GRT on Arbitrum, you can add it to your billing balance.

To take advantage of using The Graph on L2, use this dropdown switcher to toggle between chains.

![Dropdown switcher to toggle Arbitrum](/img/arbitrum-screenshot-toggle.png)

## As a subgraph developer, data consumer, Indexer, Curator, or Delegator, what do I need to do now?

Network participants must move to Arbitrum to continue participating in The Graph Network. Please refer to [L2 Transfer Tool Guide](/arbitrum/l2-transfer-tools-guide/) for additional support.

All indexing rewards are now entirely on Arbitrum.

## Were there any risks associated with scaling the network to L2?

All smart contracts have been thoroughly [audited](https://github.com/graphprotocol/contracts/blob/main/packages/contracts/audits/OpenZeppelin/2022-07-graph-arbitrum-bridge-audit.pdf).

Everything has been tested thoroughly, and a contingency plan is in place to ensure a safe and seamless transition. Details can be found [here](https://forum.thegraph.com/t/gip-0037-the-graph-arbitrum-deployment-with-linear-rewards-minted-in-l2/3551#risks-and-security-considerations-20).

## Are existing subgraphs on Ethereum working?

All subgraphs are now on Arbitrum. Please refer to [L2 Transfer Tool Guide](/arbitrum/l2-transfer-tools-guide/) to ensure your subgraphs operate seamlessly.

## Does GRT have a new smart contract deployed on Arbitrum?

Yes, GRT has an additional [smart contract on Arbitrum](https://arbiscan.io/address/0x9623063377ad1b27544c965ccd7342f7ea7e88c7). However, the Ethereum mainnet [GRT contract](https://etherscan.io/token/0xc944e90c64b2c07662a292be6244bdf05cda44a7) will remain operational.

## Billing on Arbitrum FAQs

## What do I need to do about the GRT in my billing balance?

Nothing! Your GRT has been securely migrated to Arbitrum and is being used to pay for queries as you read this.

## How do I know my funds have migrated securely to Arbitrum?

All GRT billing balances have already been successfully migrated to Arbitrum. You can view the billing contract on Arbitrum [here](https://arbiscan.io/address/0x1B07D3344188908Fb6DEcEac381f3eE63C48477a).

## How do I know the Arbitrum bridge is secure?

The bridge has been [heavily audited](https://code4rena.com/contests/2022-10-the-graph-l2-bridge-contest) to ensure safety and security for all users.

## What do I need to do if I'm adding fresh GRT from my Ethereum mainnet wallet?

Adding GRT to your Arbitrum billing balance can be done with a one-click experience in [Subgraph Studio](https://thegraph.com/studio/). You'll be able to easily bridge your GRT to Arbitrum and fill your API keys in one transaction.

Visit the [Billing page](/billing/) for more detailed instructions on adding, withdrawing, or acquiring GRT.
---
title: Tokenomics of The Graph Network
description: The Graph Network is incentivized by powerful tokenomics. Here’s how GRT, The Graph’s native work utility token works.
---

- GRT Token Address on Mainnet: [0xc944e90c64b2c07662a292be6244bdf05cda44a7](https://etherscan.io/token/0xc944e90c64b2c07662a292be6244bdf05cda44a7)

- GRT Token Address on Arbitrum One: [0x9623063377AD1B27544C965cCd7342f7EA7e88C7](https://arbiscan.io/token/0x9623063377ad1b27544c965ccd7342f7ea7e88c7)

The Graph is a decentralized protocol that enables easy access to blockchain data.

It's similar to a B2B2C model, except it is powered by a decentralized network of participants. Network participants work together to provide data to end users in exchange for GRT rewards. GRT is the work utility token that coordinates data providers and consumers. GRT serves as a utility for coordinating data providers and consumers within the network and incentivizes protocol participants to organize data effectively.

By using The Graph, users can easily access data from the blockchain, paying only for the specific information they need. The Graph is used by many [popular dapps](https://thegraph.com/explorer) in the web3 ecosystem today.

The Graph indexes blockchain data similarly to how Google indexes the web. In fact, you may already be using The Graph without realizing it. If you've viewed the front end of a dapp that gets its data from a subgraph, you queried data from a subgraph!

The Graph plays a crucial role in making blockchain data more accessible and enabling a marketplace for its exchange.

## The Roles of Network Participants

There are four primary network participants:

1.  Delegators - Delegate GRT to Indexers & secure the network

2.  Curators - Find the best subgraphs for Indexers

3.  Developers - Build & query subgraphs

4.  Indexers - Backbone of blockchain data

Fishermen and Arbitrators are also integral to the network’s success through other contributions, supporting the work of the other primary participant roles. For more information about network roles, [read this article](https://thegraph.com/blog/the-graph-grt-token-economics/).

![Tokenomics diagram](/img/updated-tokenomics-image.png)

## Delegators (Passively earn GRT)

Indexers are delegated GRT by Delegators increasing the Indexer’s stake in subgraphs on the network. In return, Delegators earn a percentage of all query fees and indexing rewards from the Indexer. Each Indexer sets the cut that will be rewarded to Delegators independently, creating competition among Indexers to attract Delegators. Most Indexers offer between 9-12% annually.

For example, if a Delegator were to delegate 15k GRT to an Indexer offering 10%, the Delegator would receive ~1500 GRT in rewards annually.

There is a 0.5% delegation tax which is burned whenever a Delegator delegates GRT on the network. If a Delegator chooses to withdraw their delegated GRT, the Delegator must wait for the 28-epoch unbonding period. Each epoch is 6,646 blocks, which means 28 epochs ends up being approximately 26 days.

If you're reading this, you're capable of becoming a Delegator right now by heading to the [network participants page](https://thegraph.com/explorer/participants/indexers), and delegating GRT to an Indexer of your choice.

## Curators (Earn GRT)

Curators identify high-quality subgraphs, and "curate" them (i.e., signal GRT on them) to earn curation shares, which guarantee a percentage of all future query fees generated by the subgraph. While any independent network participant can be a Curator, typically subgraph developers are among the first Curators for their own subgraphs because they want to ensure their subgraph is indexed.

As of April 11th, 2024, subgraph developers are encouraged to curate their subgraph with at least 3,000 GRT. However, this number may be impacted by network activity and community participation.

Curators pay a 1% curation tax when they curate a new subgraph. This curation tax is burned, decreasing the supply of GRT.

## Developers

Developers build and query subgraphs to retrieve blockchain data. Since subgraphs are open source, developers can query existing subgraphs to load blockchain data into their dapps. Developers pay for queries they make in GRT, which is distributed to network participants.

### Creating a subgraph

Developers can [create a subgraph](/developing/creating-a-subgraph/) to index data on the blockchain. Subgraphs are instructions for Indexers about which data should be served to consumers.

Once developers have built and tested their subgraph, they can [publish their subgraph](/publishing/publishing-a-subgraph/) on The Graph's decentralized network.

### Querying an existing subgraph

Once a subgraph is [published](/publishing/publishing-a-subgraph/) to The Graph's decentralized network, anyone can create an API key, add GRT to their billing balance, and query the subgraph.

Subgraphs are [queried using GraphQL](/querying/querying-the-graph/), and the query fees are paid for with GRT in [Subgraph Studio](https://thegraph.com/studio/). Query fees are distributed to network participants based on their contributions to the protocol.

1% of the query fees paid to the network are burned.

## Indexers (Earn GRT)

Indexers are the backbone of The Graph. They operate independent hardware and software powering The Graph’s decentralized network. Indexers serve data to consumers based on instructions from subgraphs.

Indexers can earn GRT rewards in two ways:

1.  Query fees: GRT paid by developers or users for subgraph data queries. Query fees are directly distributed to Indexers according to the exponential rebate function (see GIP [here](https://forum.thegraph.com/t/gip-0051-exponential-query-fee-rebates-for-indexers/4162)).

2.  Indexing rewards: the 3% annual issuance is distributed to Indexers based on the number of subgraphs they are indexing. These rewards incentivize Indexers to index subgraphs, occasionally before the query fees begin, to accrue and submit Proofs of Indexing (POIs) verifying that they have indexed data accurately.

Each subgraph is allotted a portion of the total network token issuance, based on the amount of the subgraph’s curation signal. That amount is then rewarded to Indexers based on their allocated stake on the subgraph.

In order to run an indexing node, Indexers must stake 100,000 GRT or more with the network. Indexers are incentivized to stake GRT in proportion to the amount of queries they serve.

Indexers can increase their GRT allocations on subgraphs by accepting GRT delegation from Delegators, and they can accept up to 16 times their initial stake. If an Indexer becomes "over-delegated" (i.e., more than 16 times their initial stake), they will not be able to use the additional GRT from Delegators until they increase their stake in the network.

The amount of rewards an Indexer receives can vary based on the initial stake, accepted delegation, quality of service, and many more factors. The following chart is publicly available data from an active Indexer on The Graph's decentralized network.

### The Indexer stake & reward of allnodes-com.eth

![Indexing stake and rewards](/img/indexing-stake-and-income.png)

This data is from February 2021 to September 2022.

> Please note, this will improve when the [Arbitrum migration](https://forum.thegraph.com/t/gip-0037-the-graph-arbitrum-deployment-with-linear-rewards-minted-in-l2/3551) is complete, making gas costs a significantly lower burden for participating on the network.

## Token Supply: Burning & Issuance

The initial token supply is 10 billion GRT, with a target of 3% new issuance annually to reward Indexers for allocating stake on subgraphs. This means that the total supply of GRT tokens will increase by 3% each year as new tokens are issued to Indexers for their contribution to the network.

The Graph is designed with multiple burning mechanisms to offset new token issuance. Approximately 1% of the GRT supply is burned annually through various activities on the network, and this number has been increasing as network activity continues to grow. These burning activities include a 0.5% delegation tax whenever a Delegator delegates GRT to an Indexer, a 1% curation tax when Curators signal on a subgraph, and a 1% of query fees for blockchain data.

![Total burned GRT](/img/total-burned-grt.jpeg)

In addition to these regularly occurring burning activities, the GRT token also has a slashing mechanism in place to penalize malicious or irresponsible behavior by Indexers. If an Indexer is slashed, 50% of their indexing rewards for the epoch are burned (while the other half goes to the fisherman), and their self-stake is slashed by 2.5%, with half of this amount being burned. This helps to ensure that Indexers have a strong incentive to act in the best interests of the network and to contribute to its security and stability.

## Improving the Protocol

The Graph Network is ever-evolving and improvements to the economic design of the protocol are constantly being made to provide the best experience for all network participants. The Graph Council oversees protocol changes and community members are encouraged to participate. Get involved with protocol improvements in [The Graph Forum](https://forum.thegraph.com/).
---
title: Curating
---

Curators are critical to The Graph's decentralized economy. They use their knowledge of the web3 ecosystem to assess and signal on the subgraphs that should be indexed by The Graph Network. Through Graph Explorer, Curators view network data to make signaling decisions. In turn, The Graph Network rewards Curators who signal on good quality subgraphs with a share of the query fees those subgraphs generate. The amount of GRT signaled is one of the key considerations for indexers when determining which subgraphs to index.

## What Does Signaling Mean for The Graph Network?

Before consumers can query a subgraph, it must be indexed. This is where curation comes into play. In order for Indexers to earn substantial query fees on quality subgraphs, they need to know what subgraphs to index. When Curators signal on a subgraph, it lets Indexers know that a subgraph is in demand and of sufficient quality that it should be indexed.

Indexers can trust the signal from a Curator because upon signaling, Curators mint a curation share for the subgraph, entitling Curators to a portion of future query fees that the subgraph drives.

Curators make The Graph network efficient and [signaling](#how-to-signal) is the process that curators use to let Indexers know that a subgraph is good to index. Indexers can trust the signal from a curator because upon signaling, curators mint a curation share for the subgraph, entitling them to a portion of future query fees that the subgraph drives.

Curator signals are represented as ERC20 tokens called Graph Curation Shares (GCS). Those that want to earn more query fees should signal their GRT to subgraphs that they predict will generate a strong flow of fees to the network. Curators cannot be slashed for bad behavior, but there is a deposit tax on Curators to disincentivize poor decision-making that could harm the integrity of the network. Curators will also earn fewer query fees if they curate on a low-quality subgraph because there will be fewer queries to process or fewer Indexers to process them.

The [Sunrise Upgrade Indexer](/sunrise/#what-is-the-upgrade-indexer) ensures the indexing of all subgraphs, signaling GRT on a particular subgraph will draw more indexers to it. This incentivization of additional Indexers through curation aims to enhance the quality of service for queries by reducing latency and enhancing network availability.

When signaling, Curators can decide to signal on a specific version of the subgraph or to signal using auto-migrate. If they signal using auto-migrate, a curator’s shares will always be updated to the latest version published by the developer. If they decide to signal on a specific version instead, shares will always stay on this specific version.

If you require assistance with curation to enhance the quality of service, please send a request to the Edge & Node team at support@thegraph.zendesk.com and specify the subgraphs you need assistance with.

Indexers can find subgraphs to index based on curation signals they see in Graph Explorer (screenshot below).

![Explorer subgraphs](/img/explorer-subgraphs.png)

## How to Signal

Within the Curator tab in Graph Explorer, curators will be able to signal and unsignal on certain subgraphs based on network stats. For a step-by-step overview of how to do this in Graph Explorer, [click here.](/network/explorer)

A curator can choose to signal on a specific subgraph version, or they can choose to have their signal automatically migrate to the newest production build of that subgraph. Both are valid strategies and come with their own pros and cons.

Signaling on a specific version is especially useful when one subgraph is used by multiple dApps. One dApp might need to regularly update the subgraph with new features. Another dApp might prefer to use an older, well-tested subgraph version. Upon initial curation, a 1% standard tax is incurred.

Having your signal automatically migrate to the newest production build can be valuable to ensure you keep accruing query fees. Every time you curate, a 1% curation tax is incurred. You will also pay a 0.5% curation tax on every migration. Subgraph developers are discouraged from frequently publishing new versions - they have to pay a 0.5% curation tax on all auto-migrated curation shares.

> **Note**: The first address to signal a particular subgraph is considered the first curator and will have to do much more gas-intensive work than the rest of the following curators because the first curator initializes the curation share tokens, and also transfers tokens into The Graph proxy.

## Withdrawing your GRT

Curators have the option to withdraw their signaled GRT at any time.

Unlike the process of delegating, if you decide to withdraw your signaled GRT you will not have to wait for a cooldown period and will receive the entire amount (minus the 1% curation tax).

Once a curator withdraws their signal, indexers may choose to keep indexing the subgraph, even if there's currently no active GRT signaled.

However, it is recommended that curators leave their signaled GRT in place not only to receive a portion of the query fees, but also to ensure reliability and uptime of the subgraph.

## Risks

1. The query market is inherently young at The Graph and there is risk that your %APY may be lower than you expect due to nascent market dynamics.
2. Curation Fee - when a curator signals GRT on a subgraph, they incur a 1% curation tax. This fee is burned.
3. (Ethereum only) When curators burn their shares to withdraw GRT, the GRT valuation of the remaining shares will be reduced. Be aware that in some cases, curators may decide to burn their shares **all at once**. This situation may be common if a dApp developer stops versioning/improving and querying their subgraph or if a subgraph fails. As a result, remaining curators might only be able to withdraw a fraction of their initial GRT. For a network role with a lower risk profile, see [Delegators](/network/delegating).
4. A subgraph can fail due to a bug. A failed subgraph does not accrue query fees. As a result, you’ll have to wait until the developer fixes the bug and deploys a new version.
   - If you are subscribed to the newest version of a subgraph, your shares will auto-migrate to that new version. This will incur a 0.5% curation tax.
   - If you have signaled on a specific subgraph version and it fails, you will have to manually burn your curation shares. You can then signal on the new subgraph version, thus incurring a 1% curation tax.

## Curation FAQs

### 1. What % of query fees do Curators earn?

By signalling on a subgraph, you will earn a share of all the query fees that the subgraph generates. 10% of all query fees go to the Curators pro-rata to their curation shares. This 10% is subject to governance.

### 2. How do I decide which subgraphs are high quality to signal on?

Finding high-quality subgraphs is a complex task, but it can be approached in many different ways. As a Curator, you want to look for trustworthy subgraphs that are driving query volume. A trustworthy subgraph may be valuable if it is complete, accurate, and supports a dApp’s data needs. A poorly architected subgraph might need to be revised or re-published, and can also end up failing. It is critical for Curators to review a subgraph’s architecture or code in order to assess if a subgraph is valuable. As a result:

- Curators can use their understanding of a network to try and predict how an individual subgraph may generate a higher or lower query volume in the future
- Curators should also understand the metrics that are available through Graph Explorer. Metrics like past query volume and who the subgraph developer is can help determine whether or not a subgraph is worth signalling on.

### 3. What’s the cost of updating a subgraph?

Migrating your curation shares to a new subgraph version incurs a curation tax of 1%. Curators can choose to subscribe to the newest version of a subgraph. When curator shares get auto-migrated to a new version, Curators will also pay half curation tax, ie. 0.5%, because upgrading subgraphs is an on-chain action that costs gas.

### 4. How often can I update my subgraph?

It’s suggested that you don’t update your subgraphs too frequently. See the question above for more details.

### 5. Can I sell my curation shares?

Curation shares cannot be "bought" or "sold" like other ERC20 tokens that you may be familiar with. They can only be minted (created) or burned (destroyed).

As a Curator on Arbitrum, you are guaranteed to get back the GRT you initially deposited (minus the tax).

### 6. Am I eligible for a curation grant?

Curation grants are determined individually on a case-by-case basis. If you need assistance with curation, please send a request to support@thegraph.zendesk.com.

Still confused? Check out our Curation video guide below:

<VideoEmbed youtube="VytTEcf0dxQ" />
---
title: Developing
---

To start coding right away, go to [Developer Quick Start](/quick-start/).

## Overview

As a developer, you need data to build and power your dapp. Querying and indexing blockchain data is challenging, but The Graph provides a solution to this issue.

On The Graph, you can:

1.  Create, deploy, and publish subgraphs to The Graph using Graph CLI and [Subgraph Studio](https://thegraph.com/studio/).
2.  Use GraphQL to query existing subgraphs.

### What is GraphQL?

- [GraphQL](https://graphql.org/learn/) is the query language for APIs and a runtime for executing those queries with your existing data. The Graph uses GraphQL to query subgraphs.

### Developer Actions

- Query subgraphs built by other developers in [The Graph Network](https://thegraph.com/explorer) and integrate them into your own dapps.
- Create custom subgraphs to fulfill specific data needs, allowing improved scalability and flexibility for other developers.
- Deploy, publish and signal your subgraphs within The Graph Network.

## Subgraph Specifics

### What are subgraphs?

A subgraph is a custom API built on blockchain data. It extracts data from a blockchain, processes it, and stores it so that it can be easily queried via GraphQL.

A subgraph primarily consists of the following files:

- `subgraph.yaml`: this YAML file contains the [subgraph manifest](/developing/creating-a-subgraph/#the-subgraph-manifest).
- `subgraph.graphql`: this GraphQL schema defines what data is stored for your subgraph, and how to query it via [GraphQL](/developing/creating-a-subgraph/#the-graphql-schema).
- `mappings`: this [AssemblyScript](https://github.com/AssemblyScript/assemblyscript) mappings file translates data from the event data to the entities defined in your schema.

Learn the detailed specifics to [create a subgraph](/developing/creating-a-subgraph/).

## Subgraph Lifecycle

Here is a general overview of a subgraph’s lifecycle:

![Subgraph Lifecycle](/img/subgraph-lifecycle.png)

### Build locally

Great subgraphs start with a local development environment and unit tests. Developers use [Graph CLI](https://github.com/graphprotocol/graph-tooling/tree/main/packages/cli), a command-line interface tool for building and deploying subgraphs on The Graph. They can also use [Graph TypeScript](/developing/graph-ts/) and [Matchstick](/developing/unit-testing-framework/) to create robust subgraphs.

### Deploy to Subgraph Studio

Once defined, a subgraph can be [deployed to Subgraph Studio](/deploying/deploying-a-subgraph-to-studio/). In Subgraph Studio, you can do the following:

- Use its staging environment to index the deployed subgraph and make it available for review.
- Verify that your subgraph doesn't have any indexing errors and works as expected.

### Publish to the Network

When you're happy with your subgraph, you can [publish it](/publishing/publishing-a-subgraph/) to The Graph Network.

- This is an on-chain action, which registers the subgraph and makes it discoverable by Indexers.
- Published subgraphs have a corresponding NFT, which defines the ownership of the subgraph. You can [transfer the subgraph's ownership](/managing/transfer-and-deprecate-a-subgraph/) by sending the NFT.
- Published subgraphs have associated metadata, which provides other network participants with useful context and information.

### Add Curation Signal for Indexing

Published subgraphs are unlikely to be picked up by Indexers without curation signal. To encourage indexing you should add signal to your subgraph. Learn more about signaling and [curating](/network/curating/) on The Graph.

#### What is signal?

- Signal is locked GRT associated with a given subgraph. It indicates to Indexers that a given subgraph will receive query volume and it contributes to the indexing rewards available for processing it.
- Third party Curators may also signal on a given subgraph, if they deem the subgraph likely to drive query volume.

### Querying & Application Development

Subgraphs on The Graph Network receive 100,000 free queries per month, after which point developers can either [pay for queries with GRT or a credit card](/billing/).

Learn more about [querying subgraphs](/querying/querying-the-graph/).

### Updating Subgraphs

To update your subgraph with bug fixes or new functionalities, initiate a transaction to point it to the new version. You can deploy new versions of your subgraphs to [Subgraph Studio](https://thegraph.com/studio/) for development and testing.

- If you selected "auto-migrate" when you applied the signal, updating the subgraph will migrate any signal to the new version and incur a migration tax.
- This signal migration should prompt Indexers to start indexing the new version of the subgraph, so it should soon become available for querying.

### Deprecating & Transferring Subgraphs

If you no longer need a published subgraph, you can [deprecate or transfer a subgraph](/managing/transfer-and-deprecate-a-subgraph/). Deprecating a subgraph returns any signaled GRT to [Curators](/network/curating/).
---
title: Network Overview
---

The Graph Network is a decentralized indexing protocol for organizing blockchain data.

## How does it work?

Applications use [GraphQL](/querying/graphql-api/) to query open APIs called subgraphs and retrieve data that is indexed on the network. With The Graph, developers can build serverless applications that run entirely on public infrastructure.

## Specifics

The Graph Network consists of Indexers, Curators, and Delegators that provide services to the network and serve data to web3 applications.

![Token Economics](/img/Network-roles@2x.png)

### Economics

To ensure economic security of The Graph Network and the integrity of data being queried, participants stake and use Graph Tokens ([GRT](/tokenomics)). GRT is a work utility token that is an ERC-20, which is used to allocate resources in the network.

Active Indexers, Curators, and Delegators can provide services and earn income from the network. The income they earn is proportional to the amount of work they perform and their GRT stake.
---
title: Delegating
---

Delegators are network participants who delegate (i.e., "stake") GRT to one or more Indexers.

- They help secure the network without running a Graph Node themselves.

- They earn a portion of an Indexer's query fees and rewards by delegating to them.

## How does this work?

The number of queries an Indexer can process depends on their own stake, **the delegated stake**, and the price the Indexer charges for each query. Therefore, the more stake allocated to an Indexer, the more potential queries an Indexer can process.

## Delegator Guide

Learn how to be an effective Delegator in The Graph Network.

Delegators share the earnings of the protocol alongside all Indexers based on their delegated stake. Therefore, they must use their best judgment to choose Indexers based on multiple factors.

> Please note this guide does not cover steps such as setting up MetaMask properly, as that information is widely available online.

There are three sections in this guide:

- The risks of delegating tokens in The Graph Network
- How to calculate expected returns as a Delegator
- A video guide showing the steps to delegate in the Graph Network UI

## Delegation Risks

Listed below are the main risks of being a Delegator in the protocol.

### The delegation tax

Delegators cannot be slashed for bad behavior, but there is a tax on Delegators to disincentivize poor decision-making that could harm the integrity of the network.

As a Delegator, it's important to understand the following:

- You will be charged 0.5% every time you delegate. This means that if you delegate 1,000 GRT, you will automatically burn 5 GRT.

- In order to be safe, you should calculate your potential return when delegating to an Indexer. For example, you might calculate how many days it will take before you have earned back the 0.5% tax on your delegation.

### The delegation unbonding period

Whenever a Delegator wants to undelegate, their tokens are subject to a 28-day unbonding period. This means they cannot transfer their tokens or earn any rewards for 28 days.

### Why is this important?

If you choose an Indexer that is not trustworthy or not doing a good job, you will want to undelegate. This means you will be losing a lot of opportunities to earn rewards, which can be just as bad as burning GRT. As a result, it’s recommended that you choose an Indexer wisely.

<div sx={{ mx: 'auto', maxWidth: '400px' }}>
  ![Delegation unbonding](/img/Delegation-Unbonding.png) _Note the 0.5% fee in the Delegation UI, as well as the 28 day
  unbonding period._
</div>

### Choosing a trustworthy Indexer with a fair reward payout for Delegators

In order to understand how to choose a trustworthy Indexer, you need to understand the Delegation Parameters.

#### Delegation Parameters

- **Indexing Reward Cut** - The portion of the rewards the Indexer will keep for themselves.
  - If an Indexer's reward cut is set to 100%, as a Delegator, you will get 0 indexing rewards.
  - If it is set to 80%, as a Delegator, you will receive 20%.

<div sx={{ mx: 'auto', maxWidth: '700px' }}>
  ![Indexing Reward Cut](/img/Indexing-Reward-Cut.png) *The top Indexer is giving Delegators 90% of the rewards. The
  middle one is giving Delegators 20%. The bottom one is giving Delegators ~83%.*
</div>

- **Query Fee Cut** - This is just like the Indexing Reward Cut, but it applies to returns on the query fees that the Indexer collects.

As you can see, in order to choose the right Indexer, you must consider multiple things.

- It is highly recommend that you explore [The Graph Discord](https://discord.gg/graphprotocol) to determine which Indexers have the best social and technical reputations and which ones reward Delegators consistently.
- Many Indexers are very active in Discord and will be happy to answer your questions.
- Many of them have been Indexing for months, and they are doing their best to help Delegators earn a good return, as it improves the health and success of the network.

## Calculating Delegators Expected Return

A Delegator must consider the following factors to determine a return:

- Consider an Indexer's ability to use the Delegated tokens available to them.
  - If an Indexer is not allocating all the tokens available, they are not earning the maximum profit they could be for themselves or their Delegators.
- Pay attention to the first few days of delegating.
  - An Indexer can choose to close an allocation and collect rewards anytime between 1 and 28 days. It is possible that an Indexer might have a lot of rewards they still need to collect, so their total rewards are low.

### Considering the query fee cut and indexing fee cut

You should choose an Indexer that is transparent and honest about setting their Query Fee and Indexing Fee Cuts. You should also look at the Parameters Cooldown time to see how much of a time buffer you have. After that is done, it is simple to calculate the amount of rewards you are getting.

The formula is:

![Delegation Image 3](/img/Delegation-Reward-Formula.png)

### Considering the Indexer's delegation pool

Delegators should consider the proportion of the Delegation Pool they own.

All delegation rewards are shared evenly, with a pool rebalancing based on the amount the Delegator deposited into the pool.

This gives the Delegator a share of the pool:

![Share formula](/img/Share-Forumla.png)

> The formula above shows that it is possible for an Indexer offering only 20% to Delegators to provide a better reward than an Indexer giving 90%. Simply do the math to determine the best reward.

### Considering the delegation capacity

Finally, consider the delegation capacity. Currently, the Delegation Ratio is set to 16.

#### Why does this matter?

This means that if an Indexer has staked 1,000,000 GRT, their Delegation Capacity is 16,000,000 GRT of delegated tokens that they can use in the protocol. Any delegated tokens over this amount will dilute all the Delegator rewards.

Imagine an Indexer with 100,000,000 GRT delegated to them, but their capacity is only 16,000,000 GRT. This means effectively, 84,000,000 GRT tokens are not being used to earn tokens. So, both the Delegators and the Indexers are earning less rewards than they could be.

Therefore, a Delegator should always consider the Delegation Capacity of an Indexer, and factor it into their decision making.

## Delegator FAQs and Bugs

### MetaMask "Pending Transaction" Bug

1. When I try to delegate my transaction in MetaMask, it appears as "Pending" or "Queued" for longer than expected. What should I do?

At times, attempts to delegate to Indexers via MetaMask can fail and result in prolonged periods of "Pending" or "Queued" transaction attempts.

#### Example

Let's say you attempt to delegate with an insufficient gas fee relative to the current prices.

- This action can cause the transaction attempt to display as "Pending" in your MetaMask wallet for 15+ minutes. When this happens, you can attempt subsequent transactions, but these will only be processed until the initial transaction is mined because transactions for an address must be processed in order.
- In such cases, these transactions can be cancelled in MetaMask, but the transactions attempts will accrue gas fees without any guarantee that subsequent attempts will be successful.

A simple resolution to this bug is to restart the browser (e.g., using "abort:restart" in the address bar), which will cancel all previous attempts without gas being subtracted from the wallet. Several users who have encountered this issue have reported successful transactions after restarting their browser and attempting to delegate.

## Video Guide

This video guide reviews this page while interacting with the UI.

<VideoEmbed youtube="2G7S2gdURdc" />
---
title: Graph Explorer
---

Learn about The Graph Explorer and access the world of subgraphs and network data.

Graph Explorer consists of multiple parts where you can interact with other subgraph developers, dapp developers, Curators, Indexers, and Delegators.

## Video Guide

For a general overview of Graph Explorer, check out the video below:

<VideoEmbed youtube="u224xf7rEBY" />

## Subgraphs

After you just finish deploying and publishing your subgraph in Subgraph Studio, click on the "subgraphs tab” at the top of the navigation bar to access the following:

- Your own finished subgraphs
- Subgraphs published by others
- The exact subgraph you want (based on the date created, signal amount, or name).

![Explorer Image 1](/img/Subgraphs-Explorer-Landing.png)

When you click into a subgraph, you will be able to do the following:

- Test queries in the playground and be able to leverage network details to make informed decisions.
- Signal GRT on your own subgraph or the subgraphs of others to make indexers aware of its importance and quality.
- This is critical because signaling on a subgraph incentivizes it to be indexed, meaning it’ll eventually surface on the network to serve queries.

![Explorer Image 2](/img/Subgraph-Details.png)

On each subgraph’s dedicated page, you can do the following:

- Signal/Un-signal on subgraphs
- View more details such as charts, current deployment ID, and other metadata
- Switch versions to explore past iterations of the subgraph
- Query subgraphs via GraphQL
- Test subgraphs in the playground
- View the Indexers that are indexing on a certain subgraph
- Subgraph stats (allocations, Curators, etc)
- View the entity who published the subgraph

![Explorer Image 3](/img/Explorer-Signal-Unsignal.png)

## Participants

This section provides a bird' s-eye view of all "participants," which includes everyone participating in the network, such as Indexers, Delegators, and Curators.

### 1. Indexers

![Explorer Image 4](/img/Indexer-Pane.png)

Indexers are the backbone of the protocol. They stake on subgraphs, index them, and serve queries to anyone consuming subgraphs.

In the Indexers table, you can see an Indexers’ delegation parameters, their stake, how much they have staked to each subgraph, and how much revenue they have made from query fees and indexing rewards.

**Specifics**

- Query Fee Cut - the % of the query fee rebates that the Indexer keeps when splitting with Delegators.
- Effective Reward Cut - the indexing reward cut applied to the delegation pool. If it’s negative, it means that the Indexer is giving away part of their rewards. If it’s positive, it means that the Indexer is keeping some of their rewards.
- Cooldown Remaining - the time remaining until the Indexer can change the above delegation parameters. Cooldown periods are set up by Indexers when they update their delegation parameters.
- Owned - This is the Indexer’s deposited stake, which may be slashed for malicious or incorrect behavior.
- Delegated - Stake from Delegators which can be allocated by the Indexer, but cannot be slashed.
- Allocated - Stake that Indexers are actively allocating towards the subgraphs they are indexing.
- Available Delegation Capacity - the amount of delegated stake the Indexers can still receive before they become over-delegated.
- Max Delegation Capacity - the maximum amount of delegated stake the Indexer can productively accept. An excess delegated stake cannot be used for allocations or rewards calculations.
- Query Fees - this is the total fees that end users have paid for queries from an Indexer over all time.
- Indexer Rewards - this is the total indexer rewards earned by the Indexer and their Delegators over all time. Indexer rewards are paid through GRT issuance.

Indexers can earn both query fees and indexing rewards. Functionally, this happens when network participants delegate GRT to an Indexer. This enables Indexers to receive query fees and rewards depending on their Indexer parameters.

- Indexing parameters can be set by clicking on the right-hand side of the table or by going into an Indexer’s profile and clicking the “Delegate” button.

To learn more about how to become an Indexer, you can take a look at the [official documentation](/network/indexing) or [The Graph Academy Indexer guides.](https://thegraph.academy/delegators/choosing-indexers/)

![Indexing details pane](/img/Indexing-Details-Pane.png)

### 2. Curators

Curators analyze subgraphs to identify which subgraphs are of the highest quality. Once a Curator has found a potentially high-quality subgraph, they can curate it by signaling on its bonding curve. In doing so, Curators let Indexers know which subgraphs are high quality and should be indexed.

- Curators can be community members, data consumers, or even subgraph developers who signal on their own subgraphs by depositing GRT tokens into a bonding curve.
  - By depositing GRT, Curators mint curation shares of a subgraph. As a result, they can earn a portion of the query fees generated by the subgraph they have signaled on.
  - The bonding curve incentivizes Curators to curate the highest quality data sources.

In the The Curator table listed below you can see:

- The date the Curator started curating
- The number of GRT that was deposited
- The number of shares a Curator owns

![Explorer Image 6](/img/Curation-Overview.png)

If you want to learn more about the Curator role, you can do so by visiting [official documentation.](/network/curating) or [The Graph Academy](https://thegraph.academy/curators/).

### 3. Delegators

Delegators play a key role in maintaining the security and decentralization of The Graph Network. They participate in the network by delegating (i.e., “staking”) GRT tokens to one or multiple indexers.

- Without Delegators, Indexers are less likely to earn significant rewards and fees. Therefore, Indexers attract Delegators by offering them a portion of their indexing rewards and query fees.
- Delegators select Indexers based on a number of different variables, such as past performance, indexing reward rates, and query fee cuts.
- Reputation within the community can also play a factor in the selection process. It’s recommended to connect with the selected Indexers via [The Graph’s Discord](https://discord.gg/graphprotocol) or [The Graph Forum](https://forum.thegraph.com/)!

![Explorer Image 7](/img/Delegation-Overview.png)

In the Delegators table you can see the active Delegators in the community and important metrics:

- The number of Indexers a Delegator is delegating towards
- A Delegator’s original delegation
- The rewards they have accumulated but have not withdrawn from the protocol
- The realized rewards they withdrew from the protocol
- Total amount of GRT they have currently in the protocol
- The date they last delegated

If you want to learn more about how to become a Delegator, check out the [official documentation](/network/delegating) or [The Graph Academy](https://docs.thegraph.academy/official-docs/delegator/choosing-indexers).

## Network

In this section, you can see global KPIs and view the ability to switch to a per-epoch basis and analyze network metrics in more detail. These details will give you a sense of how the network is performing over time.

### Overview

The overview section has both all the current network metrics and some cumulative metrics over time:

- The current total network stake
- The stake split between the Indexers and their Delegators
- Total supply, minted, and burned GRT since the network inception
- Total Indexing rewards since the inception of the protocol
- Protocol parameters such as curation reward, inflation rate, and more
- Current epoch rewards and fees

A few key details to note:

- **Query fees represent the fees generated by the consumers**. They can be claimed (or not) by the Indexers after a period of at least 7 epochs (see below) after their allocations towards the subgraphs have been closed and the data they served has been validated by the consumers.
- **Indexing rewards represent the amount of rewards the Indexers claimed from the network issuance during the epoch.** Although the protocol issuance is fixed, the rewards only get minted once Indexers close their allocations towards the subgraphs they’ve been indexing. So, the per-epoch number of rewards varies (ie. during some epochs, Indexers might’ve collectively closed allocations that have been open for many days).

![Explorer Image 8](/img/Network-Stats.png)

### Epochs

In the Epochs section, you can analyze on a per-epoch basis, metrics such as:

- Epoch start or end block
- Query fees generated and indexing rewards collected during a specific epoch
- Epoch status, which refers to the query fee collection and distribution and can have different states:
  - The active epoch is the one in which Indexers are currently allocating stake and collecting query fees
  - The settling epochs are the ones in which the state channels are being settled. This means that the Indexers are subject to slashing if the consumers open disputes against them.
  - The distributing epochs are the epochs in which the state channels for the epochs are being settled and Indexers can claim their query fee rebates.
  - The finalized epochs are the epochs that have no query fee rebates left to claim by the Indexers.

![Explorer Image 9](/img/Epoch-Stats.png)

## Your User Profile

Your personal profile is the place where you can see your network activity, regardless of your role on the network. Your crypto wallet will act as your user profile, and with the User Dashboard, you’ll be able to see the following tabs:

### Profile Overview

In this section, you can view the following:

- Any of your current actions you've done.
- Your profile information, description, and website (if you added one).

![Explorer Image 10](/img/Profile-Overview.png)

### Subgraphs Tab

In the Subgraphs tab, you’ll see your published subgraphs.

> This will not include any subgraphs deployed with the CLI for testing purposes. Subgraphs will only show up when they are published to the decentralized network.

![Explorer Image 11](/img/Subgraphs-Overview.png)

### Indexing Tab

In the Indexing tab, you’ll find a table with all the active and historical allocations towards subgraphs. You will also find charts where you can see and analyze your past performance as an Indexer.

This section will also include details about your net Indexer rewards and net query fees. You’ll see the following metrics:

- Delegated Stake - the stake from Delegators that can be allocated by you but cannot be slashed
- Total Query Fees - the total fees that users have paid for queries served by you over time
- Indexer Rewards - the total amount of Indexer rewards you have received, in GRT
- Fee Cut - the % of query fee rebates that you will keep when you split with Delegators
- Rewards Cut - the % of Indexer rewards that you will keep when splitting with Delegators
- Owned - your deposited stake, which could be slashed for malicious or incorrect behavior

![Explorer Image 12](/img/Indexer-Stats.png)

### Delegating Tab

Delegators are important to the Graph Network. They must use their knowledge to choose an Indexer that will provide a healthy return on rewards.

In the Delegators tab, you can find the details of your active and historical delegations, along with the metrics of the Indexers that you delegated towards.

In the first half of the page, you can see your delegation chart, as well as the rewards-only chart. To the left, you can see the KPIs that reflect your current delegation metrics.

The Delegator metrics you’ll see here in this tab include:

- Total delegation rewards
- Total unrealized rewards
- Total realized rewards

In the second half of the page, you have the delegations table. Here you can see the Indexers that you delegated towards, as well as their details (such as rewards cuts, cooldown, etc).

With the buttons on the right side of the table, you can manage your delegation - delegate more, undelegate, or withdraw your delegation after the thawing period.

Keep in mind that this chart is horizontally scrollable, so if you scroll all the way to the right, you can also see the status of your delegation (delegating, undelegating, withdrawable).

![Explorer Image 13](/img/Delegation-Stats.png)

### Curating Tab

In the Curation tab, you’ll find all the subgraphs you’re signaling on (thus enabling you to receive query fees). Signaling allows Curators to highlight to Indexers which subgraphs are valuable and trustworthy, thus signaling that they need to be indexed on.

Within this tab, you’ll find an overview of:

- All the subgraphs you're curating on with signal details
- Share totals per subgraph
- Query rewards per subgraph
- Updated at date details

![Explorer Image 14](/img/Curation-Stats.png)

## Your Profile Settings

Within your user profile, you’ll be able to manage your personal profile details (like setting up an ENS name). If you’re an Indexer, you have even more access to settings at your fingertips. In your user profile, you’ll be able to set up your delegation parameters and operators.

- Operators take limited actions in the protocol on the Indexer's behalf, such as opening and closing allocations. Operators are typically other Ethereum addresses, separate from their staking wallet, with gated access to the network that Indexers can personally set
- Delegation parameters allow you to control the distribution of GRT between you and your Delegators.

![Explorer Image 15](/img/Profile-Settings.png)

As your official portal into the world of decentralized data, Graph Explorer allows you to take a variety of actions, no matter your role in the network. You can get to your profile settings by opening the dropdown menu next to your address, then clicking on the Settings button.

<div sx={{ mx: 'auto', maxWidth: '400px' }}>![Wallet details](/img/Wallet-Details.png)</div>
---
title: Protocol Contracts
---

import { ProtocolContractsTable } from '@/src/contracts'

Below are the deployed contracts which power The Graph Network. Visit the official [contracts repository](https://github.com/graphprotocol/contracts) to learn more.

## Arbitrum

This is the principal deployment of The Graph Network.

<ProtocolContractsTable networkId={42161} />

## Mainnet

This was the original deployment of The Graph Network. [Learn more](/arbitrum/arbitrum-faq) about The Graph's scaling with Arbitrum.

<ProtocolContractsTable networkId={1} />

## Arbitrum Sepolia

This is the primary testnet for The Graph Network. Testnet is predominantly used by core developers and ecosystem participants for testing purposes. There are no guarantees of service or availability on The Graph's testnets.

<ProtocolContractsTable networkId={421614} />

## Sepolia

<ProtocolContractsTable networkId={11155111} />
---
title: The Graph Network vs. Self Hosting
socialImage: https://thegraph.com/docs/img/seo/benefits.jpg
---

The Graph’s decentralized network has been engineered and refined to create a robust indexing and querying experience—and it’s getting better every day thanks to thousands of contributors around the world.

The benefits of this decentralized protocol cannot be replicated by running a `graph-node` locally. The Graph Network is more reliable, more efficient, and less expensive.

Here is an analysis:

## Why You Should Use The Graph Network

- Significantly lower monthly costs
- $0 infrastructure setup costs
- Superior uptime
- Access to hundreds of independent Indexers around the world
- 24/7 technical support by global community

## The Benefits Explained

### Lower & more Flexible Cost Structure

No contracts. No monthly fees. Only pay for the queries you use—with an average cost-per-query of $40 per million queries (~$0.00004 per query). Queries are priced in USD and paid in GRT or credit card.

Query costs may vary; the quoted cost is the average at time of publication (March 2024).

## Low Volume User (less than 100,000 queries per month)

| Cost Comparison | Self Hosted | The Graph Network |
| :-: | :-: | :-: |
| Monthly server cost\* | $350 per month | $0 |
| Query costs | $0+ | $0 per month |
| Engineering time<sup>†</sup> | $400 per month | None, built into the network with globally distributed Indexers |
| Queries per month | Limited to infra capabilities | 100,000 (Free Plan) |
| Cost per query | $0 | $0<sup>‡</sup> |
| Infrastructure | Centralized | Decentralized |
| Geographic redundancy | $750+ per additional node | Included |
| Uptime | Varies | 99.9%+ |
| Total Monthly Costs | <span className="highlight-row" />$750+ | $0 |

## Medium Volume User (~3M queries per month)

| Cost Comparison | Self Hosted | The Graph Network |
| :-: | :-: | :-: |
| Monthly server cost\* | $350 per month | $0 |
| Query costs | $500 per month | $120 per month |
| Engineering time<sup>†</sup> | $800 per month | None, built into the network with globally distributed Indexers |
| Queries per month | Limited to infra capabilities | ~3,000,000 |
| Cost per query | $0 | $0.00004 |
| Infrastructure | Centralized | Decentralized |
| Engineering expense | $200 per hour | Included |
| Geographic redundancy | $1,200 in total costs per additional node | Included |
| Uptime | Varies | 99.9%+ |
| Total Monthly Costs | <span className="highlight-row" /> $1,650+ | $120 |

## High Volume User (~30M queries per month)

| Cost Comparison | Self Hosted | The Graph Network |
| :-: | :-: | :-: |
| Monthly server cost\* | $1100 per month, per node | $0 |
| Query costs | $4000 | $1,200 per month |
| Number of nodes needed | 10 | Not applicable |
| Engineering time<sup>†</sup> | $6,000 or more per month | None, built into the network with globally distributed Indexers |
| Queries per month | Limited to infra capabilities | ~30,000,000 |
| Cost per query | $0 | $0.00004 |
| Infrastructure | Centralized | Decentralized |
| Geographic redundancy | $1,200 in total costs per additional node | Included |
| Uptime | Varies | 99.9%+ |
| Total Monthly Costs | <span className="highlight-row" /> $11,000+ | $1,200 |

\*including costs for backup: $50-$100 per month

<sup>†</sup>Engineering time based on $200 per hour assumption

<sup>‡</sup>Reflects cost for data consumer. Query fees are still paid to Indexers for Free Plan queries.

Estimated costs are only for Ethereum Mainnet subgraphs — costs are even higher when self hosting a `graph-node` on other networks. Some users may need to update their subgraph to a new version. Due to Ethereum gas fees, an update costs ~$50 at time of writing. Note that gas fees on [Arbitrum](/arbitrum/arbitrum-faq) are substantially lower than Ethereum mainnet.

Curating signal on a subgraph is an optional one-time, net-zero cost (e.g., $1k in signal can be curated on a subgraph, and later withdrawn—with potential to earn returns in the process).

## No Setup Costs & Greater Operational Efficiency

Zero setup fees. Get started immediately with no setup or overhead costs. No hardware requirements. No outages due to centralized infrastructure, and more time to concentrate on your core product . No need for backup servers, troubleshooting, or expensive engineering resources.

## Reliability & Resiliency

The Graph’s decentralized network gives users access to geographic redundancy that does not exist when self-hosting a `graph-node`. Queries are served reliably thanks to 99.9%+ uptime, achieved by hundreds of independent Indexers securing the network globally.

Bottom line: The Graph Network is less expensive, easier to use, and produces superior results compared to running a `graph-node` locally.

Start using The Graph Network today, and learn how to [upgrade your subgraph to The Graph's decentralized network](/cookbook/upgrading-a-subgraph).
---
title: Indexing
---

Indexers are node operators in The Graph Network that stake Graph Tokens (GRT) in order to provide indexing and query processing services. Indexers earn query fees and indexing rewards for their services. They also earn query fees that are rebated according to an exponential rebate function.

GRT that is staked in the protocol is subject to a thawing period and can be slashed if Indexers are malicious and serve incorrect data to applications or if they index incorrectly. Indexers also earn rewards for delegated stake from Delegators, to contribute to the network.

Indexers select subgraphs to index based on the subgraph’s curation signal, where Curators stake GRT in order to indicate which subgraphs are high-quality and should be prioritized. Consumers (eg. applications) can also set parameters for which Indexers process queries for their subgraphs and set preferences for query fee pricing.

<Difficulty level="ADVANCED" />

## FAQ

### What is the minimum stake required to be an Indexer on the network?

The minimum stake for an Indexer is currently set to 100K GRT.

### What are the revenue streams for an Indexer?

**Query fee rebates** - Payments for serving queries on the network. These payments are mediated via state channels between an Indexer and a gateway. Each query request from a gateway contains a payment and the corresponding response a proof of query result validity.

**Indexing rewards** - Generated via a 3% annual protocol wide inflation, the indexing rewards are distributed to Indexers who are indexing subgraph deployments for the network.

### How are indexing rewards distributed?

Indexing rewards come from protocol inflation which is set to 3% annual issuance. They are distributed across subgraphs based on the proportion of all curation signal on each, then distributed proportionally to Indexers based on their allocated stake on that subgraph. **An allocation must be closed with a valid proof of indexing (POI) that meets the standards set by the arbitration charter in order to be eligible for rewards.**

Numerous tools have been created by the community for calculating rewards; you'll find a collection of them organized in the [Community Guides collection](https://www.notion.so/Community-Guides-abbb10f4dba040d5ba81648ca093e70c). You can also find an up to date list of tools in the #Delegators and #Indexers channels on the [Discord server](https://discord.gg/graphprotocol). Here we link a [recommended allocation optimiser](https://github.com/graphprotocol/allocation-optimizer) integrated with the indexer software stack.

### What is a proof of indexing (POI)?

POIs are used in the network to verify that an Indexer is indexing the subgraphs they have allocated on. A POI for the first block of the current epoch must be submitted when closing an allocation for that allocation to be eligible for indexing rewards. A POI for a block is a digest for all entity store transactions for a specific subgraph deployment up to and including that block.

### When are indexing rewards distributed?

Allocations are continuously accruing rewards while they're active and allocated within 28 epochs. Rewards are collected by the Indexers, and distributed whenever their allocations are closed. That happens either manually, whenever the Indexer wants to force close them, or after 28 epochs a Delegator can close the allocation for the Indexer, but this results in no rewards. 28 epochs is the max allocation lifetime (right now, one epoch lasts for ~24h).

### Can pending indexing rewards be monitored?

The RewardsManager contract has a read-only [getRewards](https://github.com/graphprotocol/contracts/blob/main/packages/contracts/contracts/rewards/RewardsManager.sol#L316) function that can be used to check the pending rewards for a specific allocation.

Many of the community-made dashboards include pending rewards values and they can be easily checked manually by following these steps:

1. Query the [mainnet subgraph](https://thegraph.com/explorer/subgraphs/9Co7EQe5PgW3ugCUJrJgRv4u9zdEuDJf8NvMWftNsBH8?view=Query&chain=arbitrum-one) to get the IDs for all active allocations:

```graphql
query indexerAllocations {
  indexer(id: "<INDEXER_ADDRESS>") {
    allocations {
      activeForIndexer {
        allocations {
          id
        }
      }
    }
  }
}
```

Use Etherscan to call `getRewards()`:

- Navigate to [Etherscan interface to Rewards contract](https://etherscan.io/address/0x9Ac758AB77733b4150A901ebd659cbF8cB93ED66#readProxyContract)

* To call `getRewards()`:
  - Expand the **9. getRewards** dropdown.
  - Enter the **allocationID** in the input.
  - Click the **Query** button.

### What are disputes and where can I view them?

Indexer's queries and allocations can both be disputed on The Graph during the dispute period. The dispute period varies, depending on the type of dispute. Queries/attestations have 7 epochs dispute window, whereas allocations have 56 epochs. After these periods pass, disputes cannot be opened against either of allocations or queries. When a dispute is opened, a deposit of a minimum of 10,000 GRT is required by the Fishermen, which will be locked until the dispute is finalized and a resolution has been given. Fisherman are any network participants that open disputes.

Disputes have **three** possible outcomes, so does the deposit of the Fishermen.

- If the dispute is rejected, the GRT deposited by the Fishermen will be burned, and the disputed Indexer will not be slashed.
- If the dispute is settled as a draw, the Fishermen's deposit will be returned, and the disputed Indexer will not be slashed.
- If the dispute is accepted, the GRT deposited by the Fishermen will be returned, the disputed Indexer will be slashed and the Fishermen will earn 50% of the slashed GRT.

Disputes can be viewed in the UI in an Indexer's profile page under the `Disputes` tab.

### What are query fee rebates and when are they distributed?

Query fees are collected by the gateway and distributed to indexers according to the exponential rebate function (see GIP [here](https://forum.thegraph.com/t/gip-0051-exponential-query-fee-rebates-for-indexers/4162)). The exponential rebate function is proposed as a way to ensure indexers achieve the best outcome by faithfully serving queries. It works by incentivizing Indexers to allocate a large amount of stake (which can be slashed for erring when serving a query) relative to the amount of query fees they may collect.

Once an allocation has been closed the rebates are available to be claimed by the Indexer. Upon claiming, the query fee rebates are distributed to the Indexer and their Delegators based on the query fee cut and the exponential rebate function.

### What is query fee cut and indexing reward cut?

The `queryFeeCut` and `indexingRewardCut` values are delegation parameters that the Indexer may set along with cooldownBlocks to control the distribution of GRT between the Indexer and their Delegators. See the last steps in [Staking in the Protocol](/network/indexing#stake-in-the-protocol) for instructions on setting the delegation parameters.

- **queryFeeCut** - the % of query fee rebates that will be distributed to the Indexer. If this is set to 95%, the Indexer will receive 95% of the query fees earned when an allocation is closed with the other 5% going to the Delegators.

- **indexingRewardCut** - the % of indexing rewards that will be distributed to the Indexer. If this is set to 95%, the Indexer will receive 95% of the indexing rewards when an allocation is closed and the Delegators will split the other 5%.

### How do Indexers know which subgraphs to index?

Indexers may differentiate themselves by applying advanced techniques for making subgraph indexing decisions but to give a general idea we'll discuss several key metrics used to evaluate subgraphs in the network:

- **Curation signal** - The proportion of network curation signal applied to a particular subgraph is a good indicator of the interest in that subgraph, especially during the bootstrap phase when query voluming is ramping up.

- **Query fees collected** - The historical data for volume of query fees collected for a specific subgraph is a good indicator of future demand.

- **Amount staked** - Monitoring the behavior of other Indexers or looking at proportions of total stake allocated towards specific subgraphs can allow an Indexer to monitor the supply side for subgraph queries to identify subgraphs that the network is showing confidence in or subgraphs that may show a need for more supply.

- **Subgraphs with no indexing rewards** - Some subgraphs do not generate indexing rewards mainly because they are using unsupported features like IPFS or because they are querying another network outside of mainnet. You will see a message on a subgraph if it is not generating indexing rewards.

### What are the hardware requirements?

- **Small** - Enough to get started indexing several subgraphs, will likely need to be expanded.
- **Standard** - Default setup, this is what is used in the example k8s/terraform deployment manifests.
- **Medium** - Production Indexer supporting 100 subgraphs and 200-500 requests per second.
- **Large** - Prepared to index all currently used subgraphs and serve requests for the related traffic.

| Setup | Postgres<br />(CPUs) | Postgres<br />(memory in GBs) | Postgres<br />(disk in TBs) | VMs<br />(CPUs) | VMs<br />(memory in GBs) |
| --- | :-: | :-: | :-: | :-: | :-: |
| Small | 4 | 8 | 1 | 4 | 16 |
| Standard | 8 | 30 | 1 | 12 | 48 |
| Medium | 16 | 64 | 2 | 32 | 64 |
| Large | 72 | 468 | 3.5 | 48 | 184 |

### What are some basic security precautions an Indexer should take?

- **Operator wallet** - Setting up an operator wallet is an important precaution because it allows an Indexer to maintain separation between their keys that control stake and those that are in control of day-to-day operations. See [Stake in Protocol](/network/indexing#stake-in-the-protocol) for instructions.

- **Firewall** - Only the Indexer service needs to be exposed publicly and particular attention should be paid to locking down admin ports and database access: the Graph Node JSON-RPC endpoint (default port: 8030), the Indexer management API endpoint (default port: 18000), and the Postgres database endpoint (default port: 5432) should not be exposed.

## Infrastructure

At the center of an Indexer's infrastructure is the Graph Node which monitors the indexed networks, extracts and loads data per a subgraph definition and serves it as a [GraphQL API](/about/#how-the-graph-works). The Graph Node needs to be connected to an endpoint exposing data from each indexed network; an IPFS node for sourcing data; a PostgreSQL database for its store; and Indexer components which facilitate its interactions with the network.

- **PostgreSQL database** - The main store for the Graph Node, this is where subgraph data is stored. The Indexer service and agent also use the database to store state channel data, cost models, indexing rules, and allocation actions.

- **Data endpoint** - For EVM-compatible networks, Graph Node needs to be connected to an endpoint that exposes an EVM-compatible JSON-RPC API. This may take the form of a single client or it could be a more complex setup that load balances across multiple. It's important to be aware that certain subgraphs will require particular client capabilities such as archive mode and/or the parity tracing API.

- **IPFS node (version less than 5)** - Subgraph deployment metadata is stored on the IPFS network. The Graph Node primarily accesses the IPFS node during subgraph deployment to fetch the subgraph manifest and all linked files. Network Indexers do not need to host their own IPFS node, an IPFS node for the network is hosted at https://ipfs.network.thegraph.com.

- **Indexer service** - Handles all required external communications with the network. Shares cost models and indexing statuses, passes query requests from gateways on to a Graph Node, and manages the query payments via state channels with the gateway.

- **Indexer agent** - Facilitates the Indexers interactions on chain including registering on the network, managing subgraph deployments to its Graph Node/s, and managing allocations.

- **Prometheus metrics server** - The Graph Node and Indexer components log their metrics to the metrics server.

Note: To support agile scaling, it is recommended that query and indexing concerns are separated between different sets of nodes: query nodes and index nodes.

### Ports overview

> **Important**: Be careful about exposing ports publicly - **administration ports** should be kept locked down. This includes the the Graph Node JSON-RPC and the Indexer management endpoints detailed below.

#### Graph Node

| Port | Purpose | Routes | CLI Argument | Environment Variable |
| --- | --- | --- | --- | --- |
| 8000 | GraphQL HTTP server<br />(for subgraph queries) | /subgraphs/id/...<br />/subgraphs/name/.../... | --http-port | - |
| 8001 | GraphQL WS<br />(for subgraph subscriptions) | /subgraphs/id/...<br />/subgraphs/name/.../... | --ws-port | - |
| 8020 | JSON-RPC<br />(for managing deployments) | / | --admin-port | - |
| 8030 | Subgraph indexing status API | /graphql | --index-node-port | - |
| 8040 | Prometheus metrics | /metrics | --metrics-port | - |

#### Indexer Service

| Port | Purpose | Routes | CLI Argument | Environment Variable |
| --- | --- | --- | --- | --- |
| 7600 | GraphQL HTTP server<br />(for paid subgraph queries) | /subgraphs/id/...<br />/status<br />/channel-messages-inbox | --port | `INDEXER_SERVICE_PORT` |
| 7300 | Prometheus metrics | /metrics | --metrics-port | - |

#### Indexer Agent

| Port | Purpose                | Routes | CLI Argument              | Environment Variable                    |
| ---- | ---------------------- | ------ | ------------------------- | --------------------------------------- |
| 8000 | Indexer management API | /      | --indexer-management-port | `INDEXER_AGENT_INDEXER_MANAGEMENT_PORT` |

### Setup server infrastructure using Terraform on Google Cloud

> Note: Indexers can alternatively use AWS, Microsoft Azure, or Alibaba.

#### Install prerequisites

- Google Cloud SDK
- Kubectl command line tool
- Terraform

#### Create a Google Cloud Project

- Clone or navigate to the [Indexer repository](https://github.com/graphprotocol/indexer).

- Navigate to the `./terraform` directory, this is where all commands should be executed.

```sh
cd terraform
```

- Authenticate with Google Cloud and create a new project.

```sh
gcloud auth login
project=<PROJECT_NAME>
gcloud projects create --enable-cloud-apis $project
```

- Use the Google Cloud Console's billing page to enable billing for the new project.

- Create a Google Cloud configuration.

```sh
proj_id=$(gcloud projects list --format='get(project_id)' --filter="name=$project")
gcloud config configurations create $project
gcloud config set project "$proj_id"
gcloud config set compute/region us-central1
gcloud config set compute/zone us-central1-a
```

- Enable required Google Cloud APIs.

```sh
gcloud services enable compute.googleapis.com
gcloud services enable container.googleapis.com
gcloud services enable servicenetworking.googleapis.com
gcloud services enable sqladmin.googleapis.com
```

- Create a service account.

```sh
svc_name=<SERVICE_ACCOUNT_NAME>
gcloud iam service-accounts create $svc_name \
  --description="Service account for Terraform" \
  --display-name="$svc_name"
gcloud iam service-accounts list
# Get the email of the service account from the list
svc=$(gcloud iam service-accounts list --format='get(email)'
--filter="displayName=$svc_name")
gcloud iam service-accounts keys create .gcloud-credentials.json \
  --iam-account="$svc"
gcloud projects add-iam-policy-binding $proj_id \
  --member serviceAccount:$svc \
  --role roles/editor
```

- Enable peering between database and Kubernetes cluster that will be created in the next step.

```sh
gcloud compute addresses create google-managed-services-default \
  --prefix-length=20 \
  --purpose=VPC_PEERING \
  --network default \
  --global \
  --description 'IP Range for peer networks.'
gcloud services vpc-peerings connect \
  --network=default \
  --ranges=google-managed-services-default
```

- Create minimal terraform configuration file (update as needed).

```sh
indexer=<INDEXER_NAME>
cat > terraform.tfvars <<EOF
project = "$proj_id"
indexer = "$indexer"
database_password = "<database passowrd>"
EOF
```

#### Use Terraform to create infrastructure

Before running any commands, read through [variables.tf](https://github.com/graphprotocol/indexer/blob/main/terraform/variables.tf) and create a file `terraform.tfvars` in this directory (or modify the one we created in the last step). For each variable where you want to override the default, or where you need to set a value, enter a setting into `terraform.tfvars`.

- Run the following commands to create the infrastructure.

```sh
# Install required plugins
terraform init

# View plan for resources to be created
terraform plan

# Create the resources (expect it to take up to 30 minutes)
terraform apply
```

Download credentials for the new cluster into `~/.kube/config` and set it as your default context.

```sh
gcloud container clusters get-credentials $indexer
kubectl config use-context $(kubectl config get-contexts --output='name'
| grep $indexer)
```

#### Creating the Kubernetes components for the Indexer

- Copy the directory `k8s/overlays` to a new directory `$dir,` and adjust the `bases` entry in `$dir/kustomization.yaml` so that it points to the directory `k8s/base`.

- Read through all the files in `$dir` and adjust any values as indicated in the comments.

Deploy all resources with `kubectl apply -k $dir`.

### Graph Node

[Graph Node](https://github.com/graphprotocol/graph-node) is an open source Rust implementation that event sources the Ethereum blockchain to deterministically update a data store that can be queried via the GraphQL endpoint. Developers use subgraphs to define their schema, and a set of mappings for transforming the data sourced from the blockchain and the Graph Node handles syncing the entire chain, monitoring for new blocks, and serving it via a GraphQL endpoint.

#### Getting started from source

#### Install prerequisites

- **Rust**

- **PostgreSQL**

- **IPFS**

- **Additional Requirements for Ubuntu users** - To run a Graph Node on Ubuntu a few additional packages may be needed.

```sh
sudo apt-get install -y clang libpg-dev libssl-dev pkg-config
```

#### Setup

1. Start a PostgreSQL database server

```sh
initdb -D .postgres
pg_ctl -D .postgres -l logfile start
createdb graph-node
```

2. Clone [Graph Node](https://github.com/graphprotocol/graph-node) repo and build the source by running `cargo build`

3. Now that all the dependencies are setup, start the Graph Node:

```sh
cargo run -p graph-node --release -- \
  --postgres-url postgresql://[USERNAME]:[PASSWORD]@localhost:5432/graph-node \
  --ethereum-rpc [NETWORK_NAME]:[URL] \
  --ipfs https://ipfs.network.thegraph.com
```

#### Getting started using Docker

#### Prerequisites

- **Ethereum node** - By default, the docker compose setup will use mainnet: [http://host.docker.internal:8545](http://host.docker.internal:8545) to connect to the Ethereum node on your host machine. You can replace this network name and url by updating `docker-compose.yaml`.

#### Setup

1. Clone Graph Node and navigate to the Docker directory:

```sh
git clone https://github.com/graphprotocol/graph-node
cd graph-node/docker
```

2. For linux users only - Use the host IP address instead of `host.docker.internal` in the `docker-compose.yaml `using the included script:

```sh
./setup.sh
```

3. Start a local Graph Node that will connect to your Ethereum endpoint:

```sh
docker-compose up
```

### Indexer components

To successfully participate in the network requires almost constant monitoring and interaction, so we've built a suite of Typescript applications for facilitating an Indexers network participation. There are three Indexer components:

- **Indexer agent** - The agent monitors the network and the Indexer's own infrastructure and manages which subgraph deployments are indexed and allocated towards on chain and how much is allocated towards each.

- **Indexer service** - The only component that needs to be exposed externally, the service passes on subgraph queries to the graph node, manages state channels for query payments, shares important decision making information to clients like the gateways.

- **Indexer CLI** - The command line interface for managing the Indexer agent. It allows Indexers to manage cost models, manual allocations, actions queue, and indexing rules.

#### Getting started

The Indexer agent and Indexer service should be co-located with your Graph Node infrastructure. There are many ways to set up virtual execution environments for your Indexer components; here we'll explain how to run them on baremetal using NPM packages or source, or via kubernetes and docker on the Google Cloud Kubernetes Engine. If these setup examples do not translate well to your infrastructure there will likely be a community guide to reference, come say hi on [Discord](https://discord.gg/graphprotocol)! Remember to [stake in the protocol](/network/indexing#stake-in-the-protocol) before starting up your Indexer components!

#### From NPM packages

```sh
npm install -g @graphprotocol/indexer-service
npm install -g @graphprotocol/indexer-agent

# Indexer CLI is a plugin for Graph CLI, so both need to be installed:
npm install -g @graphprotocol/graph-cli
npm install -g @graphprotocol/indexer-cli

# Indexer service
graph-indexer-service start ...

# Indexer agent
graph-indexer-agent start ...

# Indexer CLI
#Forward the port of your agent pod if using Kubernetes
kubectl port-forward pod/POD_ID 18000:8000
graph indexer connect http://localhost:18000/
graph indexer ...
```

#### From source

```sh
# From Repo root directory
yarn

# Indexer Service
cd packages/indexer-service
./bin/graph-indexer-service start ...

# Indexer agent
cd packages/indexer-agent
./bin/graph-indexer-service start ...

# Indexer CLI
cd packages/indexer-cli
./bin/graph-indexer-cli indexer connect http://localhost:18000/
./bin/graph-indexer-cli indexer ...
```

#### Using docker

- Pull images from the registry

```sh
docker pull ghcr.io/graphprotocol/indexer-service:latest
docker pull ghcr.io/graphprotocol/indexer-agent:latest
```

Or build images locally from source

```sh
# Indexer service
docker build \
  --build-arg NPM_TOKEN=<npm-token> \
  -f Dockerfile.indexer-service \
  -t indexer-service:latest \
# Indexer agent
docker build \
  --build-arg NPM_TOKEN=<npm-token> \
  -f Dockerfile.indexer-agent \
  -t indexer-agent:latest \
```

- Run the components

```sh
docker run -p 7600:7600 -it indexer-service:latest ...
docker run -p 18000:8000 -it indexer-agent:latest ...
```

**NOTE**: After starting the containers, the Indexer service should be accessible at [http://localhost:7600](http://localhost:7600) and the Indexer agent should be exposing the Indexer management API at [http://localhost:18000/](http://localhost:18000/).

#### Using K8s and Terraform

See the [Setup Server Infrastructure Using Terraform on Google Cloud](/network/indexing#setup-server-infrastructure-using-terraform-on-google-cloud) section

#### Usage

> **NOTE**: All runtime configuration variables may be applied either as parameters to the command on startup or using environment variables of the format `COMPONENT_NAME_VARIABLE_NAME`(ex. `INDEXER_AGENT_ETHEREUM`).

#### Indexer agent

```sh
graph-indexer-agent start \
  --ethereum <MAINNET_ETH_ENDPOINT> \
  --ethereum-network mainnet \
  --mnemonic <MNEMONIC> \
  --indexer-address <INDEXER_ADDRESS> \
  --graph-node-query-endpoint http://localhost:8000/ \
  --graph-node-status-endpoint http://localhost:8030/graphql \
  --graph-node-admin-endpoint http://localhost:8020/ \
  --public-indexer-url http://localhost:7600/ \
  --indexer-geo-coordinates <YOUR_COORDINATES> \
  --index-node-ids default \
  --indexer-management-port 18000 \
  --metrics-port 7040 \
  --network-subgraph-endpoint https://gateway.network.thegraph.com/network \
  --default-allocation-amount 100 \
  --register true \
  --inject-dai true \
  --postgres-host localhost \
  --postgres-port 5432 \
  --postgres-username <DB_USERNAME> \
  --postgres-password <DB_PASSWORD> \
  --postgres-database indexer \
  --allocation-management auto \
  | pino-pretty
```

#### Indexer service

```sh
SERVER_HOST=localhost \
SERVER_PORT=5432 \
SERVER_DB_NAME=is_staging \
SERVER_DB_USER=<DB_USERNAME> \
SERVER_DB_PASSWORD=<DB_PASSWORD> \
graph-indexer-service start \
  --ethereum <MAINNET_ETH_ENDPOINT> \
  --ethereum-network mainnet \
  --mnemonic <MNEMONIC> \
  --indexer-address <INDEXER_ADDRESS> \
  --port 7600 \
  --metrics-port 7300 \
  --graph-node-query-endpoint http://localhost:8000/ \
  --graph-node-status-endpoint http://localhost:8030/graphql \
  --postgres-host localhost \
  --postgres-port 5432 \
  --postgres-username <DB_USERNAME> \
  --postgres-password <DB_PASSWORD> \
  --postgres-database is_staging \
  --network-subgraph-endpoint https://gateway.network.thegraph.com/network \
  | pino-pretty
```

#### Indexer CLI

The Indexer CLI is a plugin for [`@graphprotocol/graph-cli`](https://www.npmjs.com/package/@graphprotocol/graph-cli) accessible in the terminal at `graph indexer`.

```sh
graph indexer connect http://localhost:18000
graph indexer status
```

#### Indexer management using Indexer CLI

The suggested tool for interacting with the **Indexer Management API** is the **Indexer CLI**, an extension to the **Graph CLI**. The Indexer agent needs input from an Indexer in order to autonomously interact with the network on the behalf of the Indexer. The mechanism for defining Indexer agent behavior are **allocation management** mode and **indexing rules**. Under auto mode, an Indexer can use **indexing rules** to apply their specific strategy for picking subgraphs to index and serve queries for. Rules are managed via a GraphQL API served by the agent and known as the Indexer Management API. Under manual mode, an Indexer can create allocation actions using **actions queue** and explicitly approve them before they get executed. Under oversight mode, **indexing rules** are used to populate **actions queue** and also require explicit approval for execution.

#### Usage

The **Indexer CLI** connects to the Indexer agent, typically through port-forwarding, so the CLI does not need to run on the same server or cluster. To help you get started, and to provide some context, the CLI will briefly be described here.

- `graph indexer connect <url>` - Connect to the Indexer management API. Typically the connection to the server is opened via port forwarding, so the CLI can be easily operated remotely. (Example: `kubectl port-forward pod/<indexer-agent-pod> 8000:8000`)

- `graph indexer rules get [options] <deployment-id> [<key1> ...]` - Get one or more indexing rules using `all` as the `<deployment-id>` to get all rules, or `global` to get the global defaults. An additional argument `--merged` can be used to specify that deployment specific rules are merged with the global rule. This is how they are applied in the Indexer agent.

- `graph indexer rules set [options] <deployment-id> <key1> <value1> ...` - Set one or more indexing rules.

- `graph indexer rules start [options] <deployment-id>` - Start indexing a subgraph deployment if available and set its `decisionBasis` to `always`, so the Indexer agent will always choose to index it. If the global rule is set to always then all available subgraphs on the network will be indexed.

- `graph indexer rules stop [options] <deployment-id>` - Stop indexing a deployment and set its `decisionBasis` to never, so it will skip this deployment when deciding on deployments to index.

- `graph indexer rules maybe [options] <deployment-id>` — Set the `decisionBasis` for a deployment to `rules`, so that the Indexer agent will use indexing rules to decide whether to index this deployment.

- `graph indexer actions get [options] <action-id>` - Fetch one or more actions using `all` or leave `action-id` empty to get all actions. An additional argument `--status` can be used to print out all actions of a certain status.

- `graph indexer action queue allocate <deployment-id> <allocation-amount>` - Queue allocation action

- `graph indexer action queue reallocate <deployment-id> <allocation-id> <allocationAmount>` - Queue reallocate action

- `graph indexer action queue unallocate <deployment-id> <allocation-id>` - Queue unallocate action

- `graph indexer actions cancel [<action-id> ...]` - Cancel all action in the queue if id is unspecified, otherwise cancel array of id with space as separator

- `graph indexer actions approve [<action-id> ...]` - Approve multiple actions for execution

- `graph indexer actions execute approve` - Force the worker to execute approved actions immediately

All commands which display rules in the output can choose between the supported output formats (`table`, `yaml`, and `json`) using the `-output` argument.

#### Indexing rules

Indexing rules can either be applied as global defaults or for specific subgraph deployments using their IDs. The `deployment` and `decisionBasis` fields are mandatory, while all other fields are optional. When an indexing rule has `rules` as the `decisionBasis`, then the Indexer agent will compare non-null threshold values on that rule with values fetched from the network for the corresponding deployment. If the subgraph deployment has values above (or below) any of the thresholds it will be chosen for indexing.

For example, if the global rule has a `minStake` of **5** (GRT), any subgraph deployment which has more than 5 (GRT) of stake allocated to it will be indexed. Threshold rules include `maxAllocationPercentage`, `minSignal`, `maxSignal`, `minStake`, and `minAverageQueryFees`.

Data model:

```graphql
type IndexingRule {
    identifier: string
    identifierType: IdentifierType
    decisionBasis: IndexingDecisionBasis!
    allocationAmount: number | null
    allocationLifetime: number | null
    autoRenewal: boolean
    parallelAllocations: number | null
    maxAllocationPercentage: number | null
    minSignal: string | null
    maxSignal: string | null
    minStake: string | null
    minAverageQueryFees: string | null
    custom: string | null
    requireSupported: boolean | null
  }

IdentifierType {
  deployment
  subgraph
  group
}

IndexingDecisionBasis {
  rules
  never
  always
  offchain
}
```

Example usage of indexing rule:

```
graph indexer rules offchain QmZfeJYR86UARzp9HiXbURWunYgC9ywvPvoePNbuaATrEK

graph indexer rules set QmZfeJYR86UARzp9HiXbURWunYgC9ywvPvoePNbuaATrEK decisionBasis always allocationAmount 123321 allocationLifetime 14 autoRenewal false requireSupported false

graph indexer rules stop QmZfeJYR86UARzp9HiXbURWunYgC9ywvPvoePNbuaATrEK

graph indexer rules delete QmZfeJYR86UARzp9HiXbURWunYgC9ywvPvoePNbuaATrEK
```

#### Actions queue CLI

The indexer-cli provides an `actions` module for manually working with the action queue. It uses the **Graphql API** hosted by the indexer management server to interact with the actions queue.

The action execution worker will only grab items from the queue to execute if they have `ActionStatus = approved`. In the recommended path actions are added to the queue with ActionStatus = queued, so they must then be approved in order to be executed on-chain. The general flow will look like:

- Action added to the queue by the 3rd party optimizer tool or indexer-cli user
- Indexer can use the `indexer-cli` to view all queued actions
- Indexer (or other software) can approve or cancel actions in the queue using the `indexer-cli`. The approve and cancel commands take an array of action ids as input.
- The execution worker regularly polls the queue for approved actions. It will grab the `approved` actions from the queue, attempt to execute them, and update the values in the db depending on the status of execution to `success` or `failed`.
- If an action is successful the worker will ensure that there is an indexing rule present that tells the agent how to manage the allocation moving forward, useful when taking manual actions while the agent is in `auto` or `oversight` mode.
- The indexer can monitor the action queue to see a history of action execution and if needed re-approve and update action items if they failed execution. The action queue provides a history of all actions queued and taken.

Data model:

```graphql
Type ActionInput {
    status: ActionStatus
    type: ActionType
    deploymentID: string | null
    allocationID: string | null
    amount: string | null
    poi: string | null
    force: boolean | null
    source: string
    reason: string | null
    priority: number | null
}

ActionStatus {
  queued
  approved
  pending
  success
  failed
  canceled
}

ActionType {
  allocate
  unallocate
  reallocate
  collect
}
```

Example usage from source:

```bash
graph indexer actions get all

graph indexer actions get --status queued

graph indexer actions queue allocate QmeqJ6hsdyk9dVbo1tvRgAxWrVS3rkERiEMsxzPShKLco6 5000

graph indexer actions queue reallocate QmeqJ6hsdyk9dVbo1tvRgAxWrVS3rkERiEMsxzPShKLco6 0x4a58d33e27d3acbaecc92c15101fbc82f47c2ae5 55000

graph indexer actions queue unallocate QmeqJ6hsdyk9dVbo1tvRgAxWrVS3rkERiEMsxzPShKLco6 0x4a58d33e27d3acbaecc92c15101fbc82f47c2ae

graph indexer actions cancel

graph indexer actions approve 1 3 5

graph indexer actions execute approve
```

Note that supported action types for allocation management have different input requirements:

- `Allocate` - allocate stake to a specific subgraph deployment

  - required action params:
    - deploymentID
    - amount

- `Unallocate` - close allocation, freeing up the stake to reallocate elsewhere

  - required action params:
    - allocationID
    - deploymentID
  - optional action params:
    - poi
    - force (forces using the provided POI even if it doesn’t match what the graph-node provides)

- `Reallocate` - atomically close allocation and open a fresh allocation for the same subgraph deployment

  - required action params:
    - allocationID
    - deploymentID
    - amount
  - optional action params:
    - poi
    - force (forces using the provided POI even if it doesn’t match what the graph-node provides)

#### Cost models

Cost models provide dynamic pricing for queries based on market and query attributes. The Indexer Service shares a cost model with the gateways for each subgraph for which they intend to respond to queries. The gateways, in turn, use the cost model to make Indexer selection decisions per query and to negotiate payment with chosen Indexers.

#### Agora

The Agora language provides a flexible format for declaring cost models for queries. An Agora price model is a sequence of statements that execute in order for each top-level query in a GraphQL query. For each top-level query, the first statement which matches it determines the price for that query.

A statement is comprised of a predicate, which is used for matching GraphQL queries, and a cost expression which when evaluated outputs a cost in decimal GRT. Values in the named argument position of a query may be captured in the predicate and used in the expression. Globals may also be set and substituted in for placeholders in an expression.

Example cost model:

```
# This statement captures the skip value,
# uses a boolean expression in the predicate to match specific queries that use `skip`
# and a cost expression to calculate the cost based on the `skip` value and the SYSTEM_LOAD global
query { pairs(skip: $skip) { id } } when $skip > 2000 => 0.0001 * $skip * $SYSTEM_LOAD;

# This default will match any GraphQL expression.
# It uses a Global substituted into the expression to calculate cost
default => 0.1 * $SYSTEM_LOAD;
```

Example query costing using the above model:

| Query                                                                        | Price   |
| ---------------------------------------------------------------------------- | ------- |
| &#123; pairs(skip: 5000) &#123; id &#125; &#125;                             | 0.5 GRT |
| &#123; tokens &#123; symbol &#125; &#125;                                    | 0.1 GRT |
| &#123; pairs(skip: 5000) &#123; id &#125; tokens &#123; symbol &#125; &#125; | 0.6 GRT |

#### Applying the cost model

Cost models are applied via the Indexer CLI, which passes them to the Indexer Management API of the Indexer agent for storing in the database. The Indexer Service will then pick them up and serve the cost models to gateways whenever they ask for them.

```sh
indexer cost set variables '{ "SYSTEM_LOAD": 1.4 }'
indexer cost set model my_model.agora
```

## Interacting with the network

### Stake in the protocol

The first steps to participating in the network as an Indexer are to approve the protocol, stake funds, and (optionally) set up an operator address for day-to-day protocol interactions.

> Note: For the purposes of these instructions Remix will be used for contract interaction, but feel free to use your tool of choice ([OneClickDapp](https://oneclickdapp.com/), [ABItopic](https://abitopic.io/), and [MyCrypto](https://www.mycrypto.com/account) are a few other known tools).

Once an Indexer has staked GRT in the protocol, the [Indexer components](/network/indexing#indexer-components) can be started up and begin their interactions with the network.

#### Approve tokens

1. Open the [Remix app](https://remix.ethereum.org/) in a browser

2. In the `File Explorer` create a file named **GraphToken.abi** with the [token ABI](https://raw.githubusercontent.com/graphprotocol/contracts/mainnet-deploy-build/build/abis/GraphToken.json).

3. With `GraphToken.abi` selected and open in the editor, switch to the `Deploy and run transactions` section in the Remix interface.

4. Under environment select `Injected Web3` and under `Account` select your Indexer address.

5. Set the GraphToken contract address - Paste the GraphToken contract address (`0xc944E90C64B2c07662A292be6244BDf05Cda44a7`) next to `At Address` and click the `At address` button to apply.

6. Call the `approve(spender, amount)` function to approve the Staking contract. Fill in `spender` with the Staking contract address (`0xF55041E37E12cD407ad00CE2910B8269B01263b9`) and `amount` with the tokens to stake (in wei).

#### Stake tokens

1. Open the [Remix app](https://remix.ethereum.org/) in a browser

2. In the `File Explorer` create a file named **Staking.abi** with the staking ABI.

3. With `Staking.abi` selected and open in the editor, switch to the `Deploy and run transactions` section in the Remix interface.

4. Under environment select `Injected Web3` and under `Account` select your Indexer address.

5. Set the Staking contract address - Paste the Staking contract address (`0xF55041E37E12cD407ad00CE2910B8269B01263b9`) next to `At Address` and click the `At address` button to apply.

6. Call `stake()` to stake GRT in the protocol.

7. (Optional) Indexers may approve another address to be the operator for their Indexer infrastructure in order to separate the keys that control the funds from those that are performing day to day actions such as allocating on subgraphs and serving (paid) queries. In order to set the operator call `setOperator()` with the operator address.

8. (Optional) In order to control the distribution of rewards and strategically attract Delegators Indexers can update their delegation parameters by updating their indexingRewardCut (parts per million), queryFeeCut (parts per million), and cooldownBlocks (number of blocks). To do so call `setDelegationParameters()`. The following example sets the queryFeeCut to distribute 95% of query rebates to the Indexer and 5% to Delegators, set the indexingRewardCutto distribute 60% of indexing rewards to the Indexer and 40% to Delegators, and set `thecooldownBlocks` period to 500 blocks.

```
setDelegationParameters(950000, 600000, 500)
```

### Setting delegation parameters

The `setDelegationParameters()` function in the [staking contract](https://github.com/graphprotocol/contracts/blob/main/packages/contracts/contracts/staking/Staking.sol) is essential for Indexers, allowing them to set parameters that define their interactions with Delegators, influencing their reward sharing and delegation capacity.

### How to set delegation parameters

To set the delegation parameters using Graph Explorer interface, follow these steps:

1. Navigate to [Graph Explorer](https://thegraph.com/explorer/).
2. Connect your wallet. Choose multisig (such as Gnosis Safe) and then select mainnet. Note: You will need to repeat this process for Arbitrum One.
3. Connect the wallet you have as a signer.
4. Navigate to the 'Settings' section and select 'Delegation Parameters'. These parameters should be configured to achieve an effective cut within the desired range. Upon entering values in the provided input fields, the interface will automatically calculate the effective cut. Adjust these values as necessary to attain the desired effective cut percentage.
5. Submit the transaction to the network.

> Note: This transaction will need to be confirmed by the multisig wallet signers.

### The life of an allocation

After being created by an Indexer a healthy allocation goes through four states.

- **Active** - Once an allocation is created on-chain ([allocateFrom()](https://github.com/graphprotocol/contracts/blob/main/packages/contracts/contracts/staking/Staking.sol#L316)) it is considered **active**. A portion of the Indexer's own and/or delegated stake is allocated towards a subgraph deployment, which allows them to claim indexing rewards and serve queries for that subgraph deployment. The Indexer agent manages creating allocations based on the Indexer rules.

- **Closed** - An Indexer is free to close an allocation once 1 epoch has passed ([closeAllocation()](https://github.com/graphprotocol/contracts/blob/main/packages/contracts/contracts/staking/Staking.sol#L335)) or their Indexer agent will automatically close the allocation after the **maxAllocationEpochs** (currently 28 days). When an allocation is closed with a valid proof of indexing (POI) their indexing rewards are distributed to the Indexer and its Delegators ([learn more](/network/indexing/#how-are-indexing-rewards-distributed)).

Indexers are recommended to utilize offchain syncing functionality to sync subgraph deployments to chainhead before creating the allocation on-chain. This feature is especially useful for subgraphs that may take longer than 28 epochs to sync or have some chances of failing undeterministically.
---
title: New Chain Integration
---

Chains can bring subgraph support to their ecosystem by starting a new `graph-node` integration. Subgraphs are a powerful indexing tool opening a world of possibilities for developers. Graph Node already indexes data from the chains listed here. If you are interested in a new integration, there are 2 integration strategies:

1. **EVM JSON-RPC**
2. **Firehose**: All Firehose integration solutions include Substreams, a large-scale streaming engine based off Firehose with native `graph-node` support, allowing for parallelized transforms.

> Note that while the recommended approach is to develop a new Firehose for all new chains, it is only required for non-EVM chains.

## Integration Strategies

### 1. EVM JSON-RPC

If the blockchain is EVM equivalent and the client/node exposes the standard EVM JSON-RPC API, Graph Node should be able to index the new chain.

#### Testing an EVM JSON-RPC

For Graph Node to be able to ingest data from an EVM chain, the RPC node must expose the following EVM JSON-RPC methods:

- `eth_getLogs`
- `eth_call` (for historical blocks, with EIP-1898 - requires archive node)
- `eth_getBlockByNumber`
- `eth_getBlockByHash`
- `net_version`
- `eth_getTransactionReceipt`, in a JSON-RPC batch request
- `trace_filter` *(optionally required for Graph Node to support call handlers)*

### 2. Firehose Integration

[Firehose](https://firehose.streamingfast.io/firehose-setup/overview) is a next-generation extraction layer. It collects history in flat files and streams in real time. Firehose technology replaces those polling API calls with a stream of data utilizing a push model that sends data to the indexing node faster. This helps increase the speed of syncing and indexing.

The primary method to integrate the Firehose into chains is to use an RPC polling strategy. Our polling algorithm will predict when a new block will arrive and increase the rate at which it checks for a new block near that time, making it a very low-latency and efficient solution. For help with the integration and maintenance of the Firehose, contact the [StreamingFast team](https://www.streamingfast.io/firehose-integration-program). New chains and their integrators will appreciate the [fork awareness](https://substreams.streamingfast.io/documentation/consume/reliability-guarantees) and massive parallelized indexing capabilities that Firehose and Substreams bring to their ecosystem.

> NOTE: All integrations done by the StreamingFast team include maintenance for the Firehose replication protocol into the chain's codebase. StreamingFast tracks any changes and releases binaries when you change code and when StreamingFast changes code. This includes releasing Firehose/Substreams binaries for the protocol, maintaining Substreams modules for the block model of the chain, and releasing binaries for the blockchain node with instrumentation if need be.

#### Specific Firehose Instrumentation for EVM (`geth`) chains

For EVM chains, there exists a deeper level of data that can be achieved through the `geth` [live-tracer](https://github.com/ethereum/go-ethereum/releases/tag/v1.14.0), a collaboration between Go-Ethereum and StreamingFast, in building a high-throughput and rich transaction tracing system. The Live Tracer is the most comprehensive solution, resulting in [Extended](https://streamingfastio.medium.com/new-block-model-to-accelerate-chain-integration-9f65126e5425) block details. This enables new indexing paradigms, like pattern matching of events based on state changes, calls, parent call trees, or triggering of events based on changes to the actual variables in a smart contract.

![Base block vs Extended block](/img/extended-vs-base-substreams-blocks.png)

> NOTE: This improvement upon the Firehose requires chains make use of the EVM engine `geth version 1.13.0` and up.

## EVM considerations - Difference between JSON-RPC & Firehose

While the JSON-RPC and Firehose are both suitable for subgraphs, a Firehose is always required for developers wanting to build with [Substreams](https://substreams.streamingfast.io). Supporting Substreams allows developers to build [Substreams-powered subgraphs](/cookbook/substreams-powered-subgraphs) for the new chain, and has the potential to improve the performance of your subgraphs. Additionally, Firehose — as a drop-in replacement for the JSON-RPC extraction layer of `graph-node` — reduces by 90% the number of RPC calls required for general indexing.

- All those `getLogs` calls and roundtrips get replaced by a single stream arriving into the heart of `graph-node`; a single block model for all subgraphs it processes.

> NOTE: A Firehose-based integration for EVM chains will still require Indexers to run the chain's archive RPC node to properly index subgraphs. This is due to the Firehose's inability to provide smart contract state typically accessible by the `eth_call` RPC method. (It's worth reminding that `eth_calls` are not a good practice for developers)

## Graph Node Configuration

Configuring Graph Node is as easy as preparing your local environment. Once your local environment is set, you can test the integration by locally deploying a subgraph.

1. [Clone Graph Node](https://github.com/graphprotocol/graph-node)
2. Modify [this line](https://github.com/graphprotocol/graph-node/blob/master/docker/docker-compose.yml#L22) to include the new network name and the EVM JSON-RPC compliant URL

   > Do not change the env var name itself. It must remain `ethereum` even if the network name is different.

3. Run an IPFS node or use the one used by The Graph: https://api.thegraph.com/ipfs/

### Testing an EVM JSON-RPC by locally deploying a subgraph

1. Install [graph-cli](https://github.com/graphprotocol/graph-cli)
2. Create a simple example subgraph. Some options are below:
   1. The pre-packed [Gravitar](https://github.com/graphprotocol/example-subgraph/tree/f89bdd4628efa4badae7367d4919b3f648083323) smart contract and subgraph is a good starting point
   2. Bootstrap a local subgraph from any existing smart contract or solidity dev environment [using Hardhat with a Graph plugin](https://github.com/graphprotocol/hardhat-graph)
3. Adapt the resulting `subgraph.yaml` by changing `dataSources.network` to the same name previously passed on to Graph Node.
4. Create your subgraph in Graph Node: `graph create $SUBGRAPH_NAME --node $GRAPH_NODE_ENDPOINT`
5. Publish your subgraph to Graph Node: `graph deploy $SUBGRAPH_NAME --ipfs $IPFS_ENDPOINT --node $GRAPH_NODE_ENDPOINT`

Graph Node should be syncing the deployed subgraph if there are no errors. Give it time to sync, then send some GraphQL queries to the API endpoint printed in the logs.

## Substreams-powered Subgraphs

For StreamingFast-led Firehose/Substreams integrations, basic support for foundational Substreams modules (e.g. decoded transactions, logs and smart-contract events) and Substreams codegen tools are included. These tools enable the ability to enable [Substreams-powered subgraphs](/sps/introduction). Follow the [How-To Guide](https://substreams.streamingfast.io/documentation/how-to-guides/intro-your-first-application) and run `substreams codegen subgraph` to experience the codegen tools for yourself.
---
title: Graphcast
---

## Introduction

Is there something you'd like to learn from or share with your fellow Indexers in an automated manner, but it's too much hassle or costs too much gas?

Currently, the cost to broadcast information to other network participants is determined by gas fees on the Ethereum blockchain. Graphcast solves this problem by acting as an optional decentralized, distributed peer-to-peer (P2P) communication tool that allows Indexers across the network to exchange information in real time. The cost of exchanging P2P messages is near zero, with the tradeoff of no data integrity guarantees. Nevertheless, Graphcast aims to provide message validity guarantees (i.e. that the message is valid and signed by a known protocol participant) with an open design space of reputation models.

The Graphcast SDK (Software Development Kit) allows developers to build Radios, which are gossip-powered applications that Indexers can run to serve a given purpose. We also intend to create a few Radios (or provide support to other developers/teams that wish to build Radios) for the following use cases:

- Real-time cross-checking of subgraph data integrity ([Subgraph Radio](https://docs.graphops.xyz/graphcast/radios/subgraph-radio/intro)).
- Conducting auctions and coordination for warp syncing subgraphs, substreams, and Firehose data from other Indexers.
- Self-reporting on active query analytics, including subgraph request volumes, fee volumes, etc.
- Self-reporting on indexing analytics, including subgraph indexing time, handler gas costs, indexing errors encountered, etc.
- Self-reporting on stack information including graph-node version, Postgres version, Ethereum client version, etc.

### Learn More

If you would like to learn more about Graphcast, [check out the documentation here.](https://docs.graphops.xyz/graphcast/intro)
---
title: Safe Subgraph Code Generator
---

[Subgraph Uncrashable](https://float-capital.github.io/float-subgraph-uncrashable/) is a code generation tool that generates a set of helper functions from the graphql schema of a project. It ensures that all interactions with entities in your subgraph are completely safe and consistent.

## Why integrate with Subgraph Uncrashable?

- **Continuous Uptime**. Mishandled entities may cause subgraphs to crash, which can be disruptive for projects that are dependent on The Graph. Set up helper functions to make your subgraphs “uncrashable” and ensure business continuity.

- **Completely Safe**. Common problems seen in subgraph development are issues of loading undefined entities, not setting or initializing all values of entities, and race conditions on loading and saving entities. Ensure all interactions with entities are completely atomic.

- **User Configurable** Set default values and configure the level of security checks that suits your individual project's needs. Warning logs are recorded indicating where there is a breach of subgraph logic to help patch the issue to ensure data accuracy.

**Key Features**

- The code generation tool accommodates **all** subgraph types and is configurable for users to set sane defaults on values. The code generation will use this config to generate helper functions that are to the users specification.

- The framework also includes a way (via the config file) to create custom, but safe, setter functions for groups of entity variables. This way it is impossible for the user to load/use a stale graph entity and it is also impossible to forget to save or set a variable that is required by the function.

- Warning logs are recorded as logs indicating where there is a breach of subgraph logic to help patch the issue to ensure data accuracy.

Subgraph Uncrashable can be run as an optional flag using the Graph CLI codegen command.

```sh
graph codegen -u [options] [<subgraph-manifest>]
```

Visit the [subgraph uncrashable documentation](https://float-capital.github.io/float-subgraph-uncrashable/docs/) or watch this [video tutorial](https://float-capital.github.io/float-subgraph-uncrashable/docs/tutorial) to learn more and to get started with developing safer subgraphs.
---
title: Substreams-powered subgraphs
---

[Substreams](/substreams) is a new framework for processing blockchain data, developed by StreamingFast for The Graph Network. A substreams modules can output entity changes, which are compatible with Subgraph entities. A subgraph can use such a Substreams module as a data source, bringing the indexing speed and additional data of Substreams to subgraph developers.

## Requirements

This cookbook requires [yarn](https://yarnpkg.com/), [the dependencies necessary for local Substreams development](https://substreams.streamingfast.io/documentation/consume/installing-the-cli), and the latest version of Graph CLI (>=0.52.0):

```
npm install -g @graphprotocol/graph-cli
```

## Get the cookbook

> This cookbook uses this [Substreams-powered subgraph as a reference](https://github.com/graphprotocol/graph-tooling/tree/main/examples/substreams-powered-subgraph).

```
graph init --from-example substreams-powered-subgraph
```

## Defining a Substreams package

A Substreams package is composed of types (defined as [Protocol Buffers](https://protobuf.dev/)), modules (written in Rust), and a `substreams.yaml` file which references the types, and specifies how modules are triggered. [Visit the Substreams documentation to learn more about Substreams development](/substreams), and check out [awesome-substreams](https://github.com/pinax-network/awesome-substreams) and the [Substreams cookbook](https://github.com/pinax-network/substreams-cookbook) for more examples.

The Substreams package in question detects contract deployments on Mainnet Ethereum, tracking the creation block and timestamp for all newly deployed contracts. To do this, there is a dedicated `Contract` type in `/proto/example.proto` ([learn more about defining Protocol Buffers](https://protobuf.dev/programming-guides/proto3/#simple)):

```proto
syntax = "proto3";

package example;

message Contracts {
  repeated Contract contracts = 1;
}

message Contract {
    string address = 1;
    uint64 blockNumber = 2;
    string timestamp = 3;
    uint64 ordinal = 4;
}
```

The core logic of the Substreams package is a `map_contract` module in `lib.rs`, which processes every block, filtering for Create calls which did not revert, returning `Contracts`:

```rust
#[substreams::handlers::map]
fn map_contract(block: eth::v2::Block) -> Result<Contracts, substreams::errors::Error> {
    let contracts = block
        .transactions()
        .flat_map(|tx| {
            tx.calls
                .iter()
                .filter(|call| !call.state_reverted)
                .filter(|call| call.call_type == eth::v2::CallType::Create as i32)
                .map(|call| Contract {
                    address: format!("0x{}", Hex(&call.address)),
                    block_number: block.number,
                    timestamp: block.timestamp_seconds().to_string(),
                    ordinal: tx.begin_ordinal,
                })
        })
        .collect();
    Ok(Contracts { contracts })
}
```

A Substreams package can be used by a subgraph as long as it has a module which outputs compatible entity changes. The example Substreams package has an additional `graph_out` module in `lib.rs` which returns a `substreams_entity_change::pb::entity::EntityChanges` output, which can be processed by Graph Node.

> The `substreams_entity_change` crate also has a dedicated `Tables` function for simply generating entity changes ([documentation](https://docs.rs/substreams-entity-change/1.2.2/substreams_entity_change/tables/index.html)). The Entity Changes generated must be compatible with the `schema.graphql` entities defined in the `subgraph.graphql` of the corresponding subgraph.

```rust
#[substreams::handlers::map]
pub fn graph_out(contracts: Contracts) -> Result<EntityChanges, substreams::errors::Error> {
    // hash map of name to a table
    let mut tables = Tables::new();

    for contract in contracts.contracts.into_iter() {
        tables
            .create_row("Contract", contract.address)
            .set("timestamp", contract.timestamp)
            .set("blockNumber", contract.block_number);
    }

    Ok(tables.to_entity_changes())
}
```

These types and modules are pulled together in `substreams.yaml`:

```yaml
specVersion: v0.1.0
package:
  name: 'substreams_test' # the name to be used in the .spkg
  version: v1.0.1 # the version to use when creating the .spkg

imports: # dependencies
  entity: https://github.com/streamingfast/substreams-entity-change/releases/download/v0.2.1/substreams-entity-change-v0.2.1.spkg

protobuf: # specifies custom types for use by Substreams modules
  files:
    - example.proto
  importPaths:
    - ./proto

binaries:
  default:
    type: wasm/rust-v1
    file: ./target/wasm32-unknown-unknown/release/substreams.wasm

modules: # specify modules with their inputs and outputs.
  - name: map_contract
    kind: map
    inputs:
      - source: sf.ethereum.type.v2.Block
    output:
      type: proto:test.Contracts

  - name: graph_out
    kind: map
    inputs:
      - map: map_contract
    output:
      type: proto:substreams.entity.v1.EntityChanges # this type can be consumed by Graph Node
```

You can check the overall "flow" from a Block, to `map_contract` to `graph_out` by running `substreams graph`:

```mermaid
graph TD;
  map_contract[map: map_contract];
  sf.ethereum.type.v2.Block[source: sf.ethereum.type.v2.Block] --> map_contract;
  graph_out[map: graph_out];
  map_contract --> graph_out;
```

To prepare this Substreams package for consumption by a subgraph, you must run the following commands:

```bash
yarn substreams:protogen # generates types in /src/pb
yarn substreams:build # builds the substreams
yarn substreams:package # packages the substreams in a .spkg file

# alternatively, yarn substreams:prepare calls all of the above commands
```

> These scripts are defined in the `package.json` file if you want to understand the underlying substreams commands

This generates a `spkg` file based on the package name and version from `substreams.yaml`. The `spkg` file has all the information which Graph Node needs to ingest this Substreams package.

> If you update the Substreams package, depending on the changes you make, you may need to run some or all of the above commands so that the `spkg` is up to date.

## Defining a Substreams-powered subgraph

Substreams-powered subgraphs introduce a new `kind` of data source, "substreams". Such subgraphs can only have one data source.

This data source must specify the indexed network, the Substreams package (`spkg`) as a relative file location, and the module within that Substreams package which produces subgraph-compatible entity changes (in this case `map_entity_changes`, from the Substreams package above). The mapping is specified, but simply identifies the mapping kind ("substreams/graph-entities") and the apiVersion.

> Currently, Subgraph Studio and The Graph Network support Substreams-powered subgraphs which index `mainnet` (Mainnet Ethereum).

```yaml
specVersion: 0.0.4
description: Ethereum Contract Tracking Subgraph (powered by Substreams)
repository: https://github.com/graphprotocol/graph-tooling
schema:
  file: schema.graphql
dataSources:
  - kind: substreams
    name: substream_test
    network: mainnet
    source:
      package:
        moduleName: graph_out
        file: substreams-test-v1.0.1.spkg
    mapping:
      kind: substreams/graph-entities
      apiVersion: 0.0.5
```

The `subgraph.yaml` also references a schema file. The requirements for this file are unchanged, but the entities specified must be compatible with the entity changes produced by the Substreams module referenced in the `subgraph.yaml`.

```graphql
type Contract @entity {
  id: ID!

  "The timestamp when the contract was deployed"
  timestamp: String!

  "The block number of the contract deployment"
  blockNumber: BigInt!
}
```

Given the above, subgraph developers can use Graph CLI to deploy this Substreams-powered subgraph.

> Substreams-powered subgraphs indexing mainnet Ethereum can be deployed to the [Subgraph Studio](https://thegraph.com/studio/).

```bash
yarn install # install graph-cli
yarn subgraph:build # build the subgraph
yarn subgraph:deploy # deploy the subgraph
```

That's it! You have built and deployed a Substreams-powered subgraph.

## Serving Substreams-powered subgraphs

In order to serve Substreams-powered subgraphs, Graph Node must be configured with a Substreams provider for the relevant network, as well as a Firehose or RPC to track the chain head. These providers can be configured via a `config.toml` file:

```toml
[chains.mainnet]
shard = "main"
protocol = "ethereum"
provider = [
  { label = "substreams-provider-mainnet",
    details = { type = "substreams",
    url = "https://mainnet-substreams-url.grpc.substreams.io/",
    token = "exampletokenhere" }},
  { label = "firehose-provider-mainnet",
    details = { type = "firehose",
    url = "https://mainnet-firehose-url.grpc.firehose.io/",
    token = "exampletokenhere" }},
]
```
---
title: Replace a Contract and Keep its History With Grafting
---

In this guide, you will learn how to build and deploy new subgraphs by grafting existing subgraphs.

## What is Grafting?

Grafting reuses the data from an existing subgraph and starts indexing it at a later block. This is useful during development to get past simple errors in the mappings quickly or to temporarily get an existing subgraph working again after it has failed. Also, it can be used when adding a feature to a subgraph that takes long to index from scratch.

The grafted subgraph can use a GraphQL schema that is not identical to the one of the base subgraph, but merely compatible with it. It has to be a valid subgraph schema in its own right, but may deviate from the base subgraph's schema in the following ways:

- It adds or removes entity types
- It removes attributes from entity types
- It adds nullable attributes to entity types
- It turns non-nullable attributes into nullable attributes
- It adds values to enums
- It adds or removes interfaces
- It changes for which entity types an interface is implemented

For more information, you can check:

- [Grafting](/developing/creating-a-subgraph#grafting-onto-existing-subgraphs)

In this tutorial, we will be covering a basic use case. We will replace an existing contract with an identical contract (with a new address, but the same code). Then, graft the existing subgraph onto the "base" subgraph that tracks the new contract.

## Important Note on Grafting When Upgrading to the Network

> **Caution**: It is recommended to not use grafting for subgraphs published to The Graph Network

### Why Is This Important?

Grafting is a powerful feature that allows you to "graft" one subgraph onto another, effectively transferring historical data from the existing subgraph to a new version. It is not possible to graft a subgraph from The Graph Network back to Subgraph Studio.

### Best Practices

**Initial Migration**: when you first deploy your subgraph to the decentralized network, do so without grafting. Ensure that the subgraph is stable and functioning as expected.

**Subsequent Updates**: once your subgraph is live and stable on the decentralized network, you may use grafting for future versions to make the transition smoother and to preserve historical data.

By adhering to these guidelines, you minimize risks and ensure a smoother migration process.

## Building an Existing Subgraph

Building subgraphs is an essential part of The Graph, described more in depth [here](/quick-start/). To be able to build and deploy the existing subgraph used in this tutorial, the following repo is provided:

- [Subgraph example repo](https://github.com/Shiyasmohd/grafting-tutorial)

> Note: The contract used in the subgraph was taken from the following [Hackathon Starterkit](https://github.com/schmidsi/hackathon-starterkit).

## Subgraph Manifest Definition

The subgraph manifest `subgraph.yaml` identifies the data sources for the subgraph, the triggers of interest, and the functions that should be run in response to those triggers. See below for an example subgraph manifest that you will use:

```yaml
specVersion: 0.0.4
schema:
  file: ./schema.graphql
dataSources:
  - kind: ethereum
    name: Lock
    network: sepolia
    source:
      address: '0xb3aabe721794b85fe4e72134795c2f93b4eb7e63'
      abi: Lock
      startBlock: 5955690
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
      language: wasm/assemblyscript
      entities:
        - Withdrawal
      abis:
        - name: Lock
          file: ./abis/Lock.json
      eventHandlers:
        - event: Withdrawal(uint256,uint256)
          handler: handleWithdrawal
      file: ./src/lock.ts
```

- The `Lock` data source is the abi and contract address we will get when we compile and deploy the contract
- The network should correspond to an indexed network being queried. Since we're running on Sepolia testnet, the network is `sepolia`
- The `mapping` section defines the triggers of interest and the functions that should be run in response to those triggers. In this case, we are listening for the `Withdrawal` event and calling the `handleWithdrawal` function when it is emitted.

## Grafting Manifest Definition

Grafting requires adding two new items to the original subgraph manifest:

```yaml
---
features:
  - grafting # feature name
graft:
  base: Qm... # subgraph ID of base subgraph
  block: 5956000 # block number
```

- `features:` is a list of all used [feature names](/developing/creating-a-subgraph/#experimental-features).
- `graft:` is a map of the `base` subgraph and the block to graft on to. The `block` is the block number to start indexing from. The Graph will copy the data of the base subgraph up to and including the given block and then continue indexing the new subgraph from that block on.

The `base` and `block` values can be found by deploying two subgraphs: one for the base indexing and one with grafting

## Deploying the Base Subgraph

1. Go to [Subgraph Studio](https://thegraph.com/studio/) and create a subgraph on Sepolia testnet called `graft-example`
2. Follow the directions in the `AUTH & DEPLOY` section on your subgraph page in the `graft-example` folder from the repo
3. Once finished, verify the subgraph is indexing properly. If you run the following command in The Graph Playground

```graphql
{
  withdrawals(first: 5) {
    id
    amount
    when
  }
}
```

It returns something like this:

```
{
  "data": {
    "withdrawals": [
      {
        "id": "0xe8323d21c4f104607b10b0fff9fc24b9612b9488795dea8196b2d5f980d3dc1d0a000000",
        "amount": "0",
        "when": "1716394824"
      },
      {
        "id": "0xea1cee35036f2cacb72f2a336be3e54ab911f5bebd58f23400ebb8ecc5cfc45203000000",
        "amount": "0",
        "when": "1716394848"
      }
    ]
  }
}
```

Once you have verified the subgraph is indexing properly, you can quickly update the subgraph with grafting.

## Deploying the Grafting Subgraph

The graft replacement subgraph.yaml will have a new contract address. This could happen when you update your dapp, redeploy a contract, etc.

1. Go to [Subgraph Studio](https://thegraph.com/studio/) and create a subgraph on Sepolia testnet called `graft-replacement`
2. Create a new manifest. The `subgraph.yaml` for `graph-replacement` contains a different contract address and new information about how it should graft. These are the `block` of the [last event emitted](https://sepolia.etherscan.io/tx/0xea1cee35036f2cacb72f2a336be3e54ab911f5bebd58f23400ebb8ecc5cfc452) you care about by the old contract and the `base` of the old subgraph. The `base` subgraph ID is the `Deployment ID` of your original `graph-example` subgraph. You can find this in Subgraph Studio.
3. Follow the directions in the `AUTH & DEPLOY` section on your subgraph page in the `graft-replacement` folder from the repo
4. Once finished, verify the subgraph is indexing properly. If you run the following command in The Graph Playground

```graphql
{
  withdrawals(first: 5) {
    id
    amount
    when
  }
}
```

It should return the following:

```
{
  "data": {
    "withdrawals": [
      {
        "id": "0xe8323d21c4f104607b10b0fff9fc24b9612b9488795dea8196b2d5f980d3dc1d0a000000",
        "amount": "0",
        "when": "1716394824"
      },
      {
        "id": "0xea1cee35036f2cacb72f2a336be3e54ab911f5bebd58f23400ebb8ecc5cfc45203000000",
        "amount": "0",
        "when": "1716394848"
      },
      {
        "id": "0x2410475f76a44754bae66d293d14eac34f98ec03a3689cbbb56a716d20b209af06000000",
        "amount": "0",
        "when": "1716429732"
      }
    ]
  }
}
```

You can see that the `graft-replacement` subgraph is indexing from older `graph-example` data and newer data from the new contract address. The original contract emitted two `Withdrawal` events, [Event 1](https://sepolia.etherscan.io/tx/0xe8323d21c4f104607b10b0fff9fc24b9612b9488795dea8196b2d5f980d3dc1d) and [Event 2](https://sepolia.etherscan.io/tx/0xea1cee35036f2cacb72f2a336be3e54ab911f5bebd58f23400ebb8ecc5cfc452). The new contract emitted one `Withdrawal` after, [Event 3](https://sepolia.etherscan.io/tx/0x2410475f76a44754bae66d293d14eac34f98ec03a3689cbbb56a716d20b209af). The two previously indexed transactions (Event 1 and 2) and the new transaction (Event 3) were combined together in the `graft-replacement` subgraph.

Congrats! You have successfully grafted a subgraph onto another subgraph.

## Additional Resources

If you want more experience with grafting, here are a few examples for popular contracts:

- [Curve](https://github.com/messari/subgraphs/blob/master/subgraphs/curve-finance/protocols/curve-finance/config/templates/curve.template.yaml)
- [ERC-721](https://github.com/messari/subgraphs/blob/master/subgraphs/erc721-metadata/subgraph.yaml)
- [Uniswap](https://github.com/messari/subgraphs/blob/master/subgraphs/uniswap-v3-forks/protocols/uniswap-v3/config/templates/uniswapV3Template.yaml),

To become even more of a Graph expert, consider learning about other ways to handle changes in underlying datasources. Alternatives like [Data Source Templates](/developing/creating-a-subgraph/#data-source-templates) can achieve similar results

> Note: A lot of material from this article was taken from the previously published [Arweave article](/cookbook/arweave/)
---
title: Building Subgraphs on Cosmos
---

This guide is an introduction on building subgraphs indexing [Cosmos](https://cosmos.network/) based blockchains.

## What are Cosmos subgraphs?

The Graph allows developers to process blockchain events and make the resulting data easily available via an open GraphQL API, known as a subgraph. [Graph Node](https://github.com/graphprotocol/graph-node) is now able to process Cosmos events, which means Cosmos developers can now build subgraphs to easily index on-chain events.

There are four types of handlers supported in Cosmos subgraphs:

- **Block handlers** run whenever a new block is appended to the chain.
- **Event handlers** run when a specific event is emitted.
- **Transaction handlers** run when a transaction occurs.
- **Message handlers** run when a specific message occurs.

Based on the [official Cosmos documentation](https://docs.cosmos.network/):

> [Events](https://docs.cosmos.network/main/learn/advanced/events) are objects that contain information about the execution of the application. They are mainly used by service providers like block explorers and wallets to track the execution of various messages and index transactions.

> [Transactions](https://docs.cosmos.network/main/learn/advanced/transactions) are objects created by end-users to trigger state changes in the application.

> [Messages](https://docs.cosmos.network/main/learn/advanced/transactions#messages) are module-specific objects that trigger state transitions within the scope of the module they belong to.

Even though all data can be accessed with a block handler, other handlers enable subgraph developers to process data in a much more granular way.

## Building a Cosmos subgraph

### Subgraph Dependencies

[graph-cli](https://github.com/graphprotocol/graph-tooling/tree/main/packages/cli) is a CLI tool to build and deploy subgraphs, version `>=0.30.0` is required in order to work with Cosmos subgraphs.

[graph-ts](https://github.com/graphprotocol/graph-tooling/tree/main/packages/ts) is a library of subgraph-specific types, version `>=0.27.0` is required in order to work with Cosmos subgraphs.

### Subgraph Main Components

There are three key parts when it comes to defining a subgraph:

**subgraph.yaml**: a YAML file containing the subgraph manifest, which identifies which events to track and how to process them.

**schema.graphql**: a GraphQL schema that defines what data is stored for your subgraph, and how to query it via GraphQL.

**AssemblyScript Mappings**: [AssemblyScript](https://github.com/AssemblyScript/assemblyscript) code that translates from blockchain data to the entities defined in your schema.

### Subgraph Manifest Definition

The subgraph manifest (`subgraph.yaml`) identifies the data sources for the subgraph, the triggers of interest, and the functions (`handlers`) that should be run in response to those triggers. See below for an example subgraph manifest for a Cosmos subgraph:

```yaml
specVersion: 0.0.5
description: Cosmos Subgraph Example
schema:
  file: ./schema.graphql # link to the schema file
dataSources:
  - kind: cosmos
    name: CosmosHub
    network: cosmoshub-4 # This will change for each cosmos-based blockchain. In this case, the example uses the Cosmos Hub mainnet.
    source:
      startBlock: 0 # Required for Cosmos, set this to 0 to start indexing from chain genesis
    mapping:
      apiVersion: 0.0.7
      language: wasm/assemblyscript
      blockHandlers:
        - handler: handleNewBlock # the function name in the mapping file
      eventHandlers:
        - event: rewards # the type of the event that will be handled
          handler: handleReward # the function name in the mapping file
      transactionHandlers:
        - handler: handleTransaction # the function name in the mapping file
      messageHandlers:
        - message: /cosmos.staking.v1beta1.MsgDelegate # the type of a message
          handler: handleMsgDelegate # the function name in the mapping file
      file: ./src/mapping.ts # link to the file with the Assemblyscript mappings
```

- Cosmos subgraphs introduce a new `kind` of data source (`cosmos`).
- The `network` should correspond to a chain in the Cosmos ecosystem. In the example, the Cosmos Hub mainnet is used.

### Schema Definition

Schema definition describes the structure of the resulting subgraph database and the relationships between entities. This is agnostic of the original data source. There are more details on subgraph schema definition [here](/developing/creating-a-subgraph/#the-graphql-schema).

### AssemblyScript Mappings

The handlers for processing events are written in [AssemblyScript](https://www.assemblyscript.org/).

Cosmos indexing introduces Cosmos-specific data types to the [AssemblyScript API](/developing/graph-ts/api/).

```tsx
class Block {
  header: Header
  evidence: EvidenceList
  resultBeginBlock: ResponseBeginBlock
  resultEndBlock: ResponseEndBlock
  transactions: Array<TxResult>
  validatorUpdates: Array<Validator>
}

class EventData {
  event: Event
  block: HeaderOnlyBlock
  tx: TransactionContext
}

class TransactionData {
  tx: TxResult
  block: HeaderOnlyBlock
}

class MessageData {
  message: Any
  block: HeaderOnlyBlock
  tx: TransactionContext
}

class TransactionContext {
  hash: Bytes
  index: u32
  code: u32
  gasWanted: i64
  gasUsed: i64
}

class HeaderOnlyBlock {
  header: Header
}

class Header {
  version: Consensus
  chainId: string
  height: u64
  time: Timestamp
  lastBlockId: BlockID
  lastCommitHash: Bytes
  dataHash: Bytes
  validatorsHash: Bytes
  nextValidatorsHash: Bytes
  consensusHash: Bytes
  appHash: Bytes
  lastResultsHash: Bytes
  evidenceHash: Bytes
  proposerAddress: Bytes
  hash: Bytes
}

class TxResult {
  height: u64
  index: u32
  tx: Tx
  result: ResponseDeliverTx
  hash: Bytes
}

class Event {
  eventType: string
  attributes: Array<EventAttribute>
}

class Any {
  typeUrl: string
  value: Bytes
}
```

Each handler type comes with its own data structure that is passed as an argument to a mapping function.

- Block handlers receive the `Block` type.
- Event handlers receive the `EventData` type.
- Transaction handlers receive the `TransactionData` type.
- Message handlers receive the `MessageData` type.

As a part of `MessageData` the message handler receives a transaction context, which contains the most important information about a transaction that encompasses a message. The transaction context is also available in the `EventData` type, but only when the corresponding event is associated with a transaction. Additionally, all handlers receive a reference to a block (`HeaderOnlyBlock`).

You can find the full list of types for the Cosmos integration [here](https://github.com/graphprotocol/graph-ts/blob/4c064a8118dff43b110de22c7756e5d47fcbc8df/chain/cosmos.ts).

### Message decoding

It's important to note that Cosmos messages are chain-specific and they are passed to a subgraph in the form of a serialized [Protocol Buffers](https://protobuf.dev/) payload. As a result, the message data needs to be decoded in a mapping function before it can be processed.

An example of how to decode message data in a subgraph can be found [here](https://github.com/graphprotocol/graph-tooling/blob/main/examples/cosmos-validator-delegations/src/decoding.ts).

## Creating and building a Cosmos subgraph

The first step before starting to write the subgraph mappings is to generate the type bindings based on the entities that have been defined in the subgraph schema file (`schema.graphql`). This will allow the mapping functions to create new objects of those types and save them to the store. This is done by using the `codegen` CLI command:

```bash
$ graph codegen
```

Once the mappings are ready, the subgraph needs to be built. This step will highlight any errors the manifest or the mappings might have. A subgraph needs to build successfully in order to be deployed to the Graph Node. It can be done using the `build` CLI command:

```bash
$ graph build
```

## Deploying a Cosmos subgraph

Once your subgraph has been created, you can deploy your subgraph by using the `graph deploy` CLI command:

**Subgraph Studio**

Visit the Subgraph Studio to create a new subgraph.

```bash
graph deploy --studio subgraph-name
```

**Local Graph Node (based on default configuration):**

```bash
graph create subgraph-name --node http://localhost:8020
```

```bash
graph deploy subgraph-name --node http://localhost:8020/ --ipfs http://localhost:5001
```

## Querying a Cosmos subgraph

The GraphQL endpoint for Cosmos subgraphs is determined by the schema definition, with the existing API interface. Please visit the [GraphQL API documentation](/querying/graphql-api/) for more information.

## Supported Cosmos Blockchains

### Cosmos Hub

#### What is Cosmos Hub?

The [Cosmos Hub blockchain](https://hub.cosmos.network/) is the first blockchain in the [Cosmos](https://cosmos.network/) ecosystem. You can visit the [official documentation](https://docs.cosmos.network/) for more information.

#### Networks

Cosmos Hub mainnet is `cosmoshub-4`. Cosmos Hub current testnet is `theta-testnet-001`. <br/>Other Cosmos Hub networks, i.e. `cosmoshub-3`, are halted, therefore no data is provided for them.

### Osmosis

> Osmosis support in Graph Node and on Subgraph Studio is in beta: please contact the graph team with any questions about building Osmosis subgraphs!

#### What is Osmosis?

[Osmosis](https://osmosis.zone/) is a decentralized, cross-chain automated market maker (AMM) protocol built on top of the Cosmos SDK. It allows users to create custom liquidity pools and trade IBC-enabled tokens. You can visit the [official documentation](https://docs.osmosis.zone/) for more information.

#### Networks

Osmosis mainnet is `osmosis-1`. Osmosis current testnet is `osmo-test-4`.

## Example Subgraphs

Here are some example subgraphs for reference:

[Block Filtering Example](https://github.com/graphprotocol/graph-tooling/tree/main/examples/cosmos-block-filtering)

[Validator Rewards Example](https://github.com/graphprotocol/graph-tooling/tree/main/examples/cosmos-validator-rewards)

[Validator Delegations Example](https://github.com/graphprotocol/graph-tooling/tree/main/examples/cosmos-validator-delegations)

[Osmosis Token Swaps Example](https://github.com/graphprotocol/graph-tooling/tree/main/examples/cosmos-osmosis-token-swaps)
---
title: Building Subgraphs on Arweave
---

> Arweave support in Graph Node and on Subgraph Studio is in beta: please reach us on [Discord](https://discord.gg/graphprotocol) with any questions about building Arweave subgraphs!

In this guide, you will learn how to build and deploy Subgraphs to index the Arweave blockchain.

## What is Arweave?

The Arweave protocol allows developers to store data permanently and that is the main difference between Arweave and IPFS, where IPFS lacks the feature; permanence, and files stored on Arweave can't be changed or deleted.

Arweave already has built numerous libraries for integrating the protocol in a number of different programming languages. For more information you can check:

- [Arwiki](https://arwiki.wiki/#/en/main)
- [Arweave Resources](https://www.arweave.org/build)

## What are Arweave Subgraphs?

The Graph allows you to build custom open APIs called "Subgraphs". Subgraphs are used to tell indexers (server operators) which data to index on a blockchain and save on their servers in order for you to be able to query it at any time using [GraphQL](https://graphql.org/).

[Graph Node](https://github.com/graphprotocol/graph-node) is now able to index data on Arweave protocol. The current integration is only indexing Arweave as a blockchain (blocks and transactions), it is not indexing the stored files yet.

## Building an Arweave Subgraph

To be able to build and deploy Arweave Subgraphs, you need two packages:

1. `@graphprotocol/graph-cli` above version 0.30.2 - This is a command-line tool for building and deploying subgraphs. [Click here](https://www.npmjs.com/package/@graphprotocol/graph-cli) to download using `npm`.
2. `@graphprotocol/graph-ts` above version 0.27.0 - This is library of subgraph-specific types. [Click here](https://www.npmjs.com/package/@graphprotocol/graph-ts) to download using `npm`.

## Subgraph's components

There are three components of a subgraph:

### 1. Manifest - `subgraph.yaml`

Defines the data sources of interest, and how they should be processed. Arweave is a new kind of data source.

### 2. Schema - `schema.graphql`

Here you define which data you want to be able to query after indexing your Subgraph using GraphQL. This is actually similar to a model for an API, where the model defines the structure of a request body.

The requirements for Arweave subgraphs are covered by the [existing documentation](/developing/creating-a-subgraph/#the-graphql-schema).

### 3. AssemblyScript Mappings - `mapping.ts`

This is the logic that determines how data should be retrieved and stored when someone interacts with the data sources you are listening to. The data gets translated and is stored based off the schema you have listed.

During subgraph development there are two key commands:

```
$ graph codegen # generates types from the schema file identified in the manifest
$ graph build # generates Web Assembly from the AssemblyScript files, and prepares all the subgraph files in a /build folder
```

## Subgraph Manifest Definition

The subgraph manifest `subgraph.yaml` identifies the data sources for the subgraph, the triggers of interest, and the functions that should be run in response to those triggers. See below for an example subgraph manifest for an Arweave subgraph:

```yaml
specVersion: 0.0.5
description: Arweave Blocks Indexing
schema:
  file: ./schema.graphql # link to the schema file
dataSources:
  - kind: arweave
    name: arweave-blocks
    network: arweave-mainnet # The Graph only supports Arweave Mainnet
    source:
      owner: 'ID-OF-AN-OWNER' # The public key of an Arweave wallet
      startBlock: 0 # set this to 0 to start indexing from chain genesis
    mapping:
      apiVersion: 0.0.5
      language: wasm/assemblyscript
      file: ./src/blocks.ts # link to the file with the Assemblyscript mappings
      entities:
        - Block
        - Transaction
      blockHandlers:
        - handler: handleBlock # the function name in the mapping file
      transactionHandlers:
        - handler: handleTx # the function name in the mapping file
```

- Arweave subgraphs introduce a new kind of data source (`arweave`)
- The network should correspond to a network on the hosting Graph Node. In Subgraph Studio, Arweave's mainnet is `arweave-mainnet`
- Arweave data sources introduce an optional source.owner field, which is the public key of an Arweave wallet

Arweave data sources support two types of handlers:

- `blockHandlers` - Run on every new Arweave block. No source.owner is required.
- `transactionHandlers` - Run on every transaction where the data source's `source.owner` is the owner. Currently an owner is required for `transactionHandlers`, if users want to process all transactions they should provide "" as the `source.owner`

> The source.owner can be the owner's address, or their Public Key.

> Transactions are the building blocks of the Arweave permaweb and they are objects created by end-users.

> Note: [Irys (previously Bundlr)](https://irys.xyz/) transactions are not supported yet.

## Schema Definition

Schema definition describes the structure of the resulting subgraph database and the relationships between entities. This is agnostic of the original data source. There are more details on the subgraph schema definition [here](/developing/creating-a-subgraph/#the-graphql-schema).

## AssemblyScript Mappings

The handlers for processing events are written in [AssemblyScript](https://www.assemblyscript.org/).

Arweave indexing introduces Arweave-specific data types to the [AssemblyScript API](/developing/graph-ts/api/).

```tsx
class Block {
  timestamp: u64
  lastRetarget: u64
  height: u64
  indepHash: Bytes
  nonce: Bytes
  previousBlock: Bytes
  diff: Bytes
  hash: Bytes
  txRoot: Bytes
  txs: Bytes[]
  walletList: Bytes
  rewardAddr: Bytes
  tags: Tag[]
  rewardPool: Bytes
  weaveSize: Bytes
  blockSize: Bytes
  cumulativeDiff: Bytes
  hashListMerkle: Bytes
  poa: ProofOfAccess
}

class Transaction {
  format: u32
  id: Bytes
  lastTx: Bytes
  owner: Bytes
  tags: Tag[]
  target: Bytes
  quantity: Bytes
  data: Bytes
  dataSize: Bytes
  dataRoot: Bytes
  signature: Bytes
  reward: Bytes
}
```

Block handlers receive a `Block`, while transactions receive a `Transaction`.

Writing the mappings of an Arweave Subgraph is very similar to writing the mappings of an Ethereum Subgraph. For more information, click [here](/developing/creating-a-subgraph/#writing-mappings).

## Deploying an Arweave Subgraph in Subgraph Studio

Once your subgraph has been created on your Subgraph Studio dashboard, you can deploy by using the `graph deploy` CLI command.

```bash
graph deploy --studio --access-token <your-access-token>
```

## Querying an Arweave Subgraph

The GraphQL endpoint for Arweave subgraphs is determined by the schema definition, with the existing API interface. Please visit the [GraphQL API documentation](/querying/graphql-api/) for more information.

## Example Subgraphs

Here is an example subgraph for reference:

- [Example subgraph for Arweave](https://github.com/graphprotocol/graph-tooling/tree/main/examples/arweave-blocks-transactions)

## FAQ

### Can a subgraph index Arweave and other chains?

No, a subgraph can only support data sources from one chain/network.

### Can I index the stored files on Arweave?

Currently, The Graph is only indexing Arweave as a blockchain (its blocks and transactions).

### Can I identify Bundlr bundles in my subgraph?

This is not currently supported.

### How can I filter transactions to a specific account?

The source.owner can be the user's public key or account address.

### What is the current encryption format?

Data is generally passed into the mappings as Bytes, which if stored directly is returned in the subgraph in a `hex` format (ex. block and transaction hashes). You may want to convert to a `base64` or `base64 URL`-safe format in your mappings, in order to match what is displayed in block explorers like [Arweave Explorer](https://viewblock.io/arweave/).

The following `bytesToBase64(bytes: Uint8Array, urlSafe: boolean): string` helper function can be used, and will be added to `graph-ts`:

```
const base64Alphabet = [
	"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M",
	"N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z",
	"a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m",
	"n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z",
	"0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "+", "/"
];

const base64UrlAlphabet = [
	"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M",
	"N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z",
	"a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m",
	"n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z",
	"0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "-", "_"
];

function bytesToBase64(bytes: Uint8Array, urlSafe: boolean): string {
	let alphabet = urlSafe? base64UrlAlphabet : base64Alphabet;

	let result = '', i: i32, l = bytes.length;
	for (i = 2; i < l; i += 3) {
		result += alphabet[bytes[i - 2] >> 2];
		result += alphabet[((bytes[i - 2] & 0x03) << 4) | (bytes[i - 1] >> 4)];
		result += alphabet[((bytes[i - 1] & 0x0F) << 2) | (bytes[i] >> 6)];
		result += alphabet[bytes[i] & 0x3F];
	}
	if (i === l + 1) { // 1 octet yet to write
		result += alphabet[bytes[i - 2] >> 2];
		result += alphabet[(bytes[i - 2] & 0x03) << 4];
		if (!urlSafe) {
			result += "==";
		}
	}
	if (!urlSafe && i === l) { // 2 octets yet to write
		result += alphabet[bytes[i - 2] >> 2];
		result += alphabet[((bytes[i - 2] & 0x03) << 4) | (bytes[i - 1] >> 4)];
		result += alphabet[(bytes[i - 1] & 0x0F) << 2];
		if (!urlSafe) {
			result += "=";
		}
	}
	return result;
}
```
---
title: How to Secure API Keys Using Next.js Server Components
---

## Overview

We can use [Next.js server components](https://nextjs.org/docs/app/building-your-application/rendering/server-components) to properly secure our API key from exposure in the frontend of our dapp. To further increase our API key security, we can also [restrict our API key to certain subgraphs or domains in Subgraph Studio](/cookbook/upgrading-a-subgraph/#securing-your-api-key).

In this cookbook, we will go over how to create a Next.js server component that queries a subgraph while also hiding the API key from the frontend.

### Caveats

- Next.js server components do not protect API keys from being drained using denial of service attacks.
- The Graph Network gateways have denial of service detection and mitigation strategies in place, however using server components may weaken these protections.
- Next.js server components introduce centralization risks as the server can go down.

### Why It's Needed

In a standard React application, API keys included in the frontend code can be exposed to the client-side, posing a security risk. While `.env` files are commonly used, they don't fully protect the keys since React's code is executed on the client side, exposing the API key in the headers. Next.js Server Components address this issue by handling sensitive operations server-side.

### Using client-side rendering to query a subgraph

![Client-side rendering](/img/api-key-client-side-rendering.png)

### Prerequisites

- An API key from [Subgraph Studio](https://thegraph.com/studio)
- Basic knowledge of Next.js and React.
- An existing Next.js project that uses the [App Router](https://nextjs.org/docs/app).

## Step-by-Step Cookbook

### Step 1: Set Up Environment Variables

1. In our Next.js project root, create a `.env.local` file.
2. Add our API key: `API_KEY=<api_key_here>`.

### Step 2: Create a Server Component

1. In our `components` directory, create a new file, `ServerComponent.js`.
2. Use the provided example code to set up the server component.

### Step 3: Implement Server-Side API Request

In `ServerComponent.js`, add the following code:

```javascript
const API_KEY = process.env.API_KEY

export default async function ServerComponent() {
  const response = await fetch(
    `https://gateway-arbitrum.network.thegraph.com/api/${API_KEY}/subgraphs/id/HUZDsRpEVP2AvzDCyzDHtdc64dyDxx8FQjzsmqSg4H3B`,
    {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        query: /* GraphQL */ `
          {
            factories(first: 5) {
              id
              poolCount
              txCount
              totalVolumeUSD
            }
          }
        `,
      }),
    },
  )

  const responseData = await response.json()
  const data = responseData.data

  return (
    <div>
      <h1>Server Component</h1>
      {data ? (
        <ul>
          {data.factories.map((factory) => (
            <li key={factory.id}>
              <p>ID: {factory.id}</p>
              <p>Pool Count: {factory.poolCount}</p>
              <p>Transaction Count: {factory.txCount}</p>
              <p>Total Volume USD: {factory.totalVolumeUSD}</p>
            </li>
          ))}
        </ul>
      ) : (
        <p>Loading data...</p>
      )}
    </div>
  )
}
```

### Step 4: Use the Server Component

1. In our page file (e.g., `pages/index.js`), import `ServerComponent`.
2. Render the component:

```javascript
import ServerComponent from './components/ServerComponent'

export default function Home() {
  return (
    <main>
      <ServerComponent />
    </main>
  )
}
```

### Step 5: Run and Test Our Dapp

Start our Next.js application using `npm run dev`. Verify that the server component is fetching data without exposing the API key.

![Server-side rendering](/img/api-key-server-side-rendering.png)

### Conclusion

By utilizing Next.js Server Components, we've effectively hidden the API key from the client-side, enhancing the security of our application. This method ensures that sensitive operations are handled server-side, away from potential client-side vulnerabilities. Finally, be sure to explore [other API key security measures](/cookbook/upgrading-a-subgraph/#securing-your-api-key) to increase your API key security even further.
---
title: Quick and Easy Subgraph Debugging Using Forks
---

As with many systems processing large amounts of data, The Graph's Indexers (Graph Nodes) may take quite some time to sync-up your subgraph with the target blockchain. The discrepancy between quick changes with the purpose of debugging and long wait times needed for indexing is extremely counterproductive and we are well aware of that. This is why we are introducing **subgraph forking**, developed by [LimeChain](https://limechain.tech/), and in this article I will show you how this feature can be used to substantially speed-up subgraph debugging!

## Ok, what is it?

**Subgraph forking** is the process of lazily fetching entities from _another_ subgraph's store (usually a remote one).

In the context of debugging, **subgraph forking** allows you to debug your failed subgraph at block _X_ without needing to wait to sync-up to block _X_.

## What?! How?

When you deploy a subgraph to a remote Graph Node for indexing and it fails at block _X_, the good news is that the Graph Node will still serve GraphQL queries using its store, which is synced-up to block _X_. That's great! This means we can take advantage of this "up-to-date" store to fix the bugs arising when indexing block _X_.

In a nutshell, we are going to _fork the failing subgraph_ from a remote Graph Node that is guaranteed to have the subgraph indexed up to block _X_ in order to provide the locally deployed subgraph being debugged at block _X_ an up-to-date view of the indexing state.

## Please, show me some code!

To stay focused on subgraph debugging, let's keep things simple and run along with the [example-subgraph](https://github.com/graphprotocol/graph-tooling/tree/main/examples/ethereum-gravatar) indexing the Ethereum Gravity smart contract.

Here are the handlers defined for indexing `Gravatar`s, with no bugs whatsoever:

```tsx
export function handleNewGravatar(event: NewGravatar): void {
  let gravatar = new Gravatar(event.params.id.toHex().toString())
  gravatar.owner = event.params.owner
  gravatar.displayName = event.params.displayName
  gravatar.imageUrl = event.params.imageUrl
  gravatar.save()
}

export function handleUpdatedGravatar(event: UpdatedGravatar): void {
  let gravatar = Gravatar.load(event.params.id.toI32().toString())
  if (gravatar == null) {
    log.critical('Gravatar not found!', [])
    return
  }
  gravatar.owner = event.params.owner
  gravatar.displayName = event.params.displayName
  gravatar.imageUrl = event.params.imageUrl
  gravatar.save()
}
```

Oops, how unfortunate, when I deploy my perfect looking subgraph to [Subgraph Studio](https://thegraph.com/studio/) it fails with the _"Gravatar not found!"_ error.

The usual way to attempt a fix is:

1. Make a change in the mappings source, which you believe will solve the issue (while I know it won't).
2. Re-deploy the subgraph to [Subgraph Studio](https://thegraph.com/studio/) (or another remote Graph Node).
3. Wait for it to sync-up.
4. If it breaks again go back to 1, otherwise: Hooray!

It is indeed pretty familiar to an ordinary debug process, but there is one step that horribly slows down the process: _3. Wait for it to sync-up._

Using **subgraph forking** we can essentially eliminate this step. Here is how it looks:

0. Spin-up a local Graph Node with the **_appropriate fork-base_** set.
1. Make a change in the mappings source, which you believe will solve the issue.
2. Deploy to the local Graph Node, **_forking the failing subgraph_** and **_starting from the problematic block_**.
3. If it breaks again, go back to 1, otherwise: Hooray!

Now, you may have 2 questions:

1. fork-base what???
2. Forking who?!

And I answer:

1. `fork-base` is the "base" URL, such that when the _subgraph id_ is appended the resulting URL (`<fork-base>/<subgraph-id>`) is a valid GraphQL endpoint for the subgraph's store.
2. Forking is easy, no need to sweat:

```bash
$ graph deploy <subgraph-name> --debug-fork <subgraph-id> --ipfs http://localhost:5001 --node http://localhost:8020
```

Also, don't forget to set the `dataSources.source.startBlock` field in the subgraph manifest to the number of the problematic block, so you can skip indexing unnecessary blocks and take advantage of the fork!

So, here is what I do:

1. I spin-up a local Graph Node ([here is how to do it](https://github.com/graphprotocol/graph-node#running-a-local-graph-node)) with the `fork-base` option set to: `https://api.thegraph.com/subgraphs/id/`, since I will fork a subgraph, the buggy one I deployed earlier, from [Subgraph Studio](https://thegraph.com/studio/).

```
$ cargo run -p graph-node --release -- \
    --postgres-url postgresql://USERNAME[:PASSWORD]@localhost:5432/graph-node \
    --ethereum-rpc NETWORK_NAME:[CAPABILITIES]:URL \
    --ipfs 127.0.0.1:5001
    --fork-base https://api.thegraph.com/subgraphs/id/
```

2. After careful inspection I notice that there is a mismatch in the `id` representations used when indexing `Gravatar`s in my two handlers. While `handleNewGravatar` converts it to a hex (`event.params.id.toHex()`), `handleUpdatedGravatar` uses an int32 (`event.params.id.toI32()`) which causes the `handleUpdatedGravatar` to panic with "Gravatar not found!". I make them both convert the `id` to a hex.
3. After I made the changes I deploy my subgraph to the local Graph Node, **_forking the failing subgraph_** and setting `dataSources.source.startBlock` to `6190343` in `subgraph.yaml`:

```bash
$ graph deploy gravity --debug-fork QmNp169tKvomnH3cPXTfGg4ZEhAHA6kEq5oy1XDqAxqHmW --ipfs http://localhost:5001 --node http://localhost:8020
```

4. I inspect the logs produced by the local Graph Node and, Hooray!, everything seems to be working.
5. I deploy my now bug-free subgraph to a remote Graph Node and live happily ever after! (no potatoes tho)
---
title: Building Subgraphs on NEAR
---

This guide is an introduction to building subgraphs indexing smart contracts on the [NEAR blockchain](https://docs.near.org/).

## What is NEAR?

[NEAR](https://near.org/) is a smart contract platform for building decentralized applications. Visit the [official documentation](https://docs.near.org/concepts/basics/protocol) for more information.

## What are NEAR subgraphs?

The Graph gives developers tools to process blockchain events and make the resulting data easily available via a GraphQL API, known individually as a subgraph. [Graph Node](https://github.com/graphprotocol/graph-node) is now able to process NEAR events, which means that NEAR developers can now build subgraphs to index their smart contracts.

Subgraphs are event-based, which means that they listen for and then process on-chain events. There are currently two types of handlers supported for NEAR subgraphs:

- Block handlers: these are run on every new block
- Receipt handlers: run every time a message is executed at a specified account

[From the NEAR documentation](https://docs.near.org/build/data-infrastructure/lake-data-structures/receipt):

> A Receipt is the only actionable object in the system. When we talk about "processing a transaction" on the NEAR platform, this eventually means "applying receipts" at some point.

## Building a NEAR Subgraph

`@graphprotocol/graph-cli` is a command-line tool for building and deploying subgraphs.

`@graphprotocol/graph-ts` is a library of subgraph-specific types.

NEAR subgraph development requires `graph-cli` above version `0.23.0`, and `graph-ts` above version `0.23.0`.

> Building a NEAR subgraph is very similar to building a subgraph that indexes Ethereum.

There are three aspects of subgraph definition:

**subgraph.yaml:** the subgraph manifest, defining the data sources of interest, and how they should be processed. NEAR is a new `kind` of data source.

**schema.graphql:** a schema file that defines what data is stored for your subgraph, and how to query it via GraphQL. The requirements for NEAR subgraphs are covered by [the existing documentation](/developing/creating-a-subgraph#the-graphql-schema).

**AssemblyScript Mappings:** [AssemblyScript code](/developing/graph-ts/api) that translates from the event data to the entities defined in your schema. NEAR support introduces NEAR-specific data types and new JSON parsing functionality.

During subgraph development there are two key commands:

```bash
$ graph codegen # generates types from the schema file identified in the manifest
$ graph build # generates Web Assembly from the AssemblyScript files, and prepares all the subgraph files in a /build folder
```

### Subgraph Manifest Definition

The subgraph manifest (`subgraph.yaml`) identifies the data sources for the subgraph, the triggers of interest, and the functions that should be run in response to those triggers. See below for an example subgraph manifest for a NEAR subgraph:

```yaml
specVersion: 0.0.2
schema:
  file: ./src/schema.graphql # link to the schema file
dataSources:
  - kind: near
    network: near-mainnet
    source:
      account: app.good-morning.near # This data source will monitor this account
      startBlock: 10662188 # Required for NEAR
    mapping:
      apiVersion: 0.0.5
      language: wasm/assemblyscript
      blockHandlers:
        - handler: handleNewBlock # the function name in the mapping file
      receiptHandlers:
        - handler: handleReceipt # the function name in the mapping file
      file: ./src/mapping.ts # link to the file with the Assemblyscript mappings
```

- NEAR subgraphs introduce a new `kind` of data source (`near`)
- The `network` should correspond to a network on the hosting Graph Node. On Subgraph Studio, NEAR's mainnet is `near-mainnet`, and NEAR's testnet is `near-testnet`
- NEAR data sources introduce an optional `source.account` field, which is a human-readable ID corresponding to a [NEAR account](https://docs.near.org/concepts/protocol/account-model). This can be an account or a sub-account.
- NEAR data sources introduce an alternative optional `source.accounts` field, which contains optional suffixes and prefixes. At least prefix or suffix must be specified, they will match the any account starting or ending with the list of values respectively. The example below would match: `[app|good].*[morning.near|morning.testnet]`. If only a list of prefixes or suffixes is necessary the other field can be omitted.

```yaml
accounts:
  prefixes:
    - app
    - good
  suffixes:
    - morning.near
    - morning.testnet
```

NEAR data sources support two types of handlers:

- `blockHandlers`: run on every new NEAR block. No `source.account` is required.
- `receiptHandlers`: run on every receipt where the data source's `source.account` is the recipient. Note that only exact matches are processed ([subaccounts](https://docs.near.org/tutorials/crosswords/basics/add-functions-call#create-a-subaccount) must be added as independent data sources).

### Schema Definition

Schema definition describes the structure of the resulting subgraph database and the relationships between entities. This is agnostic of the original data source. There are more details on subgraph schema definition [here](/developing/creating-a-subgraph#the-graphql-schema).

### AssemblyScript Mappings

The handlers for processing events are written in [AssemblyScript](https://www.assemblyscript.org/).

NEAR indexing introduces NEAR-specific data types to the [AssemblyScript API](/developing/graph-ts/api).

```typescript

class ExecutionOutcome {
      gasBurnt: u64,
      blockHash: Bytes,
      id: Bytes,
      logs: Array<string>,
      receiptIds: Array<Bytes>,
      tokensBurnt: BigInt,
      executorId: string,
  }

class ActionReceipt {
      predecessorId: string,
      receiverId: string,
      id: CryptoHash,
      signerId: string,
      gasPrice: BigInt,
      outputDataReceivers: Array<DataReceiver>,
      inputDataIds: Array<CryptoHash>,
      actions: Array<ActionValue>,
  }

class BlockHeader {
      height: u64,
      prevHeight: u64,// Always zero when version < V3
      epochId: Bytes,
      nextEpochId: Bytes,
      chunksIncluded: u64,
      hash: Bytes,
      prevHash: Bytes,
      timestampNanosec: u64,
      randomValue: Bytes,
      gasPrice: BigInt,
      totalSupply: BigInt,
      latestProtocolVersion: u32,
  }

class ChunkHeader {
      gasUsed: u64,
      gasLimit: u64,
      shardId: u64,
      chunkHash: Bytes,
      prevBlockHash: Bytes,
      balanceBurnt: BigInt,
  }

class Block {
      author: string,
      header: BlockHeader,
      chunks: Array<ChunkHeader>,
  }

class ReceiptWithOutcome {
      outcome: ExecutionOutcome,
      receipt: ActionReceipt,
      block: Block,
  }
```

These types are passed to block & receipt handlers:

- Block handlers will receive a `Block`
- Receipt handlers will receive a `ReceiptWithOutcome`

Otherwise, the rest of the [AssemblyScript API](/developing/graph-ts/api) is available to NEAR subgraph developers during mapping execution.

This includes a new JSON parsing function - logs on NEAR are frequently emitted as stringified JSONs. A new `json.fromString(...)` function is available as part of the [JSON API](/developing/graph-ts/api#json-api) to allow developers to easily process these logs.

## Deploying a NEAR Subgraph

Once you have a built subgraph, it is time to deploy it to Graph Node for indexing. NEAR subgraphs can be deployed to any Graph Node `>=v0.26.x` (this version has not yet been tagged & released).

Subgraph Studio and the upgrade Indexer on The Graph Network currently supports indexing NEAR mainnet and testnet in beta, with the following network names:

- `near-mainnet`
- `near-testnet`

More information on creating and deploying subgraphs on Subgraph Studio can be found [here](/deploying/deploying-a-subgraph-to-studio).

As a quick primer - the first step is to "create" your subgraph - this only needs to be done once. On Subgraph Studio, this can be done from [your Dashboard](https://thegraph.com/studio/): "Create a subgraph".

Once your subgraph has been created, you can deploy your subgraph by using the `graph deploy` CLI command:

```sh
$ graph create --node <graph-node-url> <subgraph-name> # creates a subgraph on a local Graph Node (on Subgraph Studio, this is done via the UI)
$ graph deploy --node <graph-node-url> --ipfs https://api.thegraph.com/ipfs/ <subgraph-name> # uploads the build files to a specified IPFS endpoint, and then deploys the subgraph to a specified Graph Node based on the manifest IPFS hash
```

The node configuration will depend on where the subgraph is being deployed.

### Subgraph Studio

```sh
graph auth --studio
graph deploy --studio <subgraph-name>
```

### Local Graph Node (based on default configuration)

```sh
graph deploy --node http://localhost:8020/ --ipfs http://localhost:5001 <subgraph-name>
```

Once your subgraph has been deployed, it will be indexed by Graph Node. You can check its progress by querying the subgraph itself:

```graphql
{
  _meta {
    block {
      number
    }
  }
}
```

### Indexing NEAR with a Local Graph Node

Running a Graph Node that indexes NEAR has the following operational requirements:

- NEAR Indexer Framework with Firehose instrumentation
- NEAR Firehose Component(s)
- Graph Node with Firehose endpoint configured

We will provide more information on running the above components soon.

## Querying a NEAR Subgraph

The GraphQL endpoint for NEAR subgraphs is determined by the schema definition, with the existing API interface. Please visit the [GraphQL API documentation](/querying/graphql-api) for more information.

## Example Subgraphs

Here are some example subgraphs for reference:

[NEAR Blocks](https://github.com/graphprotocol/graph-tooling/tree/main/examples/near-blocks)

[NEAR Receipts](https://github.com/graphprotocol/graph-tooling/tree/main/examples/near-receipts)

## FAQ

### How does the beta work?

NEAR support is in beta, which means that there may be changes to the API as we continue to work on improving the integration. Please email near@thegraph.com so that we can support you in building NEAR subgraphs, and keep you up to date on the latest developments!

### Can a subgraph index both NEAR and EVM chains?

No, a subgraph can only support data sources from one chain/network.

### Can subgraphs react to more specific triggers?

Currently, only Block and Receipt triggers are supported. We are investigating triggers for function calls to a specified account. We are also interested in supporting event triggers, once NEAR has native event support.

### Will receipt handlers trigger for accounts and their sub-accounts?

If an `account` is specified, that will only match the exact account name. It is possible to match sub-accounts by specifying an `accounts` field, with `suffixes` and `prefixes` specified to match accounts and sub-accounts, for example the following would match all `mintbase1.near` sub-accounts:

```yaml
accounts:
  suffixes:
    - mintbase1.near
```

### Can NEAR subgraphs make view calls to NEAR accounts during mappings?

This is not supported. We are evaluating whether this functionality is required for indexing.

### Can I use data source templates in my NEAR subgraph?

This is not currently supported. We are evaluating whether this functionality is required for indexing.

### Ethereum subgraphs support "pending" and "current" versions, how can I deploy a "pending" version of a NEAR subgraph?

Pending functionality is not yet supported for NEAR subgraphs. In the interim, you can deploy a new version to a different "named" subgraph, and then when that is synced with the chain head, you can redeploy to your primary "named" subgraph, which will use the same underlying deployment ID, so the main subgraph will be instantly synced.

### My question hasn't been answered, where can I get more help building NEAR subgraphs?

If it is a general question about subgraph development, there is a lot more information in the rest of the [Developer documentation](/quick-start). Otherwise please join [The Graph Protocol Discord](https://discord.gg/graphprotocol) and ask in the #near channel or email near@thegraph.com.

## References

- [NEAR developer documentation](https://docs.near.org/tutorials/crosswords/basics/set-up-skeleton)
---
title: Subgraph Best Practice 3 - Improve Indexing and Query Performance by Using Immutable Entities and Bytes as IDs
---

## TLDR

Using Immutable Entities and Bytes for IDs in our `schema.graphql` file [significantly improves ](https://thegraph.com/blog/two-simple-subgraph-performance-improvements/) indexing speed and query performance.

## Immutable Entities

To make an entity immutable, we simply add `(immutable: true)` to an entity.

```graphql
type Transfer @entity(immutable: true) {
  id: Bytes!
  from: Bytes!
  to: Bytes!
  value: BigInt!
}
```

By making the `Transfer` entity immutable, graph-node is able to process the entity more efficiently, improving indexing speeds and query responsiveness.

Immutable Entities structures will not change in the future. An ideal entity to become an Immutable Entity would be an entity that is directly logging on-chain event data, such as a `Transfer` event being logged as a `Transfer` entity.

### Under the hood

Mutable entities have a 'block range' indicating their validity. Updating these entities requires the graph node to adjust the block range of previous versions, increasing database workload. Queries also need filtering to find only live entities. Immutable entities are faster because they are all live and since they won't change, no checks or updates are required while writing, and no filtering is required during queries.

### When not to use Immutable Entities

If you have a field like `status` that needs to be modified over time, then you should not make the entity immutable. Otherwise, you should use immutable entities whenever possible.

## Bytes as IDs

Every entity requires an ID. In the previous example, we can see that the ID is already of the Bytes type.

```graphql
type Transfer @entity(immutable: true) {
  id: Bytes!
  from: Bytes!
  to: Bytes!
  value: BigInt!
}
```

While other types for IDs are possible, such as String and Int8, it is recommended to use the Bytes type for all IDs due to character strings taking twice as much space as Byte strings to store binary data, and comparisons of UTF-8 character strings must take the locale into account which is much more expensive than the bytewise comparison used to compare Byte strings.

### Reasons to Not Use Bytes as IDs

1. If entity IDs must be human-readable such as auto-incremented numerical IDs or readable strings, Bytes for IDs should not be used.
2. If integrating a subgraph’s data with another data model that does not use Bytes as IDs, Bytes as IDs should not be used.
3. Indexing and querying performance improvements are not desired.

### Concatenating With Bytes as IDs

It is a common practice in many subgraphs to use string concatenation to combine two properties of an event into a single ID, such as using `event.transaction.hash.toHex() + "-" + event.logIndex.toString()`. However, as this returns a string, this significantly impedes subgraph indexing and querying performance.

Instead, we should use the `concatI32()` method to concatenate event properties. This strategy results in a `Bytes` ID that is much more performant.

```typescript
export function handleTransfer(event: TransferEvent): void {
  let entity = new Transfer(event.transaction.hash.concatI32(event.logIndex.toI32()))
  entity.from = event.params.from
  entity.to = event.params.to
  entity.value = event.params.value

  entity.blockNumber = event.block.number
  entity.blockTimestamp = event.block.timestamp
  entity.transactionHash = event.transaction.hash

  entity.save()
}
```

### Sorting With Bytes as IDs

Sorting using Bytes as IDs is not optimal as seen in this example query and response.

Query:

```graphql
{
  transfers(first: 3, orderBy: id) {
    id
    from
    to
    value
  }
}
```

Query response:

```json
{
  "data": {
    "transfers": [
      {
        "id": "0x00010000",
        "from": "0xabcd...",
        "to": "0x1234...",
        "value": "256"
      },
      {
        "id": "0x00020000",
        "from": "0xefgh...",
        "to": "0x5678...",
        "value": "512"
      },
      {
        "id": "0x01000000",
        "from": "0xijkl...",
        "to": "0x9abc...",
        "value": "1"
      }
    ]
  }
}
```

The IDs are returned as hex.

To improve sorting, we should create another field on the entity that is a BigInt.

```graphql
type Transfer @entity {
  id: Bytes!
  from: Bytes! # address
  to: Bytes! # address
  value: BigInt! # unit256
  tokenId: BigInt! # uint256
}
```

This will allow for sorting to be optimized sequentially.

Query:

```graphql
{
  transfers(first: 3, orderBy: tokenId) {
    id
    tokenId
  }
}
```

Query Response:

```json
{
  "data": {
    "transfers": [
      {
        "id": "0x…",
        "tokenId": "1"
      },
      {
        "id": "0x…",
        "tokenId": "2"
      },
      {
        "id": "0x…",
        "tokenId": "3"
      }
    ]
  }
}
```

## Conclusion

Using both Immutable Entities and Bytes as IDs has been shown to markedly improve subgraph efficiency. Specifically, tests have highlighted up to a 28% increase in query performance and up to a 48% acceleration in indexing speeds.

Read more about using Immutable Entities and Bytes as IDs in this blog post by David Lutterkort, a Software Engineer at Edge & Node: [Two Simple Subgraph Performance Improvements](https://thegraph.com/blog/two-simple-subgraph-performance-improvements/).
---
title: Subgraph Best Practice 2 - Improve Indexing and Query Responsiveness By Using @derivedFrom
---

## TLDR

Arrays in your schema can really slow down a subgraph's performance as they grow beyond thousands of entries. If possible, the `@derivedFrom` directive should be used when using arrays as it prevents large arrays from forming, simplifies handlers, and reduces the size of individual entities, improving indexing speed and query performance significantly.

## How to Use the `@derivedFrom` Directive

You just need to add a `@derivedFrom` directive after your array in your schema. Like this:

```graphql
comments: [Comment!]! @derivedFrom(field: "post")
```

`@derivedFrom` creates efficient one-to-many relationships, enabling an entity to dynamically associate with multiple related entities based on a field in the related entity. This approach removes the need for both sides of the relationship to store duplicate data, making the subgraph more efficient.

### Example Use Case for `@derivedFrom`

An example of a dynamically growing array is a blogging platform where a “Post” can have many “Comments”.

Let’s start with our two entities, `Post` and `Comment`

Without optimization, you could implement it like this with an array:

```graphql
type Post @entity {
  id: Bytes!
  title: String!
  content: String!
  comments: [Comment!]!
}

type Comment @entity {
  id: Bytes!
  content: String!
}
```

Arrays like these will effectively store extra Comments data on the Post side of the relationship.

Here’s what an optimized version looks like using `@derivedFrom`:

```graphql
type Post @entity {
  id: Bytes!
  title: String!
  content: String!
  comments: [Comment!]! @derivedFrom(field: "post")
}

type Comment @entity {
  id: Bytes!
  content: String!
  post: Post!
}
```

Just by adding the `@derivedFrom` directive, this schema will only store the “Comments” on the “Comments” side of the relationship and not on the “Post” side of the relationship. Arrays are stored across individual rows, which allows them to expand significantly. This can lead to particularly large sizes if their growth is unbounded.

This will not only make our subgraph more efficient, but it will also unlock three features:

1. We can query the `Post` and see all of its comments.
2. We can do a reverse lookup and query any `Comment` and see which post it comes from.

3. We can use [Derived Field Loaders](/developing/graph-ts/api/#looking-up-derived-entities) to unlock the ability to directly access and manipulate data from virtual relationships in our subgraph mappings.

## Conclusion

Adopting the `@derivedFrom` directive in subgraphs effectively handles dynamically growing arrays, enhancing indexing efficiency and data retrieval.

To learn more detailed strategies to avoid large arrays, read this blog from Kevin Jones: [Best Practices in Subgraph Development: Avoiding Large Arrays](https://thegraph.com/blog/improve-subgraph-performance-avoiding-large-arrays/).
---
title: Subgraph Best Practice 4 - Improve Indexing Speed by Avoiding eth_calls
---

## TLDR

`eth_calls` are calls that can be made from a subgraph to an Ethereum node. These calls take a significant amount of time to return data, slowing down indexing. If possible, design smart contracts to emit all the data you need so you don’t need to use `eth_calls`.

## Why Avoiding `eth_calls` Is a Best Practice

Subgraphs are optimized to index event data emitted from smart contracts. A subgraph can also index the data coming from an `eth_call`, however, this can significantly slow down subgraph indexing as `eth_calls` require making external calls to smart contracts. The responsiveness of these calls relies not on the subgraph but on the connectivity and responsiveness of the Ethereum node being queried. By minimizing or eliminating eth_calls in our subgraphs, we can significantly improve our indexing speed.

### What Does an eth_call Look Like?

`eth_calls` are often necessary when the data required for a subgraph is not available through emitted events. For example, consider a scenario where a subgraph needs to identify whether ERC20 tokens are part of a specific pool, but the contract only emits a basic `Transfer` event and does not emit an event that contains the data that we need:

```yaml
event Transfer(address indexed from, address indexed to, uint256 value);
```

Suppose the tokens' pool membership is determined by a state variable named `getPoolInfo`. In this case, we would need to use an `eth_call` to query this data:

```typescript
import { Address } from '@graphprotocol/graph-ts'
import { ERC20, Transfer } from '../generated/ERC20/ERC20'
import { TokenTransaction } from '../generated/schema'

export function handleTransfer(event: Transfer): void {
  let transaction = new TokenTransaction(event.transaction.hash.toHex())

  // Bind the ERC20 contract instance to the given address:
  let instance = ERC20.bind(event.address)

  // Retrieve pool information via eth_call
  let poolInfo = instance.getPoolInfo(event.params.to)

  transaction.pool = poolInfo.toHexString()
  transaction.from = event.params.from.toHexString()
  transaction.to = event.params.to.toHexString()
  transaction.value = event.params.value

  transaction.save()
}
```

This is functional, however is not ideal as it slows down our subgraph’s indexing.

## How to Eliminate `eth_calls`

Ideally, the smart contract should be updated to emit all necessary data within events. For instance, modifying the smart contract to include pool information in the event could eliminate the need for `eth_calls`:

```
event TransferWithPool(address indexed from, address indexed to, uint256 value, bytes32 indexed poolInfo);
```

With this update, the subgraph can directly index the required data without external calls:

```typescript
import { Address } from '@graphprotocol/graph-ts'
import { ERC20, TransferWithPool } from '../generated/ERC20/ERC20'
import { TokenTransaction } from '../generated/schema'

export function handleTransferWithPool(event: TransferWithPool): void {
  let transaction = new TokenTransaction(event.transaction.hash.toHex())

  transaction.pool = event.params.poolInfo.toHexString()
  transaction.from = event.params.from.toHexString()
  transaction.to = event.params.to.toHexString()
  transaction.value = event.params.value

  transaction.save()
}
```

This is much more performant as it has eliminated the need for `eth_calls`.

## How to Optimize `eth_calls`

If modifying the smart contract is not possible and `eth_calls` are required, read “[Improve Subgraph Indexing Performance Easily: Reduce eth_calls](https://thegraph.com/blog/improve-subgraph-performance-reduce-eth-calls/)” by Simon Emanuel Schmid to learn various strategies on how to optimize `eth_calls`.

## Reducing the Runtime Overhead of `eth_calls`

For the `eth_calls` that can not be eliminated, the runtime overhead they introduce can be minimized by declaring them in the manifest. When `graph-node` processes a block it performs all declared `eth_calls` in parallel before handlers are run. Calls that are not declared are executed sequentially when handlers run. The runtime improvement comes from performing calls in parallel rather than sequentially - that helps reduce the total time spent in calls but does not eliminate it completely.

Currently, `eth_calls` can only be declared for event handlers. In the manifest, write

```yaml
event: TransferWithPool(address indexed, address indexed, uint256, bytes32 indexed)
handler: handleTransferWithPool
calls:
  ERC20.poolInfo: ERC20[event.address].getPoolInfo(event.params.to)
```

The portion highlighted in yellow is the call declaration. The part before the colon is simply a text label that is only used for error messages. The part after the colon has the form `Contract[address].function(params)`. Permissible values for address and params are `event.address` and `event.params.<name>`.

The handler itself accesses the result of this `eth_call` exactly as in the previous section by binding to the contract and making the call. graph-node caches the results of declared `eth_calls` in memory and the call from the handler will retrieve the result from this in memory cache instead of making an actual RPC call.

Note: Declared eth_calls can only be made in subgraphs with specVersion >= 1.2.0.

## Conclusion

We can significantly improve indexing performance by minimizing or eliminating `eth_calls` in our subgraphs.
---
title: Subgraph Best Practice 1 - Improve Query Speed with Subgraph Pruning
---

## TLDR

[Pruning](/developing/creating-a-subgraph/#prune) removes archival entities from the subgraph’s database up to a given block, and removing unused entities from a subgraph’s database will improve a subgraph’s query performance, often dramatically. Using `indexerHints` is an easy way to prune a subgraph.

## How to Prune a Subgraph With `indexerHints`

Add a section called `indexerHints` in the manifest.

`indexerHints` has three `prune` options:

- `prune: auto`: Retains the minimum necessary history as set by the Indexer, optimizing query performance. This is the generally recommended setting and is the default for all subgraphs created by `graph-cli` >= 0.66.0.
- `prune: <Number of blocks to retain>`: Sets a custom limit on the number of historical blocks to retain.
- `prune: never`: No pruning of historical data; retains the entire history and is the default if there is no `indexerHints` section. `prune: never` should be selected if [Time Travel Queries](/querying/graphql-api/#time-travel-queries) are desired.

We can add `indexerHints` to our subgraphs by updating our `subgraph.yaml`:

```yaml
specVersion: 1.0.0
schema:
  file: ./schema.graphql
indexerHints:
  prune: auto
dataSources:
  - kind: ethereum/contract
    name: Contract
    network: mainnet
```

## Important Considerations

- If [Time Travel Queries](/querying/graphql-api/#time-travel-queries) are desired as well as pruning, pruning must be performed accurately to retain Time Travel Query functionality. Due to this, it is generally not recommended to use `indexerHints: prune: auto` with Time Travel Queries. Instead, prune using `indexerHints: prune: <Number of blocks to retain>` to accurately prune to a block height that preserves the historical data required by Time Travel Queries, or use `prune: never` to maintain all data.

- It is not possible to [graft](/cookbook/grafting/) at a block height that has been pruned. If grafting is routinely performed and pruning is desired, it is recommended to use `indexerHints: prune: <Number of blocks to retain>` that will accurately retain a set number of blocks (e.g., enough for six months).

## Conclusion

Pruning using `indexerHints` is a best practice for subgraph development, offering significant query performance improvements.
---
title: GraphQL Validations migration guide
---

Soon `graph-node` will support 100% coverage of the [GraphQL Validations specification](https://spec.graphql.org/June2018/#sec-Validation).

Previous versions of `graph-node` did not support all validations and provided more graceful responses - so, in cases of ambiguity, `graph-node` was ignoring invalid GraphQL operations components.

GraphQL Validations support is the pillar for the upcoming new features and the performance at scale of The Graph Network.

It will also ensure determinism of query responses, a key requirement on The Graph Network.

**Enabling the GraphQL Validations will break some existing queries** sent to The Graph API.

To be compliant with those validations, please follow the migration guide.

> ⚠️ If you do not migrate your queries before the validations are rolled out, they will return errors and possibly break your frontends/clients.

## Migration guide

You can use the CLI migration tool to find any issues in your GraphQL operations and fix them. Alternatively you can update the endpoint of your GraphQL client to use the `https://api-next.thegraph.com/subgraphs/name/$GITHUB_USER/$SUBGRAPH_NAME` endpoint. Testing your queries against this endpoint will help you find the issues in your queries.

> Not all subgraphs will need to be migrated, if you are using [GraphQL ESlint](https://the-guild.dev/graphql/eslint/docs) or [GraphQL Code Generator](https://the-guild.dev/graphql/codegen), they already ensure that your queries are valid.

## Migration CLI tool

**Most of the GraphQL operations errors can be found in your codebase ahead of time.**

For this reason, we provide a smooth experience for validating your GraphQL operations during development or in CI.

[`@graphql-validate/cli`](https://github.com/saihaj/graphql-validate) is a simple CLI tool that helps validate GraphQL operations against a given schema.

### **Getting started**

You can run the tool as follows:

```bash
npx @graphql-validate/cli -s https://api-next.thegraph.com/subgraphs/name/$GITHUB_USER/$SUBGRAPH_NAME -o *.graphql
```

**Notes:**

- Set or replace $GITHUB_USER, $SUBGRAPH_NAME with the appropriate values. Like: [`artblocks/art-blocks`](https://api.thegraph.com/subgraphs/name/artblocks/art-blocks)
- The preview schema URL (https://api-next.thegraph.com/) provided is heavily rate-limited and will be sunset once all users have migrated to the new version. **Do not use it in production.**
- Operations are identified in files with the following extensions [`.graphql`,](https://www.graphql-tools.com/docs/schema-loading#graphql-file-loader)[`.ts`, `.tsx`, `.js`, `jsx`](https://www.graphql-tools.com/docs/schema-loading#code-file-loader) (`-o` option).

### CLI output

The `[@graphql-validate/cli](https://github.com/saihaj/graphql-validate)` CLI tool will output any GraphQL operations errors as follows:

![Error output from CLI](https://i.imgur.com/x1cBdhq.png)

For each error, you will find a description, file path and position, and a link to a solution example (see the following section).

## Run your local queries against the preview schema

We provide an endpoint `https://api-next.thegraph.com/` that runs a `graph-node` version that has validations turned on.

You can try out queries by sending them to:

- `https://api-next.thegraph.com/subgraphs/id/<Qm...>`

or

- `https://api-next.thegraph.com/subgraphs/name/<GITHUB_USER>/<SUBGRAPH_NAME>`

To work on queries that have been flagged as having validation errors, you can use your favorite GraphQL query tool, like Altair or [GraphiQL](https://cloud.hasura.io/public/graphiql), and try your query out. Those tools will also mark those errors in their UI, even before you run it.

## How to solve issues

Below, you will find all the GraphQL validations errors that could occur on your existing GraphQL operations.

### GraphQL variables, operations, fragments, or arguments must be unique

We applied rules for ensuring that an operation includes a unique set of GraphQL variables, operations, fragments, and arguments.

A GraphQL operation is only valid if it does not contain any ambiguity.

To achieve that, we need to ensure that some components in your GraphQL operation must be unique.

Here's an example of a few invalid operations that violates these rules:

**Duplicate Query name (#UniqueOperationNamesRule)**

```graphql
# The following operation violated the UniqueOperationName
# rule, since we have a single operation with 2 queries
# with the same name
query myData {
  id
}

query myData {
  name
}
```

_Solution:_

```graphql
query myData {
  id
}

query myData2 {
  # rename the second query
  name
}
```

**Duplicate Fragment name (#UniqueFragmentNamesRule)**

```graphql
# The following operation violated the UniqueFragmentName
# rule.
query myData {
  id
  ...MyFields
}

fragment MyFields {
  metadata
}

fragment MyFields {
  name
}
```

_Solution:_

```graphql
query myData {
  id
  ...MyFieldsName
  ...MyFieldsMetadata
}

fragment MyFieldsMetadata { # assign a unique name to fragment
  metadata
}

fragment MyFieldsName { # assign a unique name to fragment
  name
}
```

**Duplicate variable name (#UniqueVariableNamesRule)**

```graphql
# The following operation violates the UniqueVariables
query myData($id: String, $id: Int) {
  id
  ...MyFields
}
```

_Solution:_

```graphql
query myData($id: String) {
  # keep the relevant variable (here: `$id: String`)
  id
  ...MyFields
}
```

**Duplicate argument name (#UniqueArgument)**

```graphql
# The following operation violated the UniqueArguments
query myData($id: ID!) {
  userById(id: $id, id: "1") {
    id
  }
}
```

_Solution:_

```graphql
query myData($id: ID!) {
  userById(id: $id) {
    id
  }
}
```

**Duplicate anonymous query (#LoneAnonymousOperationRule)**

Also, using two anonymous operations will violate the `LoneAnonymousOperation` rule due to conflict in the response structure:

```graphql
# This will fail if executed together in
# a single operation with the following two queries:
query {
  someField
}

query {
  otherField
}
```

_Solution:_

```graphql
query {
  someField
  otherField
}
```

Or name the two queries:

```graphql
query FirstQuery {
  someField
}

query SecondQuery {
  otherField
}
```

### Overlapping Fields

A GraphQL selection set is considered valid only if it correctly resolves the eventual result set.

If a specific selection set, or a field, creates ambiguity either by the selected field or by the arguments used, the GraphQL service will fail to validate the operation.

Here are a few examples of invalid operations that violate this rule:

**Conflicting fields aliases (#OverlappingFieldsCanBeMergedRule)**

```graphql
# Aliasing fields might cause conflicts, either with
# other aliases or other fields that exist on the
# GraphQL schema.
query {
  dogs {
    name: nickname
    name
  }
}
```

_Solution:_

```graphql
query {
  dogs {
    name: nickname
    originalName: name # alias the original `name` field
  }
}
```

**Conflicting fields with arguments (#OverlappingFieldsCanBeMergedRule)**

```graphql
# Different arguments might lead to different data,
# so we can't assume the fields will be the same.
query {
  dogs {
    doesKnowCommand(dogCommand: SIT)
    doesKnowCommand(dogCommand: HEEL)
  }
}
```

_Solution:_

```graphql
query {
  dogs {
    knowsHowToSit: doesKnowCommand(dogCommand: SIT)
    knowsHowToHeel: doesKnowCommand(dogCommand: HEEL)
  }
}
```

Also, in more complex use-cases, you might violate this rule by using two fragments that might cause a conflict in the eventually expected set:

```graphql
query {
  # Eventually, we have two "x" definitions, pointing
  # to different fields!
  ...A
  ...B
}

fragment A on Type {
  x: a
}

fragment B on Type {
  x: b
}
```

In addition to that, client-side GraphQL directives like `@skip` and `@include` might lead to ambiguity, for example:

```graphql
fragment mergeSameFieldsWithSameDirectives on Dog {
  name @include(if: true)
  name @include(if: false)
}
```

[You can read more about the algorithm here.](https://spec.graphql.org/June2018/#sec-Field-Selection-Merging)

### Unused Variables or Fragments

A GraphQL operation is also considered valid only if all operation-defined components (variables, fragments) are used.

Here are a few examples for GraphQL operations that violates these rules:

**Unused variable** (#NoUnusedVariablesRule)

```graphql
# Invalid, because $someVar is never used.
query something($someVar: String) {
  someData
}
```

_Solution:_

```graphql
query something {
  someData
}
```

**Unused Fragment** (#NoUnusedFragmentsRule)

```graphql
# Invalid, because fragment AllFields is never used.
query something {
  someData
}

fragment AllFields { # unused :(
  name
  age
}
```

_Solution:_

```graphql
# Invalid, because fragment AllFields is never used.
query something {
  someData
}

# remove the `AllFields` fragment
```

### Invalid or missing Selection-Set (#ScalarLeafsRule)

Also, a GraphQL field selection is only valid if the following is validated:

- An object field must-have selection set specified.
- An edge field (scalar, enum) must not have a selection set specified.

Here are a few examples of violations of these rules with the following Schema:

```graphql
type Image {
  url: String!
}

type User {
  id: ID!
  avatar: Image!
}

type Query {
  user: User!
}
```

**Invalid Selection-Set**

```graphql
query {
  user {
    id { # Invalid, because "id" is of type ID and does not have sub-fields

    }
  }
}
```

_Solution:_

```graphql
query {
  user {
    id
  }
}
```

**Missing Selection-Set**

```graphql
query {
  user {
    id
    image # `image` requires a Selection-Set for sub-fields!
  }
}
```

_Solution:_

```graphql
query {
  user {
    id
    image {
      src
    }
  }
}
```

### Incorrect Arguments values (#VariablesInAllowedPositionRule)

GraphQL operations that pass hard-coded values to arguments must be valid, based on the value defined in the schema.

Here are a few examples of invalid operations that violate these rules:

```graphql
query purposes {
  # If "name" is defined as "String" in the schema,
  # this query will fail during validation.
  purpose(name: 1) {
    id
  }
}

# This might also happen when an incorrect variable is defined:

query purposes($name: Int!) {
  # If "name" is defined as `String` in the schema,
  # this query will fail during validation, because the
  # variable used is of type `Int`
  purpose(name: $name) {
    id
  }
}
```

### Unknown Type, Variable, Fragment, or Directive (#UnknownX)

The GraphQL API will raise an error if any unknown type, variable, fragment, or directive is used.

Those unknown references must be fixed:

- rename if it was a typo
- otherwise, remove

### Fragment: invalid spread or definition

**Invalid Fragment spread (#PossibleFragmentSpreadsRule)**

A Fragment cannot be spread on a non-applicable type.

Example, we cannot apply a `Cat` fragment to the `Dog` type:

```graphql
query {
	dog {
		...CatSimple
  }
}

fragment CatSimple on Cat {
  # ...
}
```

**Invalid Fragment definition (#FragmentsOnCompositeTypesRule)**

All Fragment must be defined upon (using `on ...`) a composite type, in short: object, interface, or union.

The following examples are invalid, since defining fragments on scalars is invalid.

```graphql
fragment fragOnScalar on Int {
  # we cannot define a fragment upon a scalar (`Int`)
  something
}

fragment inlineFragOnScalar on Dog {
  ... on Boolean {
    # `Boolean` is not a subtype of `Dog`
    somethingElse
  }
}
```

### Directives usage

**Directive cannot be used at this location (#KnownDirectivesRule)**

Only GraphQL directives (`@...`) supported by The Graph API can be used.

Here is an example with The GraphQL supported directives:

```graphql
query {
  dog {
    name @include(true)
    age @skip(true)
  }
}
```

_Note: `@stream`, `@live`, `@defer` are not supported._

**Directive can only be used once at this location (#UniqueDirectivesPerLocationRule)**

The directives supported by The Graph can only be used once per location.

The following is invalid (and redundant):

```graphql
query {
  dog {
    name @include(true) @include(true)
  }
}
```
---
title: AssemblyScript Migration Guide
---

Up until now, subgraphs have been using one of the [first versions of AssemblyScript](https://github.com/AssemblyScript/assemblyscript/tree/v0.6) (v0.6). Finally we've added support for the [newest one available](https://github.com/AssemblyScript/assemblyscript/tree/v0.19.10) (v0.19.10)! 🎉

That will enable subgraph developers to use newer features of the AS language and standard library.

This guide is applicable for anyone using `graph-cli`/`graph-ts` below version `0.22.0`. If you're already at a higher than (or equal) version to that, you've already been using version `0.19.10` of AssemblyScript 🙂

> Note: As of `0.24.0`, `graph-node` can support both versions, depending on the `apiVersion` specified in the subgraph manifest.

## Features

### New functionality

- `TypedArray`s can now be built from `ArrayBuffer`s by using the [new `wrap` static method](https://www.assemblyscript.org/stdlib/typedarray.html#static-members) ([v0.8.1](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.8.1))
- New standard library functions: `String#toUpperCase`, `String#toLowerCase`, `String#localeCompare`and `TypedArray#set` ([v0.9.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.9.0))
- Added support for x instanceof GenericClass ([v0.9.2](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.9.2))
- Added `StaticArray<T>`, a more efficient array variant ([v0.9.3](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.9.3))
- Added `Array<T>#flat` ([v0.10.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.10.0))
- Implemented `radix` argument on `Number#toString` ([v0.10.1](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.10.1))
- Added support for separators in floating point literals ([v0.13.7](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.13.7))
- Added support for first class functions ([v0.14.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.14.0))
- Add builtins: `i32/i64/f32/f64.add/sub/mul` ([v0.14.13](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.14.13))
- Implement `Array/TypedArray/String#at` ([v0.18.2](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.18.2))
- Added support for template literal strings ([v0.18.17](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.18.17))
- Add `encodeURI(Component)` and `decodeURI(Component)` ([v0.18.27](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.18.27))
- Add `toString`, `toDateString` and `toTimeString` to `Date` ([v0.18.29](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.18.29))
- Add `toUTCString` for `Date` ([v0.18.30](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.18.30))
- Add `nonnull/NonNullable` builtin type ([v0.19.2](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.19.2))

### Optimizations

- `Math` functions such as `exp`, `exp2`, `log`, `log2` and `pow` have been replaced by faster variants ([v0.9.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.9.0))
- Slightly optimize `Math.mod` ([v0.17.1](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.17.1))
- Cache more field accesses in std Map and Set ([v0.17.8](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.17.8))
- Optimize for powers of two in `ipow32/64` ([v0.18.2](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.18.2))

### Other

- The type of an array literal can now be inferred from its contents ([v0.9.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.9.0))
- Updated stdlib to Unicode 13.0.0 ([v0.10.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.10.0))

## How to upgrade?

1. Change your mappings `apiVersion` in `subgraph.yaml` to `0.0.6`:

```yaml
...
dataSources:
  ...
    mapping:
      ...
      apiVersion: 0.0.6
      ...
```

2. Update the `graph-cli` you're using to the `latest` version by running:

```bash
# if you have it globally installed
npm install --global @graphprotocol/graph-cli@latest

# or in your subgraph if you have it as a dev dependency
npm install --save-dev @graphprotocol/graph-cli@latest
```

3. Do the same for `graph-ts`, but instead of installing globally, save it in your main dependencies:

```bash
npm install --save @graphprotocol/graph-ts@latest
```

4. Follow the rest of the guide to fix the language breaking changes.
5. Run `codegen` and `deploy` again.

## Breaking changes

### Nullability

On the older version of AssemblyScript, you could create code like this:

```typescript
function load(): Value | null { ... }

let maybeValue = load();
maybeValue.aMethod();
```

However on the newer version, because the value is nullable, it requires you to check, like this:

```typescript
let maybeValue = load()

if (maybeValue) {
  maybeValue.aMethod() // `maybeValue` is not null anymore
}
```

Or force it like this:

```typescript
let maybeValue = load()! // breaks in runtime if value is null

maybeValue.aMethod()
```

If you are unsure which to choose, we recommend always using the safe version. If the value doesn't exist you might want to just do an early if statement with a return in you subgraph handler.

### Variable Shadowing

Before you could do [variable shadowing](https://en.wikipedia.org/wiki/Variable_shadowing) and code like this would work:

```typescript
let a = 10
let b = 20
let a = a + b
```

However now this isn't possible anymore, and the compiler returns this error:

```typescript
ERROR TS2451: Cannot redeclare block-scoped variable 'a'

 let a = a + b;
 ~~~~~~~~~~~~~
in assembly/index.ts(4,3)
```

You'll need to rename your duplicate variables if you had variable shadowing.

### Null Comparisons

By doing the upgrade on your subgraph, sometimes you might get errors like these:

```typescript
ERROR TS2322: Type '~lib/@graphprotocol/graph-ts/common/numbers/BigInt | null' is not assignable to type '~lib/@graphprotocol/graph-ts/common/numbers/BigInt'.
     if (decimals == null) {
                     ~~~~
 in src/mappings/file.ts(41,21)
```

To solve you can simply change the `if` statement to something like this:

```typescript
  if (!decimals) {

  // or

  if (decimals === null) {
```

The same applies if you're doing != instead of ==.

### Casting

The common way to do casting before was to just use the `as` keyword, like this:

```typescript
let byteArray = new ByteArray(10)
let uint8Array = byteArray as Uint8Array // equivalent to: <Uint8Array>byteArray
```

However this only works in two scenarios:

- Primitive casting (between types such as `u8`, `i32`, `bool`; eg: `let b: isize = 10; b as usize`);
- Upcasting on class inheritance (subclass → superclass)

Examples:

```typescript
// primitive casting
let a: usize = 10
let b: isize = 5
let c: usize = a + (b as usize)
```

```typescript
// upcasting on class inheritance
class Bytes extends Uint8Array {}

let bytes = new Bytes(2)
// <Uint8Array>bytes // same as: bytes as Uint8Array
```

There are two scenarios where you may want to cast, but using `as`/`<T>var` **isn't safe**:

- Downcasting on class inheritance (superclass → subclass)
- Between two types that share a superclass

```typescript
// downcasting on class inheritance
class Bytes extends Uint8Array {}

let uint8Array = new Uint8Array(2)
// <Bytes>uint8Array // breaks in runtime :(
```

```typescript
// between two types that share a superclass
class Bytes extends Uint8Array {}
class ByteArray extends Uint8Array {}

let bytes = new Bytes(2)
// <ByteArray>bytes // breaks in runtime :(
```

For those cases, you can use the `changetype<T>` function:

```typescript
// downcasting on class inheritance
class Bytes extends Uint8Array {}

let uint8Array = new Uint8Array(2)
changetype<Bytes>(uint8Array) // works :)
```

```typescript
// between two types that share a superclass
class Bytes extends Uint8Array {}
class ByteArray extends Uint8Array {}

let bytes = new Bytes(2)
changetype<ByteArray>(bytes) // works :)
```

If you just want to remove nullability, you can keep using the `as` operator (or `<T>variable`), but make sure you know that value can't be null, otherwise it will break.

```typescript
// remove nullability
let previousBalance = AccountBalance.load(balanceId) // AccountBalance | null

if (previousBalance != null) {
  return previousBalance as AccountBalance // safe remove null
}

let newBalance = new AccountBalance(balanceId)
```

For the nullability case we recommend taking a look at the [nullability check feature](https://www.assemblyscript.org/basics.html#nullability-checks), it will make your code cleaner 🙂

Also we've added a few more static methods in some types to ease casting, they are:

- Bytes.fromByteArray
- Bytes.fromUint8Array
- BigInt.fromByteArray
- ByteArray.fromBigInt

### Nullability check with property access

To use the [nullability check feature](https://www.assemblyscript.org/basics.html#nullability-checks) you can use either `if` statements or the ternary operator (`?` and `:`) like this:

```typescript
let something: string | null = 'data'

let somethingOrElse = something ? something : 'else'

// or

let somethingOrElse

if (something) {
  somethingOrElse = something
} else {
  somethingOrElse = 'else'
}
```

However that only works when you're doing the `if` / ternary on a variable, not on a property access, like this:

```typescript
class Container {
  data: string | null
}

let container = new Container()
container.data = 'data'

let somethingOrElse: string = container.data ? container.data : 'else' // doesn't compile
```

Which outputs this error:

```typescript
ERROR TS2322: Type '~lib/string/String | null' is not assignable to type '~lib/string/String'.

   let somethingOrElse: string = container.data ? container.data : "else";
                                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

To fix this issue, you can create a variable for that property access so that the compiler can do the nullability check magic:

```typescript
class Container {
  data: string | null
}

let container = new Container()
container.data = 'data'

let data = container.data

let somethingOrElse: string = data ? data : 'else' // compiles just fine :)
```

### Operator overloading with property access

If you try to sum (for example) a nullable type (from a property access) with a non nullable one, the AssemblyScript compiler instead of giving a compile time error warning that one of the values is nullable, it just compiles silently, giving chance for the code to break at runtime.

```typescript
class BigInt extends Uint8Array {
  @operator('+')
  plus(other: BigInt): BigInt {
    // ...
  }
}

class Wrapper {
  public constructor(public n: BigInt | null) {}
}

let x = BigInt.fromI32(2)
let y: BigInt | null = null

x + y // give compile time error about nullability

let wrapper = new Wrapper(y)

wrapper.n = wrapper.n + x // doesn't give compile time errors as it should
```

We've opened a issue on the AssemblyScript compiler for this, but for now if you do these kind of operations in your subgraph mappings, you should change them to do a null check before it.

```typescript
let wrapper = new Wrapper(y)

if (!wrapper.n) {
  wrapper.n = BigInt.fromI32(0)
}

wrapper.n = wrapper.n + x // now `n` is guaranteed to be a BigInt
```

### Value initialization

If you have any code like this:

```typescript
var value: Type // null
value.x = 10
value.y = 'content'
```

It will compile but break at runtime, that happens because the value hasn't been initialized, so make sure your subgraph has initialized their values, like this:

```typescript
var value = new Type() // initialized
value.x = 10
value.y = 'content'
```

Also if you have nullable properties in a GraphQL entity, like this:

```graphql
type Total @entity {
  id: Bytes!
  amount: BigInt
}
```

And you have code similar to this:

```typescript
let total = Total.load('latest')

if (total === null) {
  total = new Total('latest')
}

total.amount = total.amount + BigInt.fromI32(1)
```

You'll need to make sure to initialize the `total.amount` value, because if you try to access like in the last line for the sum, it will crash. So you either initialize it first:

```typescript
let total = Total.load('latest')

if (total === null) {
  total = new Total('latest')
  total.amount = BigInt.fromI32(0)
}

total.tokens = total.tokens + BigInt.fromI32(1)
```

Or you can just change your GraphQL schema to not use a nullable type for this property, then we'll initialize it as zero on the `codegen` step 😉

```graphql
type Total @entity {
  id: Bytes!
  amount: BigInt!
}
```

```typescript
let total = Total.load('latest')

if (total === null) {
  total = new Total('latest') // already initializes non-nullable properties
}

total.amount = total.amount + BigInt.fromI32(1)
```

### Class property initialization

If you export any classes with properties that are other classes (declared by you or by the standard library) like this:

```typescript
class Thing {}

export class Something {
  value: Thing
}
```

The compiler will error because you either need to add an initializer for the properties that are classes, or add the `!` operator:

```typescript
export class Something {
  constructor(public value: Thing) {}
}

// or

export class Something {
  value: Thing

  constructor(value: Thing) {
    this.value = value
  }
}

// or

export class Something {
  value!: Thing
}
```

### Array initialization

The `Array` class still accepts a number to initialize the length of the list, however you should take care because operations like `.push` will actually increase the size instead of adding to the beginning, for example:

```typescript
let arr = new Array<string>(5) // ["", "", "", "", ""]

arr.push('something') // ["", "", "", "", "", "something"] // size 6 :(
```

Depending on the types you're using, eg nullable ones, and how you're accessing them, you might encounter a runtime error like this one:

```
ERRO Handler skipped due to execution failure, error: Mapping aborted at ~lib/array.ts, line 110, column 40, with message: Element type must be nullable if array is holey  wasm backtrace:     0: 0x19c4 - <unknown>!~lib/@graphprotocol/graph-ts/index/format         1: 0x1e75 - <unknown>!~lib/@graphprotocol/graph-ts/common/collections/Entity#constructor        2: 0x30b9 - <unknown>!node_modules/@graphprotocol/graph-ts/global/global/id_of_type
```

To actually push at the beginning you should either, initialize the `Array` with size zero, like this:

```typescript
let arr = new Array<string>(0) // []

arr.push('something') // ["something"]
```

Or you should mutate it via index:

```typescript
let arr = new Array<string>(5) // ["", "", "", "", ""]

arr[0] = 'something' // ["something", "", "", "", ""]
```

### GraphQL schema

This is not a direct AssemblyScript change, but you may have to update your `schema.graphql` file.

Now you no longer can define fields in your types that are Non-Nullable Lists. If you have a schema like this:

```graphql
type Something @entity {
  id: Bytes!
}

type MyEntity @entity {
  id: Bytes!
  invalidField: [Something]! # no longer valid
}
```

You'll have to add an `!` to the member of the List type, like this:

```graphql
type Something @entity {
  id: Bytes!
}

type MyEntity @entity {
  id: Bytes!
  invalidField: [Something!]! # valid
}
```

This changed because of nullability differences between AssemblyScript versions, and it's related to the `src/generated/schema.ts` file (default path, you might have changed this).

### Other

- Aligned `Map#set` and `Set#add` with the spec, returning `this` ([v0.9.2](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.9.2))
- Arrays no longer inherit from ArrayBufferView, but are now distinct ([v0.10.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.10.0))
- Classes initialized from object literals can no longer define a constructor ([v0.10.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.10.0))
- The result of a `**` binary operation is now the common denominator integer if both operands are integers. Previously, the result was a float as if calling `Math/f.pow` ([v0.11.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.11.0))
- Coerce `NaN` to `false` when casting to `bool` ([v0.14.9](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.14.9))
- When shifting a small integer value of type `i8`/`u8` or `i16`/`u16`, only the 3 respectively 4 least significant bits of the RHS value affect the result, analogous to the result of an `i32.shl` only being affected by the 5 least significant bits of the RHS value. Example: `someI8 << 8` previously produced the value `0`, but now produces `someI8` due to masking the RHS as `8 & 7 = 0` (3 bits) ([v0.17.0](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.17.0))
- Bug fix of relational string comparisons when sizes differ ([v0.17.8](https://github.com/AssemblyScript/assemblyscript/releases/tag/v0.17.8))
---
title: Substreams Triggers
---

Custom triggers allow you to send data directly into your subgraph mappings file and entities (similar to tables and fields), enabling full use of the GraphQL layer. By importing the Protobuf definitions emitted by your Substreams module, you can receive and process this data within your subgraph’s handler, ensuring efficient and streamlined data management within the subgraph framework.

> Note: If you haven’t already, visit one of the How-To Guides found [here](./introduction) to scaffold your first project in the Development Container.

The following code demonstrates how to define a `handleTransactions` function in a subgraph handler. This function receives raw Substreams bytes as a parameter and decodes them into a `Transactions` object. For each transaction, a new subgraph entity is created.

```tsx
export function handleTransactions(bytes: Uint8Array): void {
  let transactions = assembly.eth.transaction.v1.Transactions.decode(bytes.buffer).trasanctions // 1.
  if (transactions.length == 0) {
    log.info('No transactions found', [])
    return
  }

  for (let i = 0; i < transactions.length; i++) {
    // 2.
    let transaction = transactions[i]

    let entity = new Transaction(transaction.hash) // 3.
    entity.from = transaction.from
    entity.to = transaction.to
    entity.save()
  }
}
```

Here's what you’re seeing in the `mappings.ts` file:

1. The bytes containing Substreams data are decoded into the generated `Transactions` object, this object is used like any other AssemblyScript object
2. Looping over the transactions
3. Create a new subgraph entity for every transaction

To go through a detailed example of a trigger-based subgraph, [click here](./triggers-example).
---
title: Introduction to Substreams-powered Subgraphs
---

By using a Substreams package (`.spkg`) as a data source, your subgraph gains access to a stream of pre-indexed blockchain data. This enables more efficient and scalable data handling, especially with large or complex blockchain networks.

There are two methods of enabling this technology:

Using Substreams [triggers](./triggers): Consume from any Substreams module by importing the Protobuf model through a subgraph handler and move all your logic into a subgraph. This method creates the subgraph entities directly in the subgraph.

Using [Entity Changes](https://substreams.streamingfast.io/documentation/consume/subgraph/graph-out): By writing more of the logic into Substreams, you can consume the module's output directly into graph-node. In graph-node, you can use the Substreams data to create your subgraph entities.

It is really a matter of where you put your logic, in the subgraph or the Substreams. Keep in mind that having more of your logic in Substreams benefits from a parallelized model, whereas triggers will be linearly consumed in graph-node.

Visit the following links for How-To Guides on using code-generation tooling to build your first end-to-end project quickly:

- [Solana](https://substreams.streamingfast.io/documentation/how-to-guides/solana)
- [EVM](https://substreams.streamingfast.io/documentation/how-to-guides/evm)
- [Injective](https://substreams.streamingfast.io/documentation/how-to-guides/injective)
---
title: 'Tutorial: Set Up a Substreams-Powered Subgraph on Solana'
---

## Prerequisites

Before starting, make sure to:

- Complete the [Getting Started Guide](https://github.com/streamingfast/substreams-starter) to set up your development environment using a Dev Container.
- Be familiar with The Graph and basic blockchain concepts such as transactions and Protobufs.

## Step 1: Initialize Your Project

<VideoEmbed youtube="satdwdbvzAQ" />

1. Open your Dev Container and run the following command to initialize your project:

   ```bash
   substreams init
   ```

2. Select the "minimal" project option.
3. Replace the contents of the generated `substreams.yaml` file with the following configuration, which filters transactions for the Orca account on the SPL token program ID:

```yaml
specVersion: v0.1.0
package:
  name: my_project_sol
  version: v0.1.0

imports: # Pass your spkg of interest
  solana: https://github.com/streamingfast/substreams-solana-spl-token/raw/master/tokens/solana-spl-token-v0.1.0.spkg

modules:
  - name: map_spl_transfers
    use: solana:map_block # Select corresponding modules available within your spkg
    initialBlock: 260000082

  - name: map_transactions_by_programid
    use: solana:solana:transactions_by_programid_without_votes

network: solana-mainnet-beta

params: # Modify the param fields to meet your needs
  # For program_id: TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA
  map_spl_transfers: token_contract:orcaEKTdK7LKz57vaAYr9QeNsVEPfiu6QeMU1kektZE
```

## Step 2: Generate the Subgraph Manifest

Once the project is initialized, generate a subgraph manifest by running the following command in the Dev Container:

```bash
substreams codegen subgraph
```

You will generate a`subgraph.yaml` manifest which imports the Substreams package as a data source:

```yaml
---
dataSources:
  - kind: substreams
    name: my_project_sol
    network: solana-mainnet-beta
    source:
      package:
        moduleName: map_spl_transfers # Module defined in the substreams.yaml
        file: ./my-project-sol-v0.1.0.spkg
    mapping:
      apiVersion: 0.0.7
      kind: substreams/graph-entities
      file: ./src/mappings.ts
      handler: handleTriggers
```

## Step 3: Define Entities in `schema.graphql`

Define the fields you want to save in your subgraph entities by updating the `schema.graphql` file. Here is an example:

```graphql
type MyTransfer @entity {
  id: ID!
  amount: String!
  source: String!
  designation: String!
  signers: [String!]!
}
```

This schema defines a `MyTransfer` entity with fields such as `id`, `amount`, `source`, `designation`, and `signers`.

## Step 4: Handle Substreams Data in `mappings.ts`

With the Protobuf objects generated, you can now handle the decoded Substreams data in your `mappings.ts` file found in the `./src` directory. The example below demonstrates how to extract to subgraph entities the non-derived transfers associated to the Orca account id:

```ts
import { Protobuf } from 'as-proto/assembly'
import { Events as protoEvents } from './pb/sf/solana/spl/token/v1/Events'
import { MyTransfer } from '../generated/schema'

export function handleTriggers(bytes: Uint8Array): void {
  const input: protoEvents = Protobuf.decode<protoEvents>(bytes, protoEvents.decode)

  for (let i = 0; i < input.data.length; i++) {
    const event = input.data[i]

    if (event.transfer != null) {
      let entity_id: string = `${event.txnId}-${i}`
      const entity = new MyTransfer(entity_id)
      entity.amount = event.transfer!.instruction!.amount.toString()
      entity.source = event.transfer!.accounts!.source
      entity.designation = event.transfer!.accounts!.destination

      if (event.transfer!.accounts!.signer!.single != null) {
        entity.signers = [event.transfer!.accounts!.signer!.single!.signer]
      } else if (event.transfer!.accounts!.signer!.multisig != null) {
        entity.signers = event.transfer!.accounts!.signer!.multisig!.signers
      }
      entity.save()
    }
  }
}
```

## Step 5: Generate Protobuf Files

To generate Protobuf objects in AssemblyScript, run the following command:

```bash
npm run protogen
```

This command converts the Protobuf definitions into AssemblyScript, allowing you to use them in the subgraph's handler.

## Conclusion

You’ve successfully set up a trigger-based Substreams-powered subgraph for a Solana SPL token. You can now further customize your schema, mappings, and modules to suit your specific use case.

For more advanced customization and optimizations, check out the official [Substreams documentation](https://substreams.streamingfast.io/tutorials/solana).
---
title: Substreams
---

![Substreams Logo](/img/substreams-logo.png)

Substreams is a powerful blockchain indexing technology designed to enhance performance and scalability within The Graph Network. It offers the following features:

- **Accelerated Indexing**: Substreams reduce subgraph indexing time thanks to a parallelized engine, enabling faster data retrieval and processing.
- **Multi-Chain Support**: Substreams expand indexing capabilities beyond EVM-based chains, supporting ecosystems like Solana, Injective, Starknet, and Vara.
- **Multi-Sink Support:** Subgraph, Postgres database, Clickhouse, Mongo database

## How Substreams Works in 4 Steps

1. **You write a Rust program, which defines the transformations that you want to apply to the blockchain data.** For example, the following Rust function extracts relevant information from an Ethereum block (number, hash, and parent hash).

```rust
fn get_my_block(blk: Block) -> Result<MyBlock, substreams::errors::Error> {
    let header = blk.header.as_ref().unwrap();

    Ok(MyBlock {
        number: blk.number,
        hash: Hex::encode(&blk.hash),
        parent_hash: Hex::encode(&header.parent_hash),
    })
}
```

2. **You wrap up your Rust program into a WASM module just by running a single CLI command.**

3. **The WASM container is sent to a Substreams endpoint for execution.** The Substreams provider feeds the WASM container with the blockchain data and the transformations are applied.

4. **You select a [sink](https://substreams.streamingfast.io/documentation/consume/other-sinks), a place where you want to send the transformed data** (a Postgres database or a Subgraph, for example).

## Substreams Documentation

The official Substreams documentation is currently maintained by the StreamingFast team [on the StreamingFast website](https://substreams.streamingfast.io/).

To learn about the latest version of Substreams CLI, which enables developers to bootstrap a Substreams project without any code, please check [Substreams Codegen](https://streamingfastio.medium.com/substreams-codegen-no-code-tool-to-bootstrap-your-project-a11efe0378c6).

### Getting Started

- In order to develop and deploy a Substreams, [you must install the Substreams CLI](https://substreams.streamingfast.io/documentation/consume/installing-the-cli).
- Then, run your first Substreams by following the [Quickstart Tutorial](https://substreams.streamingfast.io/documentation/develop/init-project).

### Expand Your Knowledge

- Take a look at the [Ethereum Explorer Tutorial](https://substreams.streamingfast.io/tutorials/evm) to learn about the basic transformations you can create with Substreams.

### Substreams Registry

A Substreams package is a precompiled binary file that defines the specific data you want to extract from the blockchain, similar to the `mapping.ts` file in traditional subgraphs. Visit [substreams.dev](https://substreams.dev/) to explore a growing collection of ready-to-use Substreams packages across various blockchain networks.
---
title: Transfer and Deprecate a Subgraph
---

## Transferring ownership of a subgraph

Subgraphs published to the decentralized network have an NFT minted to the address that published the subgraph. The NFT is based on a standard ERC721, which facilitates transfers between accounts on The Graph Network.

**Please note the following:**

- Whoever owns the NFT controls the subgraph.
- If the owner decides to sell or transfer the NFT, they will no longer be able to edit or update that subgraph on the network.
- You can easily move control of a subgraph to a multi-sig.
- A community member can create a subgraph on behalf of a DAO.

### View your subgraph as an NFT

To view your subgraph as an NFT, you can visit an NFT marketplace like **OpenSea**:

```
https://opensea.io/your-wallet-address
```

Or a wallet explorer like **Rainbow.me**:

```
https://rainbow.me/your-wallet-addres
```

### Step-by-Step

To transfer ownership of a subgraph, do the following:

1.  Use the UI built into Subgraph Studio:

    ![Subgraph Ownership Transfer](/img/subgraph-ownership-transfer-1.png)

2.  Choose the address that you would like to transfer the subgraph to:

    ![Subgraph Ownership Trasfer](/img/subgraph-ownership-transfer-2.png)

Optionally, you can also use the built-in UI of NFT marketplaces like OpenSea:

![Subgraph Ownership Transfer from NFT marketplace](/img/subgraph-ownership-transfer-nft-marketplace.png)

## Deprecating a subgraph

Although you cannot delete a subgraph, you can deprecate it on Graph Explorer.

### Step-by-Step

To deprecate your subgraph, do the following:

1.  Visit the contract address for Arbitrum One subgraphs [here](https://arbiscan.io/address/0xec9A7fb6CbC2E41926127929c2dcE6e9c5D33Bec#writeProxyContract).
2.  Call `deprecateSubgraph` with your `SubgraphID` as your argument.
3.  Your subgraph will no longer appear in searches on Graph Explorer.

**Please note the following:**

- The owner's wallet should call the `deprecateSubgraph` function.
- Curators will not be able to signal on the subgraph anymore.
- Curators that already signaled on the subgraph can withdraw their signal at an average share price.
- Deprecated subgraphs will show an error message.

> If you interacted with the deprecated subgraph, you can find it in your user profile under the "Subgraphs", "Indexing", or "Curating" tab, respectively.
---
title: Firehose
---

![Firehose Logo](/img/firehose-logo.png)

Firehose is a new technology developed by StreamingFast working with The Graph Foundation. The product provides **previously unseen capabilities and speeds for indexing blockchain data** using a files-based and streaming-first approach.

The Graph merges into Go Ethereum/geth with the adoption of [Live Tracer with v1.14.0 release](https://github.com/ethereum/go-ethereum/releases/tag/v1.14.0).

Firehose extracts, transforms and saves blockchain data in a highly performant file-based strategy. Blockchain developers can then access data extracted by Firehose through binary data streams. Firehose is intended to stand as a replacement for The Graph’s original blockchain data extraction layer.

## Firehose Documentation

The Firehose documentation is currently maintained by the StreamingFast team [on the StreamingFast website](https://firehose.streamingfast.io/).

### Getting Started

- Read this [Firehose introduction](https://firehose.streamingfast.io/introduction/firehose-overview) to get an overview of what it is and why it was built.
- Learn about the [Prerequisites](https://firehose.streamingfast.io/introduction/prerequisites) to install and deploy Firehose.

### Expand Your Knowledge

- Learn about the different [Firehose components](https://firehose.streamingfast.io/architecture/components) available.
---
title: Billing
---

## Subgraph Billing Plans

There are two plans to use when querying subgraphs on The Graph Network.

- **Free Plan**: The Free Plan includes 100,000 free monthly queries with full access to the Subgraph Studio testing environment. This plan is designed for hobbyists, hackathoners, and those with side projects to try out The Graph before scaling their dapp.

- **Growth Plan**: The Growth Plan includes everything in the Free Plan with all queries after 100,000 monthly queries requiring payments with GRT or credit card. The Growth Plan is flexible enough to cover teams that have established dapps across a variety of use cases.

<VideoEmbed youtube="Nn771WagX2I" />

## Query Payments with credit card

- To set up billing with credit/debit cards, users should access Subgraph Studio (https://thegraph.com/studio/)
  1. Go to the [Subgraph Studio Billing page](https://thegraph.com/studio/billing/).
  2. Click on the "Connect Wallet" button on the top right corner of the page. You'll be redirected to the wallet selection page. Select your wallet and click on "Connect".
  3. Choose “Upgrade plan” if you are upgrading from the Free Plan or choose “Manage Plan” if you have already added GRT to your billing balance in the past. Next, you can estimate the number of queries to get a pricing estimate, but this is not a required step.
  4. To choose a credit card payment, choose “Credit card” as the payment method and fill out your credit card information. Those who have used Stripe before can use the Link feature to autofill their details.
- Invoices will be processed at the end of each month and require an active credit card on file for all queries beyond the free plan quota.

## Query Payments with GRT

Subgraph users can use The Graph Token (or GRT) to pay for queries on The Graph Network. With GRT, invoices will be processed at the end of each month and require a sufficient balance of GRT to make queries beyond the Free Plan quota of 100,000 monthly queries. You'll be required to pay fees generated from your API keys. Using the billing contract, you'll be able to:

- Add and withdraw GRT from your account balance.
- Keep track of your balances based on how much GRT you have added to your account balance, how much you have removed, and your invoices.
- Automatically pay invoices based on query fees generated, as long as there is enough GRT in your account balance.

### GRT on Arbitrum or Ethereum

The Graph’s billing system accepts GRT on Arbitrum, and users will need ETH on Arbitrum to pay their gas. While The Graph protocol started on Ethereum Mainnet, all activity, including the billing contracts, is now on Arbitrum One.

To pay for queries, you need GRT on Arbitrum. Here are a few different ways to achieve this:

- If you already have GRT on Ethereum, you can bridge it to Arbitrum. You can do this via the GRT bridging option provided in Subgraph Studio or by using one of the following bridges:

- [The Arbitrum Bridge](https://bridge.arbitrum.io/?l2ChainId=42161)
- [TransferTo](https://transferto.xyz/swap)

- If you already have assets on Arbitrum, you can swap them for GRT via a swapping protocol like Uniswap.

- Alternatively, you acquire GRT directly on Arbitrum through a decentralized exchange.

> This section is written assuming you already have GRT in your wallet, and you're on Arbitrum. If you don't have GRT, you can learn how to get GRT [here](#getting-grt).

Once you bridge GRT, you can add it to your billing balance.

### Adding GRT using a wallet

1. Go to the [Subgraph Studio Billing page](https://thegraph.com/studio/billing/).
2. Click on the "Connect Wallet" button on the top right corner of the page. You'll be redirected to the wallet selection page. Select your wallet and click on "Connect".
3. Select the "Manage" button near the top right corner. First time users will see an option to "Upgrade to Growth plan" while returning users will click "Deposit from wallet".
4. Use the slider to estimate the number of queries you expect to make on a monthly basis.
   - For suggestions on the number of queries you may use, see our **Frequently Asked Questions** page.
5. Choose "Cryptocurrency". GRT is currently the only cryptocurrency accepted on The Graph Network.
6. Select the number of months you would like to prepay.
   - Paying in advance does not commit you to future usage. You will only be charged for what you use and you can withdraw your balance at any time.
7. Pick the network from which you are depositing your GRT. GRT on Arbitrum or Ethereum are both acceptable.
8. Click "Allow GRT Access" and then specify the amount of GRT that can be taken from you wallet.
   - If you are prepaying for multiple months, you must allow access to the amount that corresponds with that amount. This interaction will not cost any gas.
9. Lastly, click on "Add GRT to Billing Balance". This transaction will require ETH on Arbitrum to cover the gas costs.

- Note that GRT deposited from Arbitrum will process within a few moments while GRT deposited from Ethereum will take approximately 15-20 minutes to process. Once the transaction is confirmed, you'll see the GRT added to your account balance.

### Withdrawing GRT using a wallet

1. Go to the [Subgraph Studio Billing page](https://thegraph.com/studio/billing/).
2. Click on the "Connect Wallet" button on the top right corner of the page. Select your wallet and click on "Connect".
3. Click the "Manage" button at the top right corner of the page. Select "Withdraw GRT". A side panel will appear.
4. Enter the amount of GRT you would like to withdraw.
5. Click 'Withdraw GRT' to withdraw the GRT from your account balance. Sign the associated transaction in your wallet. This will cost gas. The GRT will be sent to your Arbitrum wallet.
6. Once the transaction is confirmed, you'll see the GRT withdrawn from your account balance in your Arbitrum wallet.

### Adding GRT using a multisig wallet

1. Go to the [Subgraph Studio Billing page](https://thegraph.com/studio/billing/).
2. Click on the "Connect Wallet" button on the top right corner of the page. Select your wallet and click on "Connect". If you're using [Gnosis-Safe](https://gnosis-safe.io/), you'll be able to connect your multisig as well as your signing wallet. Then, sign the associated message. This will not cost any gas.
3. Select the "Manage" button near the top right corner. First time users will see an option to "Upgrade to Growth plan" while returning users will click "Deposit from wallet".
4. Use the slider to estimate the number of queries you expect to make on a monthly basis.
   - For suggestions on the number of queries you may use, see our **Frequently Asked Questions** page.
5. Choose "Cryptocurrency". GRT is currently the only cryptocurrency accepted on The Graph Network.
6. Select the number of months you would like to prepay.
   - Paying in advance does not commit you to future usage. You will only be charged for what you use and you can withdraw your balance at any time.
7. Pick the network from which you are depositing your GRT. GRT on Arbitrum or Ethereum are both acceptable. 8. Click "Allow GRT Access" and then specify the amount of GRT that can be taken from you wallet.
   - If you are prepaying for multiple months, you must allow access to the amount that corresponds with that amount. This interaction will not cost any gas.
8. Lastly, click on "Add GRT to Billing Balance". This transaction will require ETH on Arbitrum to cover the gas costs.

- Note that GRT deposited from Arbitrum will process within a few moments while GRT deposited from Ethereum will take approximately 15-20 minutes to process. Once the transaction is confirmed, you'll see the GRT added to your account balance.

## Getting GRT

This section will show you how to get GRT to pay for query fees.

### Coinbase

This will be a step by step guide for purchasing GRT on Coinbase.

1. Go to [Coinbase](https://www.coinbase.com/) and create an account.
2. Once you have created an account, you will need to verify your identity through a process known as KYC (or Know Your Customer). This is a standard procedure for all centralized or custodial crypto exchanges.
3. Once you have verified your identity, you can purchase GRT. You can do this by clicking on the "Buy/Sell" button on the top right of the page.
4. Select the currency you want to purchase. Select GRT.
5. Select the payment method. Select your preferred payment method.
6. Select the amount of GRT you want to purchase.
7. Review your purchase. Review your purchase and click "Buy GRT".
8. Confirm your purchase. Confirm your purchase and you will have successfully purchased GRT.
9. You can transfer the GRT from your account to your wallet such as [MetaMask](https://metamask.io/).
   - To transfer the GRT to your wallet, click on the "Accounts" button on the top right of the page.
   - Click on the "Send" button next to the GRT account.
   - Enter the amount of GRT you want to send and the wallet address you want to send it to.
   - Click "Continue" and confirm your transaction. -Please note that for larger purchase amounts, Coinbase may require you to wait 7-10 days before transferring the full amount to a wallet.

You can learn more about getting GRT on Coinbase [here](https://help.coinbase.com/en/coinbase/trading-and-funding/buying-selling-or-converting-crypto/how-do-i-buy-digital-currency).

### Binance

This will be a step by step guide for purchasing GRT on Binance.

1. Go to [Binance](https://www.binance.com/en) and create an account.
2. Once you have created an account, you will need to verify your identity through a process known as KYC (or Know Your Customer). This is a standard procedure for all centralized or custodial crypto exchanges.
3. Once you have verified your identity, you can purchase GRT. You can do this by clicking on the "Buy Now" button on the homepage banner.
4. You will be taken to a page where you can select the currency you want to purchase. Select GRT.
5. Select your preferred payment method. You'll be able to pay with different fiat currencies such as Euros, US Dollars, and more.
6. Select the amount of GRT you want to purchase.
7. Review your purchase and click "Buy GRT".
8. Confirm your purchase and you will be able to see your GRT in your Binance Spot Wallet.
9. You can withdraw the GRT from your account to your wallet such as [MetaMask](https://metamask.io/).
   - [To withdraw](https://www.binance.com/en/blog/ecosystem/how-to-transfer-crypto-from-binance-to-trust-wallet-8305050796630181570) the GRT to your wallet, add your wallet's address to the withdrawal whitelist.
   - Click on the "wallet" button, click withdraw, and select GRT.
   - Enter the amount of GRT you want to send and the whitelisted wallet address you want to send it to.
   - Click "Continue" and confirm your transaction.

You can learn more about getting GRT on Binance [here](https://www.binance.com/en/support/faq/how-to-buy-cryptocurrency-on-binance-homepage-400c38f5e0cd4b46a1d0805c296b5582).

### Uniswap

This is how you can purchase GRT on Uniswap.

1. Go to [Uniswap](https://app.uniswap.org/swap?chain=arbitrum) and connect your wallet.
2. Select the token you want to swap from. Select ETH.
3. Select the token you want to swap to. Select GRT.
   - Make sure you're swapping for the correct token. The GRT smart contract address on Arbitrum One is: [0x9623063377AD1B27544C965cCd7342f7EA7e88C7](https://arbiscan.io/token/0x9623063377ad1b27544c965ccd7342f7ea7e88c7)
4. Enter the amount of ETH you want to swap.
5. Click "Swap".
6. Confirm the transaction in your wallet and you wait for the transaction to process.

You can learn more about getting GRT on Uniswap [here](https://support.uniswap.org/hc/en-us/articles/8370549680909-How-to-Swap-Tokens-).

## Getting Ether

This section will show you how to get Ether (ETH) to pay for transaction fees or gas costs. ETH is necessary to execute operations on the Ethereum network such as transferring tokens or interacting with contracts.

### Coinbase

This will be a step by step guide for purchasing ETH on Coinbase.

1.  Go to [Coinbase](https://www.coinbase.com/) and create an account.
2.  Once you have created an account, verify your identity through a process known as KYC (or Know Your Customer). This is a standard procedure for all centralized or custodial crypto exchanges.
3.  Once you have verified your identity, purchase ETH by clicking on the "Buy/Sell" button on the top right of the page.
4.  Select the currency you want to purchase. Select ETH.
5.  Select your preferred payment method.
6.  Enter the amount of ETH you want to purchase.
7.  Review your purchase and click "Buy ETH".
8.  Confirm your purchase and you will have successfully purchased ETH.
9.  You can transfer the ETH from your Coinbase account to your wallet such as [MetaMask](https://metamask.io/).
    - To transfer the ETH to your wallet, click on the "Accounts" button on the top right of the page.
    - Click on the "Send" button next to the ETH account.
    - Enter the amount of ETH you want to send and the wallet address you want to send it to.
    - Ensure that you are sending to your Ethereum wallet address on Arbitrum One.
    - Click "Continue" and confirm your transaction.

You can learn more about getting ETH on Coinbase [here](https://help.coinbase.com/en/coinbase/trading-and-funding/buying-selling-or-converting-crypto/how-do-i-buy-digital-currency).

### Binance

This will be a step by step guide for purchasing ETH on Binance.

1.  Go to [Binance](https://www.binance.com/en) and create an account.
2.  Once you have created an account, verify your identity through a process known as KYC (or Know Your Customer). This is a standard procedure for all centralized or custodial crypto exchanges.
3.  Once you have verified your identity, purchase ETH by clicking on the "Buy Now" button on the homepage banner.
4.  Select the currency you want to purchase. Select ETH.
5.  Select your preferred payment method.
6.  Enter the amount of ETH you want to purchase.
7.  Review your purchase and click "Buy ETH".
8.  Confirm your purchase and you will see your ETH in your Binance Spot Wallet.
9.  You can withdraw the ETH from your account to your wallet such as [MetaMask](https://metamask.io/).
    - To withdraw the ETH to your wallet, add your wallet's address to the withdrawal whitelist.
    - Click on the "wallet" button, click withdraw, and select ETH.
    - Enter the amount of ETH you want to send and the whitelisted wallet address you want to send it to.
    - Ensure that you are sending to your Ethereum wallet address on Arbitrum One.
    - Click "Continue" and confirm your transaction.

You can learn more about getting ETH on Binance [here](https://www.binance.com/en/support/faq/how-to-buy-cryptocurrency-on-binance-homepage-400c38f5e0cd4b46a1d0805c296b5582).

## Billing FAQs

### How many queries will I need?

You don't need to know how many queries you'll need in advance. You will only be charged for what you use and you can withdraw GRT from your account at any time.

We recommend you overestimate the number of queries you will need so that you don’t have to top up your balance frequently. A good estimate for small to medium sized applications is to start with 1M-2M queries per month and monitor usage closely in the first weeks. For larger apps, a good estimate is to use the number of daily visits your site gets multiplied by the number of queries your most active page makes upon opening.

Of course, both new and existing users can reach out to Edge & Node's BD team for a consult to learn more about anticipated usage.

### Can I withdraw GRT from my billing balance?

Yes, you can always withdraw GRT that has not already been used for queries from your billing balance. The billing contract is only designed to bridge GRT from Ethereum mainnet to the Arbitrum network. If you'd like to transfer your GRT from Arbitrum back to Ethereum mainnet, you'll need to use the [Arbitrum Bridge](https://bridge.arbitrum.io/?l2ChainId=42161).

### What happens when my billing balance runs out? Will I get a warning?

You will receive several email notifications before your billing balance runs out.
---
title: About The Graph
---

## What is The Graph?

The Graph is a powerful decentralized protocol that enables seamless querying and indexing of blockchain data. It simplifies the complex process of querying blockchain data, making dapp development faster and easier.

## Understanding the Basics

Projects with complex smart contracts such as [Uniswap](https://uniswap.org/) and NFTs initiatives like [Bored Ape Yacht Club](https://boredapeyachtclub.com/) store data on the Ethereum blockchain, making it very difficult to read anything other than basic data directly from the blockchain.

### Challenges Without The Graph

In the case of the example listed above, Bored Ape Yacht Club, you can perform basic read operations on [the contract](https://etherscan.io/address/0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d#code). You can read the owner of a certain Ape, read the content URI of an Ape based on their ID, or read the total supply.

- This can be done because these read operations are programmed directly into the smart contract itself. However, more advanced, specific, and real-world queries and operations like aggregation, search, relationships, and non-trivial filtering, **are not possible**.

- For instance, if you want to inquire about Apes owned by a specific address and refine your search based on a particular characteristic, you would not be able to obtain that information by directly interacting with the contract itself.

- To get more data, you would have to process every single [`transfer`](https://etherscan.io/address/0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d#code#L1746) event ever emitted, read the metadata from IPFS using the Token ID and IPFS hash, and then aggregate it.

### Why is this a problem?

It would take **hours or even days** for a decentralized application (dapp) running in a browser to get an answer to these simple questions.

Alternatively, you have the option to set up your own server, process the transactions, store them in a database, and create an API endpoint to query the data. However, this option is [resource intensive](/network/benefits/), needs maintenance, presents a single point of failure, and breaks important security properties required for decentralization.

Blockchain properties, such as finality, chain reorganizations, and uncled blocks, add complexity to the process, making it time-consuming and conceptually challenging to retrieve accurate query results from blockchain data.

## The Graph Provides a Solution

The Graph solves this challenge with a decentralized protocol that indexes and enables the efficient and high-performance querying of blockchain data. These APIs (indexed "subgraphs") can then be queried with a standard GraphQL API.

Today, there is a decentralized protocol that is backed by the open source implementation of [Graph Node](https://github.com/graphprotocol/graph-node) that enables this process.

### How The Graph Functions

Indexing blockchain data is very difficult, but The Graph makes it easy. The Graph learns how to index Ethereum data by using subgraphs. Subgraphs are custom APIs built on blockchain data that extract data from a blockchain, processes it, and stores it so that it can be seamlessly queried via GraphQL.

#### Specifics

- The Graph uses subgraph descriptions, which are known as the subgraph manifest inside the subgraph.

- The subgraph description outlines the smart contracts of interest for a subgraph, the events within those contracts to focus on, and how to map event data to the data that The Graph will store in its database.

- When creating a subgraph, you need to write a subgraph manifest.

- After writing the `subgraph manifest`, you can use the Graph CLI to store the definition in IPFS and instruct an Indexer to start indexing data for that subgraph.

The diagram below provides more detailed information about the flow of data after a subgraph manifest has been deployed with Ethereum transactions.

![A graphic explaining how The Graph uses Graph Node to serve queries to data consumers](/img/graph-dataflow.png)

The flow follows these steps:

1.  A dapp adds data to Ethereum through a transaction on a smart contract.
2.  The smart contract emits one or more events while processing the transaction.
3.  Graph Node continually scans Ethereum for new blocks and the data for your subgraph they may contain.
4.  Graph Node finds Ethereum events for your subgraph in these blocks and runs the mapping handlers you provided. The mapping is a WASM module that creates or updates the data entities that Graph Node stores in response to Ethereum events.
5.  The dapp queries the Graph Node for data indexed from the blockchain, using the node's [GraphQL endpoint](https://graphql.org/learn/). The Graph Node in turn translates the GraphQL queries into queries for its underlying data store in order to fetch this data, making use of the store's indexing capabilities. The dapp displays this data in a rich UI for end-users, which they use to issue new transactions on Ethereum. The cycle repeats.

## Next Steps

The following sections provide a more in-depth look at subgraphs, their deployment and data querying.

Before you write your own subgraph, it's recommended to explore [Graph Explorer](https://thegraph.com/explorer) and review some of the already deployed subgraphs. Each subgraph's page includes a GraphQL playground, allowing you to query its data.
---
title: Glossary
---

- **The Graph**: A decentralized protocol for indexing and querying data.

- **Query**: A request for data. In the case of The Graph, a query is a request for data from a subgraph that will be answered by an Indexer.

- **GraphQL**: A query language for APIs and a runtime for fulfilling those queries with your existing data. The Graph uses GraphQL to query subgraphs.

- **Endpoint**: A URL that can be used to query a subgraph. The testing endpoint for Subgraph Studio is `https://api.studio.thegraph.com/query/<ID>/<SUBGRAPH_NAME>/<VERSION>` and the Graph Explorer endpoint is `https://gateway.thegraph.com/api/<API_KEY>/subgraphs/id/<SUBGRAPH_ID>`. The Graph Explorer endpoint is used to query subgraphs on The Graph's decentralized network.

- **Subgraph**: An open API that extracts data from a blockchain, processes it, and stores it so that it can be easily queried via GraphQL. Developers can build, deploy, and publish subgraphs to The Graph Network. Once it is indexed, the subgraph can be queried by anyone.

- **Indexer**: Network participants that run indexing nodes to index data from blockchains and serve GraphQL queries.

- **Indexer Revenue Streams**: Indexers are rewarded in GRT with two components: query fee rebates and indexing rewards.

  1. **Query Fee Rebates**: Payments from subgraph consumers for serving queries on the network.

  2. **Indexing Rewards**: The rewards that Indexers receive for indexing subgraphs. Indexing rewards are generated via new issuance of 3% GRT annually.

- **Indexer's Self Stake**: The amount of GRT that Indexers stake to participate in the decentralized network. The minimum is 100,000 GRT, and there is no upper limit.

- **Upgrade Indexer**: An Indexer designed to act as a fallback for subgraph queries not serviced by other Indexers on the network. The upgrade Indexer is not competitive with other Indexers.

- **Delegator**: Network participants who own GRT and delegate their GRT to Indexers. This allows Indexers to increase their stake in subgraphs on the network. In return, Delegators receive a portion of the Indexing Rewards that Indexers receive for processing subgraphs.

- **Delegation Tax**: A 0.5% fee paid by Delegators when they delegate GRT to Indexers. The GRT used to pay the fee is burned.

- **Curator**: Network participants that identify high-quality subgraphs, and signal GRT on them in exchange for curation shares. When Indexers claim query fees on a subgraph, 10% is distributed to the Curators of that subgraph. There is a positive correlation between the amount of GRT signaled and the number of Indexers indexing a subgraph.

- **Curation Tax**: A 1% fee paid by Curators when they signal GRT on subgraphs. The GRT used to pay the fee is burned.

- **Data Consumer**: Any application or user that queries a subgraph.

- **Subgraph Developer**: A developer who builds and deploys a subgraph to The Graph's decentralized network.

- **Subgraph Manifest**: A YAML file that describes the subgraph's GraphQL schema, data sources, and other metadata. [Here](https://github.com/graphprotocol/example-subgraph/blob/master/subgraph.yaml) is an example.

- **Epoch**: A unit of time within the network. Currently, one epoch is 6,646 blocks or approximately 1 day.

- **Allocation**: An Indexer can allocate their total GRT stake (including Delegators' stake) towards subgraphs that have been published on The Graph's decentralized network. Allocations can have different statuses:

  1. **Active**: An allocation is considered active when it is created on-chain. This is called opening an allocation, and indicates to the network that the Indexer is actively indexing and serving queries for a particular subgraph. Active allocations accrue indexing rewards proportional to the signal on the subgraph, and the amount of GRT allocated.

  2. **Closed**: An Indexer may claim the accrued indexing rewards on a given subgraph by submitting a recent, and valid, Proof of Indexing (POI). This is known as closing an allocation. An allocation must have been open for a minimum of one epoch before it can be closed. The maximum allocation period is 28 epochs. If an Indexer leaves an allocation open beyond 28 epochs, it is known as a stale allocation. When an allocation is in the **Closed** state, a Fisherman can still open a dispute to challenge an Indexer for serving false data.

- **Subgraph Studio**: A powerful dapp for building, deploying, and publishing subgraphs.

- **Fishermen**: A role within The Graph Network held by participants who monitor the accuracy and integrity of data served by Indexers. When a Fisherman identifies a query response or a POI they believe to be incorrect, they can initiate a dispute against the Indexer. If the dispute rules in favor of the Fisherman, the Indexer is slashed by losing 2.5% of their self-stake. Of this amount, 50% is awarded to the Fisherman as a bounty for their vigilance, and the remaining 50% is removed from circulation (burned). This mechanism is designed to encourage Fishermen to help maintain the reliability of the network by ensuring that Indexers are held accountable for the data they provide.

- **Arbitrators**: Arbitrators are network participants appointed through a governance process. The role of the Arbitrator is to decide the outcome of indexing and query disputes. Their goal is to maximize the utility and reliability of The Graph Network.

- **Slashing**: Indexers can have their self-staked GRT slashed for providing an incorrect POI or for serving inaccurate data. The slashing percentage is a protocol parameter currently set to 2.5% of an Indexer's self stake. 50% of the slashed GRT goes to the Fisherman that disputed the inaccurate data or incorrect POI. The other 50% is burned.

- **Indexing Rewards**: The rewards that Indexers receive for indexing subgraphs. Indexing rewards are distributed in GRT.

- **Delegation Rewards**: The rewards that Delegators receive for delegating GRT to Indexers. Delegation rewards are distributed in GRT.

- **GRT**: The Graph's work utility token. GRT provides economic incentives to network participants for contributing to the network.

- **Proof of Indexing (POI)**: When an Indexer closes their allocation and wants to claim their accrued indexing rewards on a given subgraph, they must provide a valid and recent POI. Fishermen may dispute the POI provided by an Indexer. A dispute resolved in the Fisherman's favor will result in slashing of the Indexer.

- **Graph Node**: Graph Node is the component that indexes subgraphs and makes the resulting data available to query via a GraphQL API. As such it is central to the Indexer stack, and correct operation of Graph Node is crucial to running a successful Indexer.

- **Indexer agent**: The Indexer agent is part of the Indexer stack. It facilitates the Indexer's interactions on-chain, including registering on the network, managing subgraph deployments to its Graph Node(s), and managing allocations.

- **The Graph Client**: A library for building GraphQL-based dapps in a decentralized way.

- **Graph Explorer**: A dapp designed for network participants to explore subgraphs and interact with the protocol.

- **Graph CLI**: A command line interface tool for building and deploying to The Graph.

- **Cooldown Period**: The time remaining until an Indexer who changed their delegation parameters can do so again.

- **L2 Transfer Tools**: Smart contracts and UI that enable network participants to transfer network related assets from Ethereum mainnet to Arbitrum One. Network participants can transfer delegated GRT, subgraphs, curation shares, and Indexer's self stake.

- **Updating a subgraph**: The process of releasing a new subgraph version with updates to the subgraph's manifest, schema, or mappings.

- **Migrating**: The process of curation shares moving from an old version of a subgraph to a new version of a subgraph (e.g. when v0.0.1 is updated to v0.0.2).
---
title: Operating Graph Node
---

Graph Node is the component which indexes subgraphs, and makes the resulting data available to query via a GraphQL API. As such it is central to the indexer stack, and correct operation of Graph Node is crucial to running a successful indexer.

This provides a contextual overview of Graph Node, and some of the more advanced options available to indexers. Detailed documentation and instructions can be found in the [Graph Node repository](https://github.com/graphprotocol/graph-node).

## Graph Node

[Graph Node](https://github.com/graphprotocol/graph-node) is the reference implementation for indexing Subgraphs on The Graph Network, connecting to blockchain clients, indexing subgraphs and making indexed data available to query.

Graph Node (and the whole indexer stack) can be run on bare metal, or in a cloud environment. This flexibility of the central indexing component is crucial to the robustness of The Graph Protocol. Similarly, Graph Node can be [built from source](https://github.com/graphprotocol/graph-node), or indexers can use one of the [provided Docker Images](https://hub.docker.com/r/graphprotocol/graph-node).

### PostgreSQL database

The main store for the Graph Node, this is where subgraph data is stored, as well as metadata about subgraphs, and subgraph-agnostic network data such as the block cache, and eth_call cache.

### Network clients

In order to index a network, Graph Node needs access to a network client via an EVM-compatible JSON-RPC API. This RPC may connect to a single client or it could be a more complex setup that load balances across multiple.

While some subgraphs may just require a full node, some may have indexing features which require additional RPC functionality. Specifically subgraphs which make `eth_calls` as part of indexing will require an archive node which supports [EIP-1898](https://eips.ethereum.org/EIPS/eip-1898), and subgraphs with `callHandlers`, or `blockHandlers` with a `call` filter, require `trace_filter` support ([see trace module documentation here](https://openethereum.github.io/JSONRPC-trace-module)).

**Network Firehoses** - a Firehose is a gRPC service providing an ordered, yet fork-aware, stream of blocks, developed by The Graph's core developers to better support performant indexing at scale. This is not currently an Indexer requirement, but Indexers are encouraged to familiarise themselves with the technology, ahead of full network support. Learn more about the Firehose [here](https://firehose.streamingfast.io/).

### IPFS Nodes

Subgraph deployment metadata is stored on the IPFS network. The Graph Node primarily accesses the IPFS node during subgraph deployment to fetch the subgraph manifest and all linked files. Network indexers do not need to host their own IPFS node. An IPFS node for the network is hosted at https://ipfs.network.thegraph.com.

### Prometheus metrics server

To enable monitoring and reporting, Graph Node can optionally log metrics to a Prometheus metrics server.

### Getting started from source

#### Install prerequisites

- **Rust**

- **PostgreSQL**

- **IPFS**

- **Additional Requirements for Ubuntu users** - To run a Graph Node on Ubuntu a few additional packages may be needed.

```sh
sudo apt-get install -y clang libpq-dev libssl-dev pkg-config
```

#### Setup

1. Start a PostgreSQL database server

```sh
initdb -D .postgres
pg_ctl -D .postgres -l logfile start
createdb graph-node
```

2. Clone [Graph Node](https://github.com/graphprotocol/graph-node) repo and build the source by running `cargo build`

3. Now that all the dependencies are setup, start the Graph Node:

```sh
cargo run -p graph-node --release -- \
  --postgres-url postgresql://[USERNAME]:[PASSWORD]@localhost:5432/graph-node \
  --ethereum-rpc [NETWORK_NAME]:[URL] \
  --ipfs https://ipfs.network.thegraph.com
```

### Getting started with Kubernetes

A complete Kubernetes example configuration can be found in the [indexer repository](https://github.com/graphprotocol/indexer/tree/main/k8s).

### Ports

When it is running Graph Node exposes the following ports:

| Port | Purpose | Routes | CLI Argument | Environment Variable |
| --- | --- | --- | --- | --- |
| 8000 | GraphQL HTTP server<br />(for subgraph queries) | /subgraphs/id/...<br />/subgraphs/name/.../... | --http-port | - |
| 8001 | GraphQL WS<br />(for subgraph subscriptions) | /subgraphs/id/...<br />/subgraphs/name/.../... | --ws-port | - |
| 8020 | JSON-RPC<br />(for managing deployments) | / | --admin-port | - |
| 8030 | Subgraph indexing status API | /graphql | --index-node-port | - |
| 8040 | Prometheus metrics | /metrics | --metrics-port | - |

> **Important**: Be careful about exposing ports publicly - **administration ports** should be kept locked down. This includes the the Graph Node JSON-RPC endpoint.

## Advanced Graph Node configuration

At its simplest, Graph Node can be operated with a single instance of Graph Node, a single PostgreSQL database, an IPFS node, and the network clients as required by the subgraphs to be indexed.

This setup can be scaled horizontally, by adding multiple Graph Nodes, and multiple databases to support those Graph Nodes. Advanced users may want to take advantage of some of the horizontal scaling capabilities of Graph Node, as well as some of the more advanced configuration options, via the `config.toml` file and Graph Node's environment variables.

### `config.toml`

A [TOML](https://toml.io/en/) configuration file can be used to set more complex configurations than those exposed in the CLI. The location of the file is passed with the --config command line switch.

> When using a configuration file, it is not possible to use the options --postgres-url, --postgres-secondary-hosts, and --postgres-host-weights.

A minimal `config.toml` file can be provided; the following file is equivalent to using the --postgres-url command line option:

```toml
[store]
[store.primary]
connection="<.. postgres-url argument ..>"
[deployment]
[[deployment.rule]]
indexers = [ "<.. list of all indexing nodes ..>" ]
```

Full documentation of `config.toml` can be found in the [Graph Node docs](https://github.com/graphprotocol/graph-node/blob/master/docs/config.md).

#### Multiple Graph Nodes

Graph Node indexing can scale horizontally, running multiple instances of Graph Node to split indexing and querying across different nodes. This can be done simply by running Graph Nodes configured with a different `node_id` on startup (e.g. in the Docker Compose file), which can then be used in the `config.toml` file to specify [dedicated query nodes](#dedicated-query-nodes), [block ingestors](#dedicated-block-ingestion), and splitting subgraphs across nodes with [deployment rules](#deployment-rules).

> Note that multiple Graph Nodes can all be configured to use the same database, which itself can be horizontally scaled via sharding.

#### Deployment rules

Given multiple Graph Nodes, it is necessary to manage deployment of new subgraphs so that the same subgraph isn't being indexed by two different nodes, which would lead to collisions. This can be done by using deployment rules, which can also specify which `shard` a subgraph's data should be stored in, if database sharding is being used. Deployment rules can match on the subgraph name and the network that the deployment is indexing in order to make a decision.

Example deployment rule configuration:

```toml
[deployment]
[[deployment.rule]]
match = { name = "(vip|important)/.*" }
shard = "vip"
indexers = [ "index_node_vip_0", "index_node_vip_1" ]
[[deployment.rule]]
match = { network = "kovan" }
# No shard, so we use the default shard called 'primary'
indexers = [ "index_node_kovan_0" ]
[[deployment.rule]]
match = { network = [ "xdai", "poa-core" ] }
indexers = [ "index_node_other_0" ]
[[deployment.rule]]
# There's no 'match', so any subgraph matches
shards = [ "sharda", "shardb" ]
indexers = [
    "index_node_community_0",
    "index_node_community_1",
    "index_node_community_2",
    "index_node_community_3",
    "index_node_community_4",
    "index_node_community_5"
  ]
```

Read more about deployment rules [here](https://github.com/graphprotocol/graph-node/blob/master/docs/config.md#controlling-deployment).

#### Dedicated query nodes

Nodes can be configured to explicitly be query nodes by including the following in the configuration file:

```toml
[general]
query = "<regular expression>"
```

Any node whose --node-id matches the regular expression will be set up to only respond to queries.

#### Database scaling via sharding

For most use cases, a single Postgres database is sufficient to support a graph-node instance. When a graph-node instance outgrows a single Postgres database, it is possible to split the storage of graph-node's data across multiple Postgres databases. All databases together form the store of the graph-node instance. Each individual database is called a shard.

Shards can be used to split subgraph deployments across multiple databases, and can also be used to use replicas to spread query load across databases. This includes configuring the number of available database connections each `graph-node` should keep in its connection pool for each database, which becomes increasingly important as more subgraphs are being indexed.

Sharding becomes useful when your existing database can't keep up with the load that Graph Node puts on it, and when it's not possible to increase the database size anymore.

> It is generally better make a single database as big as possible, before starting with shards. One exception is where query traffic is split very unevenly between subgraphs; in those situations it can help dramatically if the high-volume subgraphs are kept in one shard and everything else in another because that setup makes it more likely that the data for the high-volume subgraphs stays in the db-internal cache and doesn't get replaced by data that's not needed as much from low-volume subgraphs.

In terms of configuring connections, start with max_connections in postgresql.conf set to 400 (or maybe even 200) and look at the store_connection_wait_time_ms and store_connection_checkout_count Prometheus metrics. Noticeable wait times (anything above 5ms) is an indication that there are too few connections available; high wait times there will also be caused by the database being very busy (like high CPU load). However if the database seems otherwise stable, high wait times indicate a need to increase the number of connections. In the configuration, how many connections each graph-node instance can use is an upper limit, and Graph Node will not keep connections open if it doesn't need them.

Read more about store configuration [here](https://github.com/graphprotocol/graph-node/blob/master/docs/config.md#configuring-multiple-databases).

#### Dedicated block ingestion

If there are multiple nodes configured, it will be necessary to specify one node which is responsible for ingestion of new blocks, so that all configured index nodes aren't polling the chain head. This is done as part of the `chains` namespace, specifying the `node_id` to be used for block ingestion:

```toml
[chains]
ingestor = "block_ingestor_node"
```

#### Supporting multiple networks

The Graph Protocol is increasing the number of networks supported for indexing rewards, and there exist many subgraphs indexing unsupported networks which an indexer would like to process. The `config.toml` file allows for expressive and flexible configuration of:

- Multiple networks
- Multiple providers per network (this can allow splitting of load across providers, and can also allow for configuration of full nodes as well as archive nodes, with Graph Node preferring cheaper providers if a given workload allows).
- Additional provider details, such as features, authentication and the type of provider (for experimental Firehose support)

The `[chains]` section controls the ethereum providers that graph-node connects to, and where blocks and other metadata for each chain are stored. The following example configures two chains, mainnet and kovan, where blocks for mainnet are stored in the vip shard and blocks for kovan are stored in the primary shard. The mainnet chain can use two different providers, whereas kovan only has one provider.

```toml
[chains]
ingestor = "block_ingestor_node"
[chains.mainnet]
shard = "vip"
provider = [
  { label = "mainnet1", url = "http://..", features = [], headers = { Authorization = "Bearer foo" } },
  { label = "mainnet2", url = "http://..", features = [ "archive", "traces" ] }
]
[chains.kovan]
shard = "primary"
provider = [ { label = "kovan", url = "http://..", features = [] } ]
```

Read more about provider configuration [here](https://github.com/graphprotocol/graph-node/blob/master/docs/config.md#configuring-ethereum-providers).

### Environment variables

Graph Node supports a range of environment variables which can enable features, or change Graph Node behaviour. These are documented [here](https://github.com/graphprotocol/graph-node/blob/master/docs/environment-variables.md).

### Continuous deployment

Users who are operating a scaled indexing setup with advanced configuration may benefit from managing their Graph Nodes with Kubernetes.

- The indexer repository has an [example Kubernetes reference](https://github.com/graphprotocol/indexer/tree/main/k8s)
- [Launchpad](https://docs.graphops.xyz/launchpad/intro) is a toolkit for running a Graph Protocol Indexer on Kubernetes maintained by GraphOps. It provides a set of Helm charts and a CLI to manage a Graph Node deployment.

### Managing Graph Node

Given a running Graph Node (or Graph Nodes!), the challenge is then to manage deployed subgraphs across those nodes. Graph Node surfaces a range of tools to help with managing subgraphs.

#### Logging

Graph Node's logs can provide useful information for debugging and optimisation of Graph Node and specific subgraphs. Graph Node supports different log levels via the `GRAPH_LOG` environment variable, with the following levels: error, warn, info, debug or trace.

In addition setting `GRAPH_LOG_QUERY_TIMING` to `gql` provides more details about how GraphQL queries are running (though this will generate a large volume of logs).

#### Monitoring & alerting

Graph Node provides the metrics via Prometheus endpoint on 8040 port by default. Grafana can then be used to visualise these metrics.

The indexer repository provides an [example Grafana configuration](https://github.com/graphprotocol/indexer/blob/main/k8s/base/grafana.yaml).

#### Graphman

`graphman` is a maintenance tool for Graph Node, helping with diagnosis and resolution of different day-to-day and exceptional tasks.

The graphman command is included in the official containers, and you can docker exec into your graph-node container to run it. It requires a `config.toml` file.

Full documentation of `graphman` commands is available in the Graph Node repository. See [/docs/graphman.md] (https://github.com/graphprotocol/graph-node/blob/master/docs/graphman.md) in the Graph Node `/docs`

### Working with subgraphs

#### Indexing status API

Available on port 8030/graphql by default, the indexing status API exposes a range of methods for checking indexing status for different subgraphs, checking proofs of indexing, inspecting subgraph features and more.

The full schema is available [here](https://github.com/graphprotocol/graph-node/blob/master/server/index-node/src/schema.graphql).

#### Indexing performance

There are three separate parts of the indexing process:

- Fetching events of interest from the provider
- Processing events in order with the appropriate handlers (this can involve calling the chain for state, and fetching data from the store)
- Writing the resulting data to the store

These stages are pipelined (i.e. they can be executed in parallel), but they are dependent on one another. Where subgraphs are slow to index, the underlying cause will depend on the specific subgraph.

Common causes of indexing slowness:

- Time taken to find relevant events from the chain (call handlers in particular can be slow, given the reliance on `trace_filter`)
- Making large numbers of `eth_calls` as part of handlers
- A large amount of store interaction during execution
- A large amount of data to save to the store
- A large number of events to process
- Slow database connection time, for crowded nodes
- The provider itself falling behind the chain head
- Slowness in fetching new receipts at the chain head from the provider

Subgraph indexing metrics can help diagnose the root cause of indexing slowness. In some cases, the problem lies with the subgraph itself, but in others, improved network providers, reduced database contention and other configuration improvements can markedly improve indexing performance.

#### Failed subgraphs

During indexing subgraphs might fail, if they encounter data that is unexpected, some component not working as expected, or if there is some bug in the event handlers or configuration. There are two general types of failure:

- Deterministic failures: these are failures which will not be resolved with retries
- Non-deterministic failures: these might be down to issues with the provider, or some unexpected Graph Node error. When a non-deterministic failure occurs, Graph Node will retry the failing handlers, backing off over time.

In some cases a failure might be resolvable by the indexer (for example if the error is a result of not having the right kind of provider, adding the required provider will allow indexing to continue). However in others, a change in the subgraph code is required.

> Deterministic failures are considered "final", with a Proof of Indexing generated for the failing block, while non-determinstic failures are not, as the subgraph may manage to "unfail" and continue indexing. In some cases, the non-deterministic label is incorrect, and the subgraph will never overcome the error; such failures should be reported as issues on the Graph Node repository.

#### Block and call cache

Graph Node caches certain data in the store in order to save refetching from the provider. Blocks are cached, as are the results of `eth_calls` (the latter being cached as of a specific block). This caching can dramatically increase indexing speed during "resyncing" of a slightly altered subgraph.

However, in some instances, if an Ethereum node has provided incorrect data for some period, that can make its way into the cache, leading to incorrect data or failed subgraphs. In this case indexers can use `graphman` to clear the poisoned cache, and then rewind the affected subgraphs, which will then fetch fresh data from the (hopefully) healthy provider.

If a block cache inconsistency is suspected, such as a tx receipt missing event:

1. `graphman chain list` to find the chain name.
2. `graphman chain check-blocks <CHAIN> by-number <NUMBER>` will check if the cached block matches the provider, and deletes the block from the cache if it doesn’t.
   1. If there is a difference, it may be safer to truncate the whole cache with `graphman chain truncate <CHAIN>`.
   2. If the block matches the provider, then the issue can be debugged directly against the provider.

#### Querying issues and errors

Once a subgraph has been indexed, indexers can expect to serve queries via the subgraph's dedicated query endpoint. If the indexer is hoping to serve significant query volume, a dedicated query node is recommended, and in case of very high query volumes, indexers may want to configure replica shards so that queries don't impact the indexing process.

However, even with a dedicated query node and replicas, certain queries can take a long time to execute, and in some cases increase memory usage and negatively impact the query time for other users.

There is not one "silver bullet", but a range of tools for preventing, diagnosing and dealing with slow queries.

##### Query caching

Graph Node caches GraphQL queries by default, which can significantly reduce database load. This can be further configured with the `GRAPH_QUERY_CACHE_BLOCKS` and `GRAPH_QUERY_CACHE_MAX_MEM` settings - read more [here](https://github.com/graphprotocol/graph-node/blob/master/docs/environment-variables.md#graphql-caching).

##### Analysing queries

Problematic queries most often surface in one of two ways. In some cases, users themselves report that a given query is slow. In that case the challenge is to diagnose the reason for the slowness - whether it is a general issue, or specific to that subgraph or query. And then of course to resolve it, if possible.

In other cases, the trigger might be high memory usage on a query node, in which case the challenge is first to identify the query causing the issue.

Indexers can use [qlog](https://github.com/graphprotocol/qlog/) to process and summarize Graph Node's query logs. `GRAPH_LOG_QUERY_TIMING` can also be enabled to help identify and debug slow queries.

Given a slow query, indexers have a few options. Of course they can alter their cost model, to significantly increase the cost of sending the problematic query. This may result in a reduction in the frequency of that query. However this often doesn't resolve the root cause of the issue.

##### Account-like optimisation

Database tables that store entities seem to generally come in two varieties: 'transaction-like', where entities, once created, are never updated, i.e., they store something akin to a list of financial transactions, and 'account-like' where entities are updated very often, i.e., they store something like financial accounts that get modified every time a transaction is recorded. Account-like tables are characterized by the fact that they contain a large number of entity versions, but relatively few distinct entities. Often, in such tables the number of distinct entities is 1% of the total number of rows (entity versions)

For account-like tables, `graph-node` can generate queries that take advantage of details of how Postgres ends up storing data with such a high rate of change, namely that all of the versions for recent blocks are in a small subsection of the overall storage for such a table.

The command `graphman stats show <sgdNNNN`> shows, for each entity type/table in a deployment, how many distinct entities, and how many entity versions each table contains. That data is based on Postgres-internal estimates, and is therefore necessarily imprecise, and can be off by an order of magnitude. A `-1` in the `entities` column means that Postgres believes that all rows contain a distinct entity.

In general, tables where the number of distinct entities are less than 1% of the total number of rows/entity versions are good candidates for the account-like optimization. When the output of `graphman stats show` indicates that a table might benefit from this optimization, running `graphman stats show <sgdNNN> <table>` will perform a full count of the table - that can be slow, but gives a precise measure of the ratio of distinct entities to overall entity versions.

Once a table has been determined to be account-like, running `graphman stats account-like <sgdNNN>.<table>` will turn on the account-like optimization for queries against that table. The optimization can be turned off again with `graphman stats account-like --clear <sgdNNN>.<table>` It takes up to 5 minutes for query nodes to notice that the optimization has been turned on or off. After turning the optimization on, it is necessary to verify that the change does not in fact make queries slower for that table. If you have configured Grafana to monitor Postgres, slow queries would show up in `pg_stat_activity`in large numbers, taking several seconds. In that case, the optimization needs to be turned off again.

For Uniswap-like subgraphs, the `pair` and `token` tables are prime candidates for this optimization, and can have a dramatic effect on database load.

#### Removing subgraphs

> This is new functionality, which will be available in Graph Node 0.29.x

At some point an indexer might want to remove a given subgraph. This can be easily done via `graphman drop`, which deletes a deployment and all it's indexed data. The deployment can be specified as either a subgraph name, an IPFS hash `Qm..`, or the database namespace `sgdNNN`. Further documentation is available [here](https://github.com/graphprotocol/graph-node/blob/master/docs/graphman.md#-drop).
---
title: Chain Integration Process Overview
---

A transparent and governance-based integration process was designed for blockchain teams seeking [integration with The Graph protocol](https://forum.thegraph.com/t/gip-0057-chain-integration-process/4468). It is a 3-phase process, as summarised below.

## Stage 1. Technical Integration

- Please visit [New Chain Integration](/new-chain-integration) for information on `graph-node` support for new chains.
- Teams initiate the protocol integration process by creating a Forum thread [here](https://forum.thegraph.com/c/governance-gips/new-chain-support/71) (New Data Sources sub-category under Governance & GIPs). Using the default Forum template is mandatory.

## Stage 2. Integration Validation

- Teams collaborate with core developers, Graph Foundation and operators of GUIs and network gateways, such as [Subgraph Studio](https://thegraph.com/studio/), to ensure a smooth integration process. This involves providing the necessary backend infrastructure, such as the integrating chain's JSON-RPC, Firehose or Substreams endpoints. Teams wanting to avoid self-hosting such infrastructure can leverage The Graph's community of node operators (Indexers) to do so, which the Foundation can help with.
- Graph Indexers test the integration on The Graph's testnet.
- Core developers and Indexers monitor stability, performance, and data determinism.

## Stage 3. Mainnet Integration

- Teams propose mainnet integration by submitting a Graph Improvement Proposal (GIP) and initiating a pull request (PR) on the [feature support matrix](https://github.com/graphprotocol/indexer/blob/main/docs/feature-support-matrix.md) (more details on the link).
- The Graph Council reviews the request and approves mainnet support, providing a successful Stage 2 and positive community feedback.

---

If the process looks daunting, don't worry! The Graph Foundation is committed to supporting integrators by fostering collaboration, offering essential information, and guiding them through various stages, including navigating governance processes such as Graph Improvement Proposals (GIPs) and pull requests. If you have questions, please reach out to [info@thegraph.foundation](mailto:info@thegraph.foundation) or through Discord (either Pedro, The Graph Foundation member, IndexerDAO, or other core developers).

Ready to shape the future of The Graph Network? [Start your proposal](https://github.com/graphprotocol/graph-improvement-proposals/blob/main/gips/0057-chain-integration-process.md) now and be a part of the web3 revolution!

---

## Frequently Asked Questions

### 1. How does this relate to the [World of Data Services GIP](https://forum.thegraph.com/t/gip-0042-a-world-of-data-services/3761)?

This process is related to the Subgraph Data Service, applicable only to new Subgraph `Data Sources`.

### 2. What happens if Firehose & Substreams support comes after the network is supported on mainnet?

This would only impact protocol support for indexing rewards on Substreams-powered subgraphs. The new Firehose implementation would need testing on testnet, following the methodology outlined for Stage 2 in this GIP. Similarly, assuming the implementation is performant and reliable, a PR on the [Feature Support Matrix](https://github.com/graphprotocol/indexer/blob/main/docs/feature-support-matrix.md) would be required (`Substreams data sources` Subgraph Feature), as well as a new GIP for protocol support for indexing rewards. Anyone can create the PR and GIP; the Foundation would help with Council approval.

### 3. How much time will the process of reaching full protocol support take?

The time to mainnet is expected to be several weeks, varying based on the time of integration development, whether additional research is required, testing and bug fixes, and, as always, the timing of the governance process that requires community feedback.

Protocol support for indexing rewards depends on the stakeholders' bandwidth to proceed with testing, feedback gathering, and handling contributions to the core codebase, if applicable. This is directly tied to the integration's maturity and how responsive the integration team is (who may or may not be the team behind the RPC/Firehose implementation). The Foundation is here to help support throughout the whole process.

### 4. How will priorities be handled?

Similar to #3, it will depend on overall readiness and involved stakeholders' bandwidth. For example, a new chain with a brand new Firehose implementation may take longer than integrations that have already been battle-tested or are farther along in the governance process.
---
title: Managing your API keys
---

Regardless of whether you’re a dapp developer or a subgraph developer, you’ll need to manage your API keys. This is important for you to be able to query subgraphs because API keys make sure the connections between application services are valid and authorized. This includes authenticating the end user and the device using the application.

The "API keys" table lists out existing API keys, which will give you the ability to manage or delete them. For each key, you can see its status, the cost for the current period, the spending limit for the current period, as well as total query numbers. You can click the "three dots" menu to edit a given API key:

- Rename API key
- Regenerate API key
- Delete API key
- Manage spending limit: this is an optional monthly spending limit for a given API key, in USD. This limit is per billing period (calendar month).

You can click on an individual API key to view the Details page:

1. The **Overview** section will allow you to:
   - Edit your key name
   - Regenerate API keys
   - View the current usage of the API key with stats:
     - Number of queries
     - Amount of GRT spent
2. Under **Security**, you’ll be able to opt into security settings depending on the level of control you’d like to have over your API keys. In this section, you can:
   - View and manage the domain names authorized to use your API key
   - Assign subgraphs that can be queried with your API key
---
title: Querying The Graph
---

When a subgraph is published to The Graph Network, you can visit its subgraph details page on [Graph Explorer](https://thegraph.com/explorer) and use the "Playground" tab to explore the deployed GraphQL API for the subgraph, issuing queries and viewing the schema.

> Please see the [Query API](/querying/graphql-api) for a complete reference on how to query the subgraph's entities. You can learn about GraphQL querying best practices [here](/querying/querying-best-practices)

> Note: If you encounter 405 errors with a GET request to the Graph Explorer URL, please switch to a POST request instead.

Each subgraph published to The Graph Network has a unique query URL in Graph Explorer for making direct queries that you can find by navigating to the subgraph details page and clicking on the "Query" button on the top right corner.

![Query Subgraph Pane](/img/query-subgraph-pane.png)

Learn more about querying from an application [here](/querying/querying-from-an-application).

As you can notice, this query URL must use a unique API key. You can create and manage your API keys in [Subgraph Studio](https://thegraph.com/studio), in the "API Keys" section. Learn more about how to use Subgraph Studio [here](/deploying/subgraph-studio).

Subgraph Studio users start on a Free Plan, which allows them to make 100,000 queries per month. Additional queries are available on the Growth Plan, which offers usage based pricing for additional queries, payable by credit card, or GRT on Arbitrum. You can learn more about billing [here](/billing).
---
title: Query The Graph with Python and Subgrounds
---

Subgrounds is an intuitive Python library for querying subgraphs, built by [Playgrounds](https://playgrounds.network/). It allows you to directly connect subgraph data to a Python data environment, letting you use libraries like [pandas](https://pandas.pydata.org/) to perform data analysis!

Subgrounds offers a simple Pythonic API for building GraphQL queries, automates tedious workflows such as pagination, and empowers advanced users through controlled schema transformations.

## Getting Started

Subgrounds requires Python 3.10 or higher and is available on [pypi](https://pypi.org/project/subgrounds/).

```bash
pip install --upgrade subgrounds
# or
python -m pip install --upgrade subgrounds
```

Once installed, you can test out subgrounds with the following query. The following example grabs a subgraph for the Aave v2 protocol and queries the top 5 markets ordered by TVL (Total Value Locked), selects their name and their TVL (in USD) and returns the data as a pandas [DataFrame](https://pandas.pydata.org/pandas-docs/dev/reference/api/pandas.DataFrame.html#pandas.DataFrame).

```python
from subgrounds import Subgrounds

sg = Subgrounds()

# Load the subgraph
aave_v2 = sg.load_subgraph(
    "https://api.thegraph.com/subgraphs/name/messari/aave-v2-ethereum")

# Construct the query
latest_markets = aave_v2.Query.markets(
    orderBy=aave_v2.Market.totalValueLockedUSD,
    orderDirection='desc',
    first=5,
)
# Return query to a dataframe
sg.query_df([
    latest_markets.name,
    latest_markets.totalValueLockedUSD,
])
```

## Documentation

Subgrounds is built and maintained by the [Playgrounds](https://playgrounds.network/) team and can be accessed on the [Playgrounds docs](https://docs.playgrounds.network/subgrounds).

Since subgrounds has a large feature set to explore, here are some helpful starting places:

- [Getting Started with Querying](https://docs.playgrounds.network/subgrounds/getting_started/basics/)
  - A good first step for how to build queries with subgrounds.
- [Building Synthetic Fields](https://docs.playgrounds.network/subgrounds/getting_started/synthetic_fields/)
  - A gentle introduction to defining synthetic fields that transform data defined from the schema.
- [Concurrent Queries](https://docs.playgrounds.network/subgrounds/getting_started/async/)
  - Learn how to level up your queries by parallelizing them.
- [Exporting Data to CSVs](https://docs.playgrounds.network/subgrounds/faq/exporting/)
  - A quick article on how to seemlessly save your data as CSVs for further analysis.
---
title: GraphQL API
---

Learn about the GraphQL Query API used in The Graph.

## What is GraphQL?

[GraphQL](https://graphql.org/learn/) is a query language for APIs and a runtime for executing those queries with your existing data. The Graph uses GraphQL to query subgraphs.

To understand the larger role that GraphQL plays, review [developing](/network/developing/) and [creating a subgraph](/developing/creating-a-subgraph/).

## Queries with GraphQL

In your subgraph schema you define types called `Entities`. For each `Entity` type, `entity` and `entities` fields will be generated on the top-level `Query` type.

> Note: `query` does not need to be included at the top of the `graphql` query when using The Graph.

### Examples

Query for a single `Token` entity defined in your schema:

```graphql
{
  token(id: "1") {
    id
    owner
  }
}
```

> Note: When querying for a single entity, the `id` field is required, and it must be writen as a string.

Query all `Token` entities:

```graphql
{
  tokens {
    id
    owner
  }
}
```

### Sorting

When querying a collection, you may:

- Use the `orderBy` parameter to sort by a specific attribute.
- Use the `orderDirection` to specify the sort direction, `asc` for ascending or `desc` for descending.

#### Example

```graphql
{
  tokens(orderBy: price, orderDirection: asc) {
    id
    owner
  }
}
```

#### Example for nested entity sorting

As of Graph Node [`v0.30.0`](https://github.com/graphprotocol/graph-node/releases/tag/v0.30.0) entities can be sorted on the basis of nested entities.

The following example shows tokens sorted by the name of their owner:

```graphql
{
  tokens(orderBy: owner__name, orderDirection: asc) {
    id
    owner {
      name
    }
  }
}
```

> Currently, you can sort by one-level deep `String` or `ID` types on `@entity` and `@derivedFrom` fields. Unfortunately, [sorting by interfaces on one level-deep entities](https://github.com/graphprotocol/graph-node/pull/4058), sorting by fields which are arrays and nested entities is not yet supported.

### Pagination

When querying a collection, it's best to:

- Use the `first` parameter to paginate from the beginning of the collection.
  - The default sort order is by `ID` in ascending alphanumeric order, **not** by creation time.
- Use the `skip` parameter to skip entities and paginate. For instance, `first:100` shows the first 100 entities and `first:100, skip:100` shows the next 100 entities.
- Avoid using `skip` values in queries because they generally perform poorly. To retrieve a large number of items, it's best to page through entities based on an attribute as shown in the previous example above.

#### Example using `first`

Query the first 10 tokens:

```graphql
{
  tokens(first: 10) {
    id
    owner
  }
}
```

To query for groups of entities in the middle of a collection, the `skip` parameter may be used in conjunction with the `first` parameter to skip a specified number of entities starting at the beginning of the collection.

#### Example using `first` and `skip`

Query 10 `Token` entities, offset by 10 places from the beginning of the collection:

```graphql
{
  tokens(first: 10, skip: 10) {
    id
    owner
  }
}
```

#### Example using `first` and `id_ge`

If a client needs to retrieve a large number of entities, it's more performant to base queries on an attribute and filter by that attribute. For example, a client could retrieve a large number of tokens using this query:

```graphql
query manyTokens($lastID: String) {
  tokens(first: 1000, where: { id_gt: $lastID }) {
    id
    owner
  }
}
```

The first time, it would send the query with `lastID = ""`, and for subsequent requests it would set `lastID` to the `id` attribute of the last entity in the previous request. This approach will perform significantly better than using increasing `skip` values.

### Filtering

- You can use the `where` parameter in your queries to filter for different properties.
- You can filter on multiple values within the `where` parameter.

#### Example using `where`

Query challenges with `failed` outcome:

```graphql
{
  challenges(where: { outcome: "failed" }) {
    challenger
    outcome
    application {
      id
    }
  }
}
```

You can use suffixes like `_gt`, `_lte` for value comparison:

#### Example for range filtering

```graphql
{
  applications(where: { deposit_gt: "10000000000" }) {
    id
    whitelisted
    deposit
  }
}
```

#### Example for block filtering

You can also filter entities that were updated in or after a specified block with `_change_block(number_gte: Int)`.

This can be useful if you are looking to fetch only entities which have changed, for example since the last time you polled. Or alternatively it can be useful to investigate or debug how entities are changing in your subgraph (if combined with a block filter, you can isolate only entities that changed in a specific block).

```graphql
{
  applications(where: { _change_block: { number_gte: 100 } }) {
    id
    whitelisted
    deposit
  }
}
```

#### Example for nested entity filtering

Filtering on the basis of nested entities is possible in the fields with the `_` suffix.

This can be useful if you are looking to fetch only entities whose child-level entities meet the provided conditions.

```graphql
{
  challenges(where: { application_: { id: 1 } }) {
    challenger
    outcome
    application {
      id
    }
  }
}
```

#### Logical operators

As of Graph Node [`v0.30.0`](https://github.com/graphprotocol/graph-node/releases/tag/v0.30.0) you can group multiple parameters in the same `where` argument using the `and` or the `or` operators to filter results based on more than one criteria.

##### `AND` Operator

The following example filters for challenges with `outcome` `succeeded` and `number` greater than or equal to `100`.

```graphql
{
  challenges(where: { and: [{ number_gte: 100 }, { outcome: "succeeded" }] }) {
    challenger
    outcome
    application {
      id
    }
  }
}
```

> **Syntactic sugar:** You can simplify the above query by removing the `and` operator by passing a sub-expression separated by commas.
>
> ```graphql
> {
>   challenges(where: { number_gte: 100, outcome: "succeeded" }) {
>     challenger
>     outcome
>     application {
>       id
>     }
>   }
> }
> ```

##### `OR` Operator

The following example filters for challenges with `outcome` `succeeded` or `number` greater than or equal to `100`.

```graphql
{
  challenges(where: { or: [{ number_gte: 100 }, { outcome: "succeeded" }] }) {
    challenger
    outcome
    application {
      id
    }
  }
}
```

> **Note**: When constructing queries, it is important to consider the performance impact of using the `or` operator. While `or` can be a useful tool for broadening search results, it can also have significant costs. One of the main issues with `or` is that it can cause queries to slow down. This is because `or` requires the database to scan through multiple indexes, which can be a time-consuming process. To avoid these issues, it is recommended that developers use and operators instead of or whenever possible. This allows for more precise filtering and can lead to faster, more accurate queries.

#### All Filters

Full list of parameter suffixes:

```
_
_not
_gt
_lt
_gte
_lte
_in
_not_in
_contains
_contains_nocase
_not_contains
_not_contains_nocase
_starts_with
_starts_with_nocase
_ends_with
_ends_with_nocase
_not_starts_with
_not_starts_with_nocase
_not_ends_with
_not_ends_with_nocase
```

> Please note that some suffixes are only supported for specific types. For example, `Boolean` only supports `_not`, `_in`, and `_not_in`, but `_` is available only for object and interface types.

In addition, the following global filters are available as part of `where` argument:

```gr
_change_block(number_gte: Int)
```

### Time-travel queries

You can query the state of your entities not just for the latest block, which is the default, but also for an arbitrary block in the past. The block at which a query should happen can be specified either by its block number or its block hash by including a `block` argument in the toplevel fields of queries.

The result of such a query will not change over time, i.e., querying at a certain past block will return the same result no matter when it is executed, with the exception that if you query at a block very close to the head of the chain, the result might change if that block turns out to **not** be on the main chain and the chain gets reorganized. Once a block can be considered final, the result of the query will not change.

> Note: The current implementation is still subject to certain limitations that might violate these guarantees. The implementation can not always tell that a given block hash is not on the main chain at all, or if a query result by a block hash for a block that is not yet considered final could be influenced by a block reorganization running concurrently with the query. They do not affect the results of queries by block hash when the block is final and known to be on the main chain. [This issue](https://github.com/graphprotocol/graph-node/issues/1405) explains what these limitations are in detail.

#### Example

```graphql
{
  challenges(block: { number: 8000000 }) {
    challenger
    outcome
    application {
      id
    }
  }
}
```

This query will return `Challenge` entities, and their associated `Application` entities, as they existed directly after processing block number 8,000,000.

#### Example

```graphql
{
  challenges(block: { hash: "0x5a0b54d5dc17e0aadc383d2db43b0a0d3e029c4c" }) {
    challenger
    outcome
    application {
      id
    }
  }
}
```

This query will return `Challenge` entities, and their associated `Application` entities, as they existed directly after processing the block with the given hash.

### Fulltext Search Queries

Fulltext search query fields provide an expressive text search API that can be added to the subgraph schema and customized. Refer to [Defining Fulltext Search Fields](/developing/creating-a-subgraph#defining-fulltext-search-fields) to add fulltext search to your subgraph.

Fulltext search queries have one required field, `text`, for supplying search terms. Several special fulltext operators are available to be used in this `text` search field.

Fulltext search operators:

| Symbol | Operator | Description |
| --- | --- | --- |
| `&` | `And` | For combining multiple search terms into a filter for entities that include all of the provided terms |
| &#x7c; | `Or` | Queries with multiple search terms separated by the or operator will return all entities with a match from any of the provided terms |
| `<->` | `Follow by` | Specify the distance between two words. |
| `:*` | `Prefix` | Use the prefix search term to find words whose prefix match (2 characters required.) |

#### Examples

Using the `or` operator, this query will filter to blog entities with variations of either "anarchism" or "crumpet" in their fulltext fields.

```graphql
{
  blogSearch(text: "anarchism | crumpets") {
    id
    title
    body
    author
  }
}
```

The `follow by` operator specifies a words a specific distance apart in the fulltext documents. The following query will return all blogs with variations of "decentralize" followed by "philosophy"

```graphql
{
  blogSearch(text: "decentralized <-> philosophy") {
    id
    title
    body
    author
  }
}
```

Combine fulltext operators to make more complex filters. With a pretext search operator combined with a follow by this example query will match all blog entities with words that start with "lou" followed by "music".

```graphql
{
  blogSearch(text: "lou:* <-> music") {
    id
    title
    body
    author
  }
}
```

### Validation

Graph Node implements [specification-based](https://spec.graphql.org/October2021/#sec-Validation) validation of the GraphQL queries it receives using [graphql-tools-rs](https://github.com/dotansimha/graphql-tools-rs#validation-rules), which is based on the [graphql-js reference implementation](https://github.com/graphql/graphql-js/tree/main/src/validation). Queries which fail a validation rule do so with a standard error - visit the [GraphQL spec](https://spec.graphql.org/October2021/#sec-Validation) to learn more.

## Schema

The schema of your dataSources, i.e. the entity types, values, and relationships that are available to query, are defined through the [GraphQL Interface Definition Langauge (IDL)](https://facebook.github.io/graphql/draft/#sec-Type-System).

GraphQL schemas generally define root types for `queries`, `subscriptions` and `mutations`. The Graph only supports `queries`. The root `Query` type for your subgraph is automatically generated from the GraphQL schema that's included in your [subgraph manifest](/developing/creating-a-subgraph/#components-of-a-subgraph).

> Note: Our API does not expose mutations because developers are expected to issue transactions directly against the underlying blockchain from their applications.

### Entities

All GraphQL types with `@entity` directives in your schema will be treated as entities and must have an `ID` field.

> **Note:** Currently, all types in your schema must have an `@entity` directive. In the future, we will treat types without an `@entity` directive as value objects, but this is not yet supported.

### Subgraph Metadata

All subgraphs have an auto-generated `_Meta_` object, which provides access to subgraph metadata. This can be queried as follows:

```graphQL
{
  _meta(block: { number: 123987 }) {
    block {
      number
      hash
      timestamp
    }
    deployment
    hasIndexingErrors
  }
}
```

If a block is provided, the metadata is as of that block, if not the latest indexed block is used. If provided, the block must be after the subgraph's start block, and less than or equal to the most recently indexed block.

`deployment` is a unique ID, corresponding to the IPFS CID of the `subgraph.yaml` file.

`block` provides information about the latest block (taking into account any block constraints passed to `_meta`):

- hash: the hash of the block
- number: the block number
- timestamp: the timestamp of the block, if available (this is currently only available for subgraphs indexing EVM networks)

`hasIndexingErrors` is a boolean identifying whether the subgraph encountered indexing errors at some past block
---
title: Querying Best Practices
---

The Graph provides a decentralized way to query data from blockchains via GraphQL APIs, making it easier to query data with the GraphQL language.

Learn the essential GraphQL language rules and GraphQL querying best practices.

---

## Querying a GraphQL API

### The anatomy of a GraphQL query

Unlike REST API, a GraphQL API is built upon a Schema that defines which queries can be performed.

For example, a query to get a token using the `token` query will look as follows:

```graphql
query GetToken($id: ID!) {
  token(id: $id) {
    id
    owner
  }
}
```

which will return the following predictable JSON response (_when passing the proper `$id` variable value_):

```json
{
  "token": {
    "id": "...",
    "owner": "..."
  }
}
```

GraphQL queries use the GraphQL language, which is defined upon [a specification](https://spec.graphql.org/).

The above `GetToken` query is composed of multiple language parts (replaced below with `[...]` placeholders):

```graphql
query [operationName]([variableName]: [variableType]) {
  [queryName]([argumentName]: [variableName]) {
    # "{ ... }" express a Selection-Set, we are querying fields from `queryName`.
    [field]
    [field]
  }
}
```

While the list of syntactic do's and don'ts is long, here are the essential rules to keep in mind when it comes to writing GraphQL queries:

- Each `queryName` must only be used once per operation.
- Each `field` must be used only once in a selection (we cannot query `id` twice under `token`)
- Some `field`s or queries (like `tokens`) return complex types that require a selection of sub-field. Not providing a selection when expected (or providing one when not expected - for example, on `id`) will raise an error. To know a field type, please refer to [Graph Explorer](/network/explorer).
- Any variable assigned to an argument must match its type.
- In a given list of variables, each of them must be unique.
- All defined variables must be used.

Failing to follow the above rules will end with an error from the Graph API.

For a complete list of rules with code examples, please look at our [GraphQL Validations guide](/release-notes/graphql-validations-migration-guide/).

### Sending a query to a GraphQL API

GraphQL is a language and set of conventions that transport over HTTP.

It means that you can query a GraphQL API using standard `fetch` (natively or via `@whatwg-node/fetch` or `isomorphic-fetch`).

However, as stated in ["Querying from an Application"](/querying/querying-from-an-application), it's recommend to use `graph-client` which supports unique features such as:

- Cross-chain Subgraph Handling: Querying from multiple subgraphs in a single query
- [Automatic Block Tracking](https://github.com/graphprotocol/graph-client/blob/main/packages/block-tracking/README.md)
- [Automatic Pagination](https://github.com/graphprotocol/graph-client/blob/main/packages/auto-pagination/README.md)
- Fully typed result

Here's how to query The Graph with `graph-client`:

```tsx
import { execute } from '../.graphclient'

const query = `
query GetToken($id: ID!) {
  token(id: $id) {
    id
    owner
  }
}
`
const variables = { id: '1' }

async function main() {
  const result = await execute(query, variables)
  // `result` is fully typed!
  console.log(result)
}

main()
```

More GraphQL client alternatives are covered in ["Querying from an Application"](/querying/querying-from-an-application).

---

## Best Practices

### Always write static queries

A common (bad) practice is to dynamically build query strings as follows:

```tsx
const id = params.id
const fields = ['id', 'owner']
const query = `
query GetToken {
  token(id: ${id}) {
    ${fields.join('\n')}
  }
}
`

// Execute query...
```

While the above snippet produces a valid GraphQL query, **it has many drawbacks**:

- it makes it **harder to understand** the query as a whole
- developers are **responsible for safely sanitizing the string interpolation**
- not sending the values of the variables as part of the request parameters **prevent possible caching on server-side**
- it **prevents tools from statically analyzing the query** (ex: Linter, or type generations tools)

For this reason, it is recommended to always write queries as static strings:

```tsx
import { execute } from 'your-favorite-graphql-client'

const id = params.id
const query = `
query GetToken($id: ID!) {
  token(id: $id) {
    id
    owner
  }
}
`

const result = await execute(query, {
  variables: {
    id,
  },
})
```

Doing so brings **many advantages**:

- **Easy to read and maintain** queries
- The GraphQL **server handles variables sanitization**
- **Variables can be cached** at server-level
- **Queries can be statically analyzed by tools** (more on this in the following sections)

### How to include fields conditionally in static queries

You might want to include the `owner` field only on a particular condition.

For this, you can leverage the `@include(if:...)` directive as follows:

```tsx
import { execute } from 'your-favorite-graphql-client'

const id = params.id
const query = `
query GetToken($id: ID!, $includeOwner: Boolean) {
  token(id: $id) {
    id
    owner @include(if: $includeOwner)
  }
}
`

const result = await execute(query, {
  variables: {
    id,
    includeOwner: true,
  },
})
```

> Note: The opposite directive is `@skip(if: ...)`.

### Ask for what you want

GraphQL became famous for its "Ask for what you want" tagline.

For this reason, there is no way, in GraphQL, to get all available fields without having to list them individually.

- When querying GraphQL APIs, always think of querying only the fields that will be actually used.
- Make sure queries only fetch as many entities as you actually need. By default, queries will fetch 100 entities in a collection, which is usually much more than what will actually be used, e.g., for display to the user. This applies not just to top-level collections in a query, but even more so to nested collections of entities.

For example, in the following query:

```graphql
query listTokens {
  tokens {
    # will fetch up to 100 tokens
    id
    transactions {
      # will fetch up to 100 transactions
      id
    }
  }
}
```

The response could contain 100 transactions for each of the 100 tokens.

If the application only needs 10 transactions, the query should explicitly set `first: 10` on the transactions field.

### Use a single query to request multiple records

By default, subgraphs have a singular entity for one record. For multiple records, use the plural entities and filter: `where: {id_in:[X,Y,Z]}` or `where: {volume_gt:100000}`

Example of inefficient querying:

```graphql
query SingleRecord {
  entity(id: X) {
    id
    name
  }
}
query SingleRecord {
  entity(id: Y) {
    id
    name
  }
}
```

Example of optimized querying:

```graphql
query ManyRecords {
  entities(where: { id_in: [X, Y] }) {
    id
    name
  }
}
```

### Combine multiple queries in a single request

Your application might require querying multiple types of data as follows:

```graphql
import { execute } from "your-favorite-graphql-client"

const tokensQuery = `
query GetTokens {
  tokens(first: 50) {
    id
    owner
  }
}
`
const countersQuery = `
query GetCounters {
  counters {
    id
    value
  }
}
`

const [tokens, counters] = Promise.all(
  [
    tokensQuery,
    countersQuery,
  ].map(execute)
)
```

While this implementation is totally valid, it will require two round trips with the GraphQL API.

Fortunately, it is also valid to send multiple queries in the same GraphQL request as follows:

```graphql
import { execute } from "your-favorite-graphql-client"

const query = `
query GetTokensandCounters {
  tokens(first: 50) {
    id
    owner
  }
  counters {
    id
    value
  }
}
`

const  { result: { tokens, counters } } = execute(query)
```

This approach will **improve the overall performance** by reducing the time spent on the network (saves you a round trip to the API) and will provide a **more concise implementation**.

### Leverage GraphQL Fragments

A helpful feature to write GraphQL queries is GraphQL Fragment.

Looking at the following query, you will notice that some fields are repeated across multiple Selection-Sets (`{ ... }`):

```graphql
query {
  bondEvents {
    id
    newDelegate {
      id
      active
      status
    }
    oldDelegate {
      id
      active
      status
    }
  }
}
```

Such repeated fields (`id`, `active`, `status`) bring many issues:

- More extensive queries become harder to read.
- When using tools that generate TypeScript types based on queries (_more on that in the last section_), `newDelegate` and `oldDelegate` will result in two distinct inline interfaces.

A refactored version of the query would be the following:

```graphql
query {
  bondEvents {
    id
    newDelegate {
      ...DelegateItem
    }
    oldDelegate {
      ...DelegateItem
    }
  }
}

# we define a fragment (subtype) on Transcoder
# to factorize repeated fields in the query
fragment DelegateItem on Transcoder {
  id
  active
  status
}
```

Using GraphQL `fragment` will improve readability (especially at scale) and result in better TypeScript types generation.

When using the types generation tool, the above query will generate a proper `DelegateItemFragment` type (_see last "Tools" section_).

### GraphQL Fragment do's and don'ts

### Fragment base must be a type

A Fragment cannot be based on a non-applicable type, in short, **on type not having fields**:

```graphql
fragment MyFragment on BigInt {
  # ...
}
```

`BigInt` is a **scalar** (native "plain" type) that cannot be used as a fragment's base.

#### How to spread a Fragment

Fragments are defined on specific types and should be used accordingly in queries.

Example:

```graphql
query {
  bondEvents {
    id
    newDelegate {
      ...VoteItem # Error! `VoteItem` cannot be spread on `Transcoder` type
    }
    oldDelegate {
      ...VoteItem
    }
  }
}

fragment VoteItem on Vote {
  id
  voter
}
```

`newDelegate` and `oldDelegate` are of type `Transcoder`.

It is not possible to spread a fragment of type `Vote` here.

#### Define Fragment as an atomic business unit of data

GraphQL `Fragment`s must be defined based on their usage.

For most use-case, defining one fragment per type (in the case of repeated fields usage or type generation) is sufficient.

Here is a rule of thumb for using fragments:

- When fields of the same type are repeated in a query, group them in a `Fragment`.
- When similar but different fields are repeated, create multiple fragments, for instance:

```graphql
# base fragment (mostly used in listing)
fragment Voter on Vote {
  id
  voter
}

# extended fragment (when querying a detailed view of a vote)
fragment VoteWithPoll on Vote {
  id
  voter
  choiceID
  poll {
    id
    proposal
  }
}
```

---

## The Essential Tools

### GraphQL web-based explorers

Iterating over queries by running them in your application can be cumbersome. For this reason, don't hesitate to use [Graph Explorer](https://thegraph.com/explorer) to test your queries before adding them to your application. Graph Explorer will provide you a preconfigured GraphQL playground to test your queries.

If you are looking for a more flexible way to debug/test your queries, other similar web-based tools are available such as [Altair](https://altairgraphql.dev/) and [GraphiQL](https://graphiql-online.com/graphiql).

### GraphQL Linting

In order to keep up with the mentioned above best practices and syntactic rules, it is highly recommended to use the following workflow and IDE tools.

**GraphQL ESLint**

[GraphQL ESLint](https://the-guild.dev/graphql/eslint/docs/getting-started) will help you stay on top of GraphQL best practices with zero effort.

[Setup the "operations-recommended"](https://the-guild.dev/graphql/eslint/docs/configs) config will enforce essential rules such as:

- `@graphql-eslint/fields-on-correct-type`: is a field used on a proper type?
- `@graphql-eslint/no-unused variables`: should a given variable stay unused?
- and more!

This will allow you to **catch errors without even testing queries** on the playground or running them in production!

### IDE plugins

**VSCode and GraphQL**

The [GraphQL VSCode extension](https://marketplace.visualstudio.com/items?itemName=GraphQL.vscode-graphql) is an excellent addition to your development workflow to get:

- Syntax highlighting
- Autocomplete suggestions
- Validation against schema
- Snippets
- Go to definition for fragments and input types

If you are using `graphql-eslint`, the [ESLint VSCode extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) is a must-have to visualize errors and warnings inlined in your code correctly.

**WebStorm/Intellij and GraphQL**

The [JS GraphQL plugin](https://plugins.jetbrains.com/plugin/8097-graphql/) will significantly improve your experience while working with GraphQL by providing:

- Syntax highlighting
- Autocomplete suggestions
- Validation against schema
- Snippets

For more information on this topic, check out the [WebStorm article](https://blog.jetbrains.com/webstorm/2019/04/featured-plugin-js-graphql/) which showcases all the plugin's main features.
import { RemoteContent } from 'nextra/data'
import { buildDynamicMDX } from 'nextra/remote'
import { buildGetStaticProps } from '@/src/buildGetStaticProps'
import { remarkReplaceLinks } from '@/src/remarkReplaceLinks'
import { Mermaid } from 'nextra/components'
import { visit } from 'unist-util-visit'
import json from '@/remote-files/graph-client.json'

export const getStaticPaths = () => ({
  fallback: false,
  paths: json.filePaths.map((filePath) => ({
    params: {
      slug: filePath.replace(/\.mdx?/, '').split('/'),
    },
  })),
})

export const getStaticProps = buildGetStaticProps(__filename, async ({ params }) => {
  const { filePaths, user, repo, branch, docsPath } = json
  const paths = params?.slug?.join('/')
  const foundPath = filePaths.find((filePath) => filePath.startsWith(paths))
  const baseURL = `https://raw.githubusercontent.com/${user}/${repo}/${branch}/${docsPath}${foundPath}`
  const response = await fetch(baseURL)
  const content = await response.text()
  const mdx = await buildDynamicMDX(content, {
    mdxOptions: {
      format: 'md',
      remarkPlugins: [
        () => (tree, _file) => {
          visit(tree, 'link', (node) => {
            if (node.url.startsWith('../')) {
              node.url = node.url.replace('../', `https://github.com/${user}/${repo}/tree/${branch}/`)
            }
          })
        },
        [remarkReplaceLinks, { foundPath, basePath: '/querying/graph-client/' }],
      ],
    },
    codeHighlight: false,
  })
  return {
    props: {
      ...mdx,
      hideLocaleSwitcher: true,
      remoteFilePath: `https://github.com/${user}/${repo}/tree/${branch}/${docsPath}${foundPath}`,
    },
  }
})

<RemoteContent components={{ Mermaid }} />
---
title: Subgraph ID vs Deployment ID
---

A subgraph is identified by a Subgraph ID, and each version of the subgraph is identified by a Deployment ID.

When querying a subgraph, either ID can be used, though it is generally suggested that the Deployment ID is used due to its ability to specify a specific version of a subgraph.

Here are some key differences between the two IDs: ![](/img/subgraph-id-vs-deployment-id.png)

## Deployment ID

The Deployment ID is the IPFS hash of the compiled manifest file, which refers to other files on IPFS instead of relative URLs on the computer. For example, the compiled manifest can be accessed via: `https://api.thegraph.com/ipfs/api/v0/cat?arg=QmQKXcNQQRdUvNRMGJiE2idoTu9fo5F5MRtKztH4WyKxED`. To change the Deployment ID, one can simply update the manifest file, such as modifying the description field as described in the [subgraph manifest documentation](https://github.com/graphprotocol/graph-node/blob/master/docs/subgraph-manifest.md#13-top-level-api).

When queries are made using a subgraph's Deployment ID, we are specifying a version of that subgraph to query. Using the Deployment ID to query a specific subgraph version results in a more sophisticated and robust setup as there is full control over the subgraph version being queried. However, this results in the need of updating the query code manually every time a new version of the subgraph is published.

Example endpoint that uses Deployment ID:

`https://gateway-arbitrum.network.thegraph.com/api/[api-key]/deployments/id/QmfYaVdSSekUeK6expfm47tP8adg3NNdEGnVExqswsSwaB`

## Subgraph ID

The Subgraph ID is a unique identifier for a subgraph. It remains constant across all versions of a subgraph. It is recommended to use the Subgraph ID to query the latest version of a subgraph, although there are some caveats.

Be aware that querying using Subgraph ID may result in queries being responded to by an older version of the subgraph due to the new version needing time to sync. Also, new versions could introduce breaking schema changes.

Example endpoint that uses Subgraph ID: `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/FL3ePDCBbShPvfRJTaSCNnehiqxsPHzpLud6CpbHoeKW`
---
title: Distributed Systems
---

The Graph is a protocol implemented as a distributed system.

Connections fail. Requests arrive out of order. Different computers with out-of-sync clocks and states process related requests. Servers restart. Re-orgs happen between requests. These problems are inherent to all distributed systems but are exacerbated in systems operating at a global scale.

Consider this example of what may occur if a client polls an Indexer for the latest data during a re-org.

1. Indexer ingests block 8
2. Request served to the client for block 8
3. Indexer ingests block 9
4. Indexer ingests block 10A
5. Request served to the client for block 10A
6. Indexer detects reorg to 10B and rolls back 10A
7. Request served to the client for block 9
8. Indexer ingests block 10B
9. Indexer ingests block 11
10. Request served to the client for block 11

From the point of view of the Indexer, things are progressing forward logically. Time is moving forward, though we did have to roll back an uncle block and play the block under consensus forward on top of it. Along the way, the Indexer serves requests using the latest state it knows about at that time.

From the point of view of the client, however, things appear chaotic. The client observes that the responses were for blocks 8, 10, 9, and 11 in that order. We call this the "block wobble" problem. When a client experiences block wobble, data may appear to contradict itself over time. The situation worsens when we consider that Indexers do not all ingest the latest blocks simultaneously, and your requests may be routed to multiple Indexers.

It is the responsibility of the client and server to work together to provide consistent data to the user. Different approaches must be used depending on the desired consistency as there is no one right program for every problem.

Reasoning through the implications of distributed systems is hard, but the fix may not be! We've established APIs and patterns to help you navigate some common use-cases. The following examples illustrate those patterns but still elide details required by production code (like error handling and cancellation) to not obfuscate the main ideas.

## Polling for updated data

The Graph provides the `block: { number_gte: $minBlock }` API, which ensures that the response is for a single block equal or higher to `$minBlock`. If the request is made to a `graph-node` instance and the min block is not yet synced, `graph-node` will return an error. If `graph-node` has synced min block, it will run the response for the latest block. If the request is made to an Edge & Node Gateway, the Gateway will filter out any Indexers that have not yet synced min block and make the request for the latest block the Indexer has synced.

We can use `number_gte` to ensure that time never travels backward when polling for data in a loop. Here is an example:

```javascript
/// Updates the protocol.paused variable to the latest
/// known value in a loop by fetching it using The Graph.
async function updateProtocolPaused() {
  // It's ok to start with minBlock at 0. The query will be served
  // using the latest block available. Setting minBlock to 0 is the
  // same as leaving out that argument.
  let minBlock = 0

  for (;;) {
    // Schedule a promise that will be ready once
    // the next Ethereum block will likely be available.
    const nextBlock = new Promise((f) => {
      setTimeout(f, 14000)
    })

    const query = `
        query GetProtocol($minBlock: Int!) {
            protocol(block: { number_gte: $minBlock }  id: "0") {
              paused
            }
            _meta {
                block {
                    number
                }
            }
        }`

    const variables = { minBlock }
    const response = await graphql(query, variables)
    minBlock = response._meta.block.number

    // TODO: Do something with the response data here instead of logging it.
    console.log(response.protocol.paused)

    // Sleep to wait for the next block
    await nextBlock
  }
}
```

## Fetching a set of related items

Another use-case is retrieving a large set or, more generally, retrieving related items across multiple requests. Unlike the polling case (where the desired consistency was to move forward in time), the desired consistency is for a single point in time.

Here we will use the `block: { hash: $blockHash }` argument to pin all of our results to the same block.

```javascript
/// Gets a list of domain names from a single block using pagination
async function getDomainNames() {
  // Set a cap on the maximum number of items to pull.
  let pages = 5
  const perPage = 1000

  // The first query will get the first page of results and also get the block
  // hash so that the remainder of the queries are consistent with the first.
  const listDomainsQuery = `
    query ListDomains($perPage: Int!) {
        domains(first: $perPage) {
            name
            id
        }
        _meta {
            block {
                hash
            }
        }
    }`

  let data = await graphql(listDomainsQuery, { perPage })
  let result = data.domains.map((d) => d.name)
  let blockHash = data._meta.block.hash

  let query
  // Continue fetching additional pages until either we run into the limit of
  // 5 pages total (specified above) or we know we have reached the last page
  // because the page has fewer entities than a full page.
  while (data.domains.length == perPage && --pages) {
    let lastID = data.domains[data.domains.length - 1].id
    query = `
        query ListDomains($perPage: Int!, $lastID: ID!, $blockHash: Bytes!) {
            domains(first: $perPage, where: { id_gt: $lastID }, block: { hash: $blockHash }) {
                name
                id
            }
        }`

    data = await graphql(query, { perPage, lastID, blockHash })

    // Accumulate domain names into the result
    for (domain of data.domains) {
      result.push(domain.name)
    }
  }
  return result
}
```

Note that in case of a re-org, the client will need to retry from the first request to update the block hash to a non-uncle block.
---
title: Querying from an Application
---

Once a subgraph is deployed to Subgraph Studio or to Graph Explorer, you will be given the endpoint for your GraphQL API that should look something like this:

**Subgraph Studio (testing endpoint)**

```sh
Queries (HTTP)
https://api.studio.thegraph.com/query/<ID>/<SUBGRAPH_NAME>/<VERSION>
```

**Graph Explorer**

```sh
Queries (HTTP)
https://gateway.thegraph.com/api/<API_KEY>/subgraphs/id/<SUBGRAPH_ID>
```

Using the GraphQL endpoint, you can use various GraphQL Client libraries to query the subgraph and populate your app with the data indexed by the subgraph.

Here are a couple of the more popular GraphQL clients in the ecosystem and how to use them:

## GraphQL clients

### Graph client

The Graph is providing it own GraphQL client, `graph-client` that supports unique features such as:

- Cross-chain Subgraph Handling: Querying from multiple subgraphs in a single query
- [Automatic Block Tracking](https://github.com/graphprotocol/graph-client/blob/main/packages/block-tracking/README.md)
- [Automatic Pagination](https://github.com/graphprotocol/graph-client/blob/main/packages/auto-pagination/README.md)
- Fully typed result

Also integrated with popular GraphQL clients such as Apollo and URQL and compatible with all environments (React, Angular, Node.js, React Native), using `graph-client` will give you the best experience for interacting with The Graph.

Let's look at how to fetch data from a subgraph with `graphql-client`.

To get started, make sure to install The Graph Client CLI in your project:

```sh
yarn add -D @graphprotocol/client-cli
# or, with NPM:
npm install --save-dev @graphprotocol/client-cli
```

Define your query in a `.graphql` file (or inlined in your `.js` or `.ts` file):

```graphql
query ExampleQuery {
  # this one is coming from compound-v2
  markets(first: 7) {
    borrowRate
    cash
    collateralFactor
  }
  # this one is coming from uniswap-v2
  pair(id: "0x00004ee988665cdda9a1080d5792cecd16dc1220") {
    id
    token0 {
      id
      symbol
      name
    }
    token1 {
      id
      symbol
      name
    }
  }
}
```

Then, create a configuration file (called `.graphclientrc.yml`) and point to your GraphQL endpoints provided by The Graph, for example:

```yaml
# .graphclientrc.yml
sources:
  - name: uniswapv2
    handler:
      graphql:
        endpoint: https://api.thegraph.com/subgraphs/name/uniswap/uniswap-v2
  - name: compoundv2
    handler:
      graphql:
        endpoint: https://api.thegraph.com/subgraphs/name/graphprotocol/compound-v2

documents:
  - ./src/example-query.graphql
```

Running the following The Graph Client CLI command will generate typed and ready to use JavaScript code:

```sh
graphclient build
```

Finally, update your `.ts` file to use the generated typed GraphQL documents:

```tsx
import React, { useEffect } from 'react'
// ...
// we import types and typed-graphql document from the generated code (`..graphclient/`)
import { ExampleQueryDocument, ExampleQueryQuery, execute } from '../.graphclient'

function App() {
  const [data, setData] = React.useState<ExampleQueryQuery>()

  useEffect(() => {
    execute(ExampleQueryDocument, {}).then((result) => {
      setData(result?.data)
    })
  }, [setData])
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>Graph Client Example</p>
        <fieldset>
          {data && (
            <form>
              <label>Data</label>
              <br />
              <textarea value={JSON.stringify(data, null, 2)} readOnly rows={25} />
            </form>
          )}
        </fieldset>
      </header>
    </div>
  )
}

export default App
```

**⚠️ Important notice**

`graph-client` is perfectly integrated with other GraphQL clients such as Apollo client, URQL, or React Query; you will [find examples in the official repository](https://github.com/graphprotocol/graph-client/tree/main/examples).

However, if you choose to go with another client, keep in mind that **you won't be able to get to use Cross-chain Subgraph Handling or Automatic Pagination, which are core features for querying The Graph**.

### Apollo client

[Apollo client](https://www.apollographql.com/docs/) is the ubiquitous GraphQL client on the front-end ecosystem.

Available for React, Angular, Vue, Ember, iOS, and Android, Apollo Client, although the heaviest client, brings many features to build advanced UI on top of GraphQL:

- advanced error handling
- pagination
- data prefetching
- optimistic UI
- local state management

Let's look at how to fetch data from a subgraph with Apollo client in a web project.

First, install `@apollo/client` and `graphql`:

```sh
npm install @apollo/client graphql
```

Then you can query the API with the following code:

```javascript
import { ApolloClient, InMemoryCache, gql } from '@apollo/client'

const APIURL = 'https://api.studio.thegraph.com/query//<SUBGRAPH_NAME>/'

const tokensQuery = `
  query {
    tokens {
      id
      tokenID
      contentURI
      metadataURI
    }
  }
`

const client = new ApolloClient({
  uri: APIURL,
  cache: new InMemoryCache(),
})

client
  .query({
    query: gql(tokensQuery),
  })
  .then((data) => console.log('Subgraph data: ', data))
  .catch((err) => {
    console.log('Error fetching data: ', err)
  })
```

To use variables, you can pass in a `variables` argument to the query:

```javascript
const tokensQuery = `
  query($first: Int, $orderBy: BigInt, $orderDirection: String) {
    tokens(
      first: $first, orderBy: $orderBy, orderDirection: $orderDirection
    ) {
      id
      tokenID
      contentURI
      metadataURI
    }
  }
`

client
  .query({
    query: gql(tokensQuery),
    variables: {
      first: 10,
      orderBy: 'createdAtTimestamp',
      orderDirection: 'desc',
    },
  })
  .then((data) => console.log('Subgraph data: ', data))
  .catch((err) => {
    console.log('Error fetching data: ', err)
  })
```

### URQL

Another option is [URQL](https://formidable.com/open-source/urql/) which is available within Node.js, React/Preact, Vue, and Svelte environments, with more advanced features:

- Flexible cache system
- Extensible design (easing adding new capabilities on top of it)
- Lightweight bundle (~5x lighter than Apollo Client)
- Support for file uploads and offline mode

Let's look at how to fetch data from a subgraph with URQL in a web project.

First, install `urql` and `graphql`:

```sh
npm install urql graphql
```

Then you can query the API with the following code:

```javascript
import { createClient } from 'urql'

const APIURL = 'https://api.thegraph.com/subgraphs/name/username/subgraphname'

const tokensQuery = `
  query {
    tokens {
      id
      tokenID
      contentURI
      metadataURI
    }
  }
`

const client = createClient({
  url: APIURL,
})

const data = await client.query(tokensQuery).toPromise()
```
---
title: Supported Network Requirements
---

| Network | Guides | System Requirements | Indexing Rewards |
| --- | --- | --- | :-: |
| Arbitrum | [Baremetal Guide](https://docs.infradao.com/archive-nodes-101/arbitrum/baremetal)<br /> [Docker Guide](https://docs.infradao.com/archive-nodes-101/arbitrum/docker) | 4+ core CPU<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >= 8 TiB NVMe SSD<br /> _last updated August 2023_ | ✅ |
| Avalanche | [Docker Guide](https://docs.infradao.com/archive-nodes-101/avalanche/docker) | 4 core / 8 threads CPU<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >= 5 TiB NVMe SSD<br /> _last updated August 2023_ | ✅ |
| Base | [Erigon Baremetal Guide](https://docs.infradao.com/archive-nodes-101/base/erigon/baremetal)<br /><br /> [GETH Baremetal Guide](https://docs.infradao.com/archive-nodes-101/base/geth/baremetal)<br /> [GETH Docker Guide](https://docs.infradao.com/archive-nodes-101/base/geth/docker) | 8+ core CPU<br /> Debian 12/Ubuntu 22.04<br /> 16 GB RAM<br /> >= 4.5TB (NVME preffered)<br /> _last updated 14th May 2024_ | ✅ |
| Binance | [Erigon Baremetal Guide](https://docs.infradao.com/archive-nodes-101/binance/erigon/baremetal) | 8 core / 16 threads CPU<br /> Ubuntu 22.04<br /> >=32 GB RAM<br /> >= 14 TiB NVMe SSD<br /> _last updated 22nd June 2024_ | ✅ |
| Celo | [Docker Guide](https://docs.infradao.com/archive-nodes-101/celo/docker) | 4 core / 8 threads CPU<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >= 2 TiB NVMe SSD<br /> _last updated August 2023_ | ✅ |
| Ethereum | [Docker Guide](https://docs.infradao.com/archive-nodes-101/ethereum/erigon/docker) | Higher clock speed over core count<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >=3TB (NVMe recommended)<br /> _last updated August 2023_ | ✅ |
| Fantom | [Docker Guide](https://docs.infradao.com/archive-nodes-101/fantom/docker) | 4 core / 8 threads CPU<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >= 13 TiB NVMe SSD<br /> _last updated August 2023_ | ✅ |
| Gnosis | [Baremetal Guide](https://docs.infradao.com/archive-nodes-101/gnosis/erigon/baremetal) | 6 core / 12 threads CPU<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >= 3 TiB NVMe SSD<br /> _last updated August 2023_ | ✅ |
| Linea | [Baremetal Guide](https://docs.infradao.com/archive-nodes-101/linea/baremetal) | 4+ core CPU<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >= 1 TiB NVMe SSD<br /> _last updated 2nd April 2024_ | ✅ |
| Optimism | [Erigon Baremetal Guide](https://docs.infradao.com/archive-nodes-101/optimism/erigon/baremetal)<br /><br /> [GETH Baremetal Guide](https://docs.infradao.com/archive-nodes-101/optimism/geth/baremetal)<br /> [GETH Docker Guide](https://docs.infradao.com/archive-nodes-101/optimism/geth/docker) | 4 core / 8 threads CPU<br /> Ubuntu 22.04<br /> 16GB+ RAM<br /> >= 8 TiB NVMe SSD<br /> _last updated August 2023_ | ✅ |
| Polygon | [Docker Guide](https://docs.infradao.com/archive-nodes-101/polygon/docker) | 16 core CPU<br /> Ubuntu 22.04<br /> 32GB+ RAM<br /> >= 10 TiB NVMe SSD<br /> _last updated August 2023_ | ✅ |
| Scroll | [Baremetal Guide](https://docs.infradao.com/archive-nodes-101/scroll/baremetal)<br /> [Docker Guide](https://docs.infradao.com/archive-nodes-101/scroll/docker) | 4 core / 8 threads CPU<br /> Debian 12<br /> 16GB+ RAM<br /> >= 1 TiB NVMe SSD<br /> _last updated 3rd April 2024_ | ✅ |
---
title: How to Use Subgraph Studio
---

Welcome to your new launchpad 👩🏽‍🚀

Subgraph Studio is your place to build and create subgraphs, add metadata, and publish them to the new decentralized Explorer (more on that [here](/network/explorer)).

What you can do in Subgraph Studio:

- Create a subgraph through the Studio UI
- Deploy a subgraph using the CLI
- Publish a subgraph with the Studio UI
- Test it in the playground
- Integrate it in staging using the query URL
- Create and manage your API keys for specific subgraphs

Here in Subgraph Studio, you have full control over your subgraphs. Not only can you test your subgraphs before you publish them, but you can also restrict your API keys to specific domains and only allow certain Indexers to query from their API keys.

Querying subgraphs generates query fees, used to reward [Indexers](/network/indexing) on the Graph network. If you’re a dapp developer or subgraph developer, the Studio will empower you to build better subgraphs to power your or your community’s queries. The Studio is comprised of 5 main parts:

- Your user account controls
- A list of subgraphs that you’ve created
- A section to manage, view details and visualize the status of a specific subgraph
- A section to manage your API keys that you will need to query a subgraph
- A section to manage your billing

## How to Create Your Account

1. Sign in with your wallet - you can do this via MetaMask, WalletConnect, Coinbase Wallet or Safe.
1. Once you sign in, you will see your unique deploy key on your account home page. This will allow you to either publish your subgraphs or manage your API keys + billing. You will have a unique deploy key that can be re-generated if you think it has been compromised.

## How to Create a Subgraph in Subgraph Studio

<VideoEmbed youtube="nGIFuC69bSA" />

## Subgraph Compatibility with The Graph Network

In order to be supported by Indexers on The Graph Network, subgraphs must:

- Index a [supported network](/developing/supported-networks)
- Must not use any of the following features:
  - ipfs.cat & ipfs.map
  - Non-fatal errors
  - Grafting

More features & networks will be added to The Graph Network incrementally.

### Subgraph lifecycle flow

![Subgraph Lifecycle](/img/subgraph-lifecycle.png)

After you have created your subgraph, you will be able to deploy it using the [CLI](https://github.com/graphprotocol/graph-tooling/tree/main/packages/cli), or command-line interface. Deploying a subgraph with the CLI will push the subgraph to the Studio where you’ll be able to test subgraphs using the playground. This will eventually allow you to publish to the Graph Network. For more information on CLI setup, [check this out](/developing/defining-a-subgraph#install-the-graph-cli) (psst, make sure you have your deploy key on hand). Remember, deploying is **not the same as** publishing. When you deploy a subgraph, you just push it to the Studio where you’re able to test it. Versus, when you publish a subgraph, you are publishing it on-chain.

## Testing your Subgraph in Subgraph Studio

If you’d like to test your subgraph before publishing it to the network, you can do this in the Subgraph **Playground** or look at your logs. The Subgraph logs will tell you **where** your subgraph fails in the case that it does.

## Publish your Subgraph in Subgraph Studio

You’ve made it this far - congrats!

In order to publish your subgraph successfully, you’ll need to go through the following steps outlined in this [section](/publishing/publishing-a-subgraph/).

Check out the video overview below as well:

<VideoEmbed youtube="satdwdbvzAQ" />

Remember, while you’re going through your publishing flow, you’ll be able to push to either Arbitrum One or Arbitrum Sepolia. If you’re a first-time subgraph developer, we highly suggest you start with publishing to Arbitrum Sepolia, which is free to do. This will allow you to see how the subgraph will work in Graph Explorer and will allow you to test curation elements.

Indexers need to submit mandatory Proof of Indexing records as of a specific block hash. Because publishing a subgraph is an action taken on-chain, remember that the transaction can take up to a few minutes to go through. Any address you use to publish the contract will be the only one able to publish future versions. Choose wisely!

Subgraphs with curation signal are shown to Indexers so that they can be indexed on the decentralized network. You can publish subgraphs and signal in one transaction, which allows you to mint the first curation signal on the subgraph and saves on gas costs. By adding your signal to the signal later provided by Curators, your subgraph will also have a higher chance of ultimately serving queries.

**Now that you’ve published your subgraph, let’s get into how you’ll manage them on a regular basis.** Note that you cannot publish your subgraph to the network if it has failed syncing. This is usually because the subgraph has bugs - the logs will tell you where those issues exist!

## Versioning your Subgraph with the CLI

Developers might want to update their subgraph, for a variety of reasons. When this is the case, you can deploy a new version of your subgraph to the Studio using the CLI (it will only be private at this point) and if you are happy with it, you can publish this new deployment to Graph Explorer. This will create a new version of your subgraph that curators can start signaling on and Indexers will be able to index this new version.

Up until recently, developers were forced to deploy and publish a new version of their subgraph to the Explorer to update the metadata of their subgraphs. Now, developers can update the metadata of their subgraphs **without having to publish a new version**. Developers can update their subgraph details in the Studio (under the profile picture, name, description, etc) by checking an option called **Update Details** in Graph Explorer. If this is checked, an on-chain transaction will be generated that updates subgraph details in the Explorer without having to publish a new version with a new deployment.

Please note that there are costs associated with publishing a new version of a subgraph to the network. In addition to the transaction fees, developers must also fund a part of the curation tax on the auto-migrating signal. You cannot publish a new version of your subgraph if curators have not signaled on it. For more information on the risks of curation, please read more [here](/network/curating).

### Automatic Archiving of Subgraph Versions

Whenever you deploy a new subgraph version in Subgraph Studio, the previous version will be archived. Archived versions won't be indexed/synced and therefore cannot be queried. You can unarchive an archived version of your subgraph in the Studio UI. Please note that previous versions of non-published subgraphs deployed to the Studio will be automatically archived.

![Subgraph Studio - Unarchive](/img/Unarchive.png)
---
title: Subgraph Studio FAQs
---

## 1. What is Subgraph Studio?

[Subgraph Studio](https://thegraph.com/studio/) is a dapp for creating, managing, and publishing subgraphs and API keys.

## 2. How do I create an API Key?

To create an API, navigate to Subgraph Studio and connect your wallet. You will be able to click the API keys tab at the top. There, you will be able to create an API key.

## 3. Can I create multiple API Keys?

Yes! You can create multiple API Keys to use in different projects. Check out the link [here](https://thegraph.com/studio/apikeys/).

## 4. How do I restrict a domain for an API Key?

After creating an API Key, in the Security section, you can define the domains that can query a specific API Key.

## 5. Can I transfer my subgraph to another owner?

Yes, subgraphs that have been published to Arbitrum One can be transferred to a new wallet or a Multisig. You can do so by clicking the three dots next to the 'Publish' button on the subgraph's details page and selecting 'Transfer ownership'.

Note that you will no longer be able to see or edit the subgraph in Studio once it has been transferred.

## 6. How do I find query URLs for subgraphs if I’m not the developer of the subgraph I want to use?

You can find the query URL of each subgraph in the Subgraph Details section of Graph Explorer. When you click on the “Query” button, you will be directed to a pane wherein you can view the query URL of the subgraph you’re interested in. You can then replace the `<api_key>` placeholder with the API key you wish to leverage in Subgraph Studio.

Remember that you can create an API key and query any subgraph published to the network, even if you build a subgraph yourself. These queries via the new API key, are paid queries as any other on the network.
---
title: Deploying a Subgraph to Multiple Networks
---

This page explains how to deploy a subgraph to multiple networks. To deploy a subgraph you need to first install the [Graph CLI](https://github.com/graphprotocol/graph-tooling/tree/main/packages/cli). If you have not created a subgraph already, see [Creating a subgraph](/developing/creating-a-subgraph).

## Deploying the subgraph to multiple networks

In some cases, you will want to deploy the same subgraph to multiple networks without duplicating all of its code. The main challenge that comes with this is that the contract addresses on these networks are different.

### Using `graph-cli`

Both `graph build` (since `v0.29.0`) and `graph deploy` (since `v0.32.0`) accept two new options:

```sh
Options:

      ...
      --network <name>          Network configuration to use from the networks config file
      --network-file <path>     Networks config file path (default: "./networks.json")
```

You can use the `--network` option to specify a network configuration from a `json` standard file (defaults to `networks.json`) to easily update your subgraph during development.

> Note: The `init` command will now auto-generate a `networks.json` based on the provided information. You will then be able to update existing or add additional networks.

If you don't have a `networks.json` file, you'll need to manually create one with the following structure:

```json
{
    "network1": { // the network name
        "dataSource1": { // the dataSource name
            "address": "0xabc...", // the contract address (optional)
            "startBlock": 123456 // the startBlock (optional)
        },
        "dataSource2": {
            "address": "0x123...",
            "startBlock": 123444
        }
    },
    "network2": {
        "dataSource1": {
            "address": "0x987...",
            "startBlock": 123
        },
        "dataSource2": {
            "address": "0xxyz..",
            "startBlock": 456
        }
    },
    ...
}
```

> Note: You don't have to specify any of the `templates` (if you have any) in the config file, only the `dataSources`. If there are any `templates` declared in the `subgraph.yaml` file, their network will be automatically updated to the one specified with the `--network` option.

Now, let's assume you want to be able to deploy your subgraph to the `mainnet` and `sepolia` networks, and this is your `subgraph.yaml`:

```yaml
# ...
dataSources:
  - kind: ethereum/contract
    name: Gravity
    network: mainnet
    source:
      address: '0x123...'
      abi: Gravity
    mapping:
      kind: ethereum/events
```

This is what your networks config file should look like:

```json
{
  "mainnet": {
    "Gravity": {
      "address": "0x123..."
    }
  },
  "sepolia": {
    "Gravity": {
      "address": "0xabc..."
    }
  }
}
```

Now we can run one of the following commands:

```sh
# Using default networks.json file
yarn build --network sepolia

# Using custom named file
yarn build --network sepolia --network-file path/to/config
```

The `build` command will update your `subgraph.yaml` with the `sepolia` configuration and then re-compile the subgraph. Your `subgraph.yaml` file now should look like this:

```yaml
# ...
dataSources:
  - kind: ethereum/contract
    name: Gravity
    network: sepolia
    source:
      address: '0xabc...'
      abi: Gravity
    mapping:
      kind: ethereum/events
```

Now you are ready to `yarn deploy`.

> Note: As mentioned earlier, since `graph-cli 0.32.0` you can directly run `yarn deploy` with the `--network` option:

```sh
# Using default networks.json file
yarn deploy --network sepolia

# Using custom named file
yarn deploy --network sepolia --network-file path/to/config
```

### Using subgraph.yaml template

One way to parameterize aspects like contract addresses using older `graph-cli` versions is to generate parts of it with a templating system like [Mustache](https://mustache.github.io/) or [Handlebars](https://handlebarsjs.com/).

To illustrate this approach, let's assume a subgraph should be deployed to mainnet and Sepolia using different contract addresses. You could then define two config files providing the addresses for each network:

```json
{
  "network": "mainnet",
  "address": "0x123..."
}
```

and

```json
{
  "network": "sepolia",
  "address": "0xabc..."
}
```

Along with that, you would substitute the network name and addresses in the manifest with variable placeholders `{{network}}` and `{{address}}` and rename the manifest to e.g. `subgraph.template.yaml`:

```yaml
# ...
dataSources:
  - kind: ethereum/contract
    name: Gravity
    network: mainnet
    network: {{network}}
    source:
      address: '0x2E645469f354BB4F5c8a05B3b30A929361cf77eC'
      address: '{{address}}'
      abi: Gravity
    mapping:
      kind: ethereum/events
```

In order to generate a manifest to either network, you could add two additional commands to `package.json` along with a dependency on `mustache`:

```json
{
  ...
  "scripts": {
    ...
    "prepare:mainnet": "mustache config/mainnet.json subgraph.template.yaml > subgraph.yaml",
    "prepare:sepolia": "mustache config/sepolia.json subgraph.template.yaml > subgraph.yaml"
  },
  "devDependencies": {
    ...
    "mustache": "^3.1.0"
  }
}
```

To deploy this subgraph for mainnet or Sepolia you would now simply run one of the two following commands:

```sh
# Mainnet:
yarn prepare:mainnet && yarn deploy

# Sepolia:
yarn prepare:sepolia && yarn deploy
```

A working example of this can be found [here](https://github.com/graphprotocol/example-subgraph/tree/371232cf68e6d814facf5e5413ad0fef65144759).

**Note:** This approach can also be applied to more complex situations, where it is necessary to substitute more than contract addresses and network names or where generating mappings or ABIs from templates as well.

This will give you the `chainHeadBlock` which you can compare with the `latestBlock` on your subgraph to check if it is running behind. `synced` informs if the subgraph has ever caught up to the chain. `health` can currently take the values of `healthy` if no errors occurred, or `failed` if there was an error which halted the progress of the subgraph. In this case, you can check the `fatalError` field for details on this error.

## Subgraph Studio subgraph archive policy

A subgraph version in Studio is archived if and only if it meets the following criteria:

- The version is not published to the network (or pending publish)
- The version was created 45 or more days ago
- The subgraph hasn't been queried in 30 days

In addition, when a new version is deployed, if the subgraph has not been published, then the N-2 version of the subgraph is archived.

Every subgraph affected with this policy has an option to bring the version in question back.

## Checking subgraph health

If a subgraph syncs successfully, that is a good sign that it will continue to run well forever. However, new triggers on the network might cause your subgraph to hit an untested error condition or it may start to fall behind due to performance issues or issues with the node operators.

Graph Node exposes a GraphQL endpoint which you can query to check the status of your subgraph. On the hosted service, it is available at `https://api.thegraph.com/index-node/graphql`. On a local node, it is available on port `8030/graphql` by default. The full schema for this endpoint can be found [here](https://github.com/graphprotocol/graph-node/blob/master/server/index-node/src/schema.graphql). Here is an example query that checks the status of the current version of a subgraph:

```graphql
{
  indexingStatusForCurrentVersion(subgraphName: "org/subgraph") {
    synced
    health
    fatalError {
      message
      block {
        number
        hash
      }
      handler
    }
    chains {
      chainHeadBlock {
        number
      }
      latestBlock {
        number
      }
    }
  }
}
```

This will give you the `chainHeadBlock` which you can compare with the `latestBlock` on your subgraph to check if it is running behind. `synced` informs if the subgraph has ever caught up to the chain. `health` can currently take the values of `healthy` if no errors occurred, or `failed` if there was an error which halted the progress of the subgraph. In this case, you can check the `fatalError` field for details on this error.
---
title: Deploying a Subgraph to Subgraph Studio
---

These are the steps to deploy your subgraph to Subgraph Studio:

- Install The Graph CLI (with either yarn or npm)
- Create your Subgraph in Subgraph Studio
- Authenticate your account from the CLI
- Deploying a Subgraph to Subgraph Studio

## Installing Graph CLI

There is a CLI to deploy subgraphs to [Subgraph Studio](https://thegraph.com/studio/). Here are the commands to install `graph-cli`. This can be done using npm or yarn.

**Install with yarn:**

```bash
yarn global add @graphprotocol/graph-cli
```

**Install with npm:**

```bash
npm install -g @graphprotocol/graph-cli
```

## Create your Subgraph in Subgraph Studio

Before deploying your actual subgraph you need to create a subgraph in [Subgraph Studio](https://thegraph.com/studio/). We recommend you read our [Studio documentation](/deploying/subgraph-studio) to learn more about this.

## Initialize your Subgraph

Once your subgraph has been created in Subgraph Studio you can initialize the subgraph code using this command:

```bash
graph init --studio <SUBGRAPH_SLUG>
```

The `<SUBGRAPH_SLUG>` value can be found on your subgraph details page in Subgraph Studio:

![Subgraph Studio - Slug](/img/doc-subgraph-slug.png)

After running `graph init`, you will be asked to input the contract address, network, and ABI that you want to query. Doing this will generate a new folder on your local machine with some basic code to start working on your subgraph. You can then finalize your subgraph to make sure it works as expected.

## Graph Auth

Before being able to deploy your subgraph to Subgraph Studio, you need to login into your account within the CLI. To do this, you will need your deploy key that you can find on your "My Subgraphs" page or your subgraph details page.

Here is the command that you need to use to authenticate from the CLI:

```bash
graph auth --studio <DEPLOY KEY>
```

## Deploying a Subgraph to Subgraph Studio

Once you are ready, you can deploy your subgraph to Subgraph Studio. Doing this won't publish your subgraph to the decentralized network, it will only deploy it to your Studio account where you will be able to test it and update the metadata.

Here is the CLI command that you need to use to deploy your subgraph.

```bash
graph deploy --studio <SUBGRAPH_SLUG>
```

After running this command, the CLI will ask for a version label, you can name it however you want, you can use labels such as `0.1` and `0.2` or use letters as well such as `uniswap-v2-0.1`. Those labels will be visible in Graph Explorer and can be used by curators to decide if they want to signal on this version or not, so choose them wisely.

Once deployed, you can test your subgraph in Subgraph Studio using the playground, deploy another version if needed, update the metadata, and when you are ready, publish your subgraph to Graph Explorer.
