chris | 2024-09-09 09:49:27 UTC | #1


## 🧑‍🚀 Executive Summary

We are excited to share the latest updates and advancements across our workstreams, bringing new features and enhacements to the community.

In [GraphSeer](https://graphseer.com/), our team has been working on a new backend that calculates average statistics for Delegators, setting the stage for smooth integration with the frontend. We're also enhancing the overall developer experience with improvements to the local development environment and CI/CD processes. Plus, stay tuned for the **upcoming GraphSeer account feature** :eyes:, which will soon be available in the app! Other recent updates include autopagination for queries, along with SEO and styling improvements that will be available soon in the app.

Launchpad has seen some great updates as well! We've rolled out chart enhancements and introduced a new component: [Launchpad Taskfiles](https://github.com/graphops/launchpad-taskfiles). This new component allows us to modularize predefined Indexer tasks and ship them to users of Launchpad seamlessly. We’ve also updated stable namespaces across multiple blockchains.

For Network Operations, our efforts have led to the successful implementation of a consumer for all Kafka topics in the QoS Oracle V2 and the orchestration of a comprehensive testing environment. We also have been working on a new processing pipeline, and on an IPFS Publishing pipeline. Additionally, we’ve refactored SMART to operate within the decentralized network.

Happy September everyone ✨

## :tada: Looking Back (what was delivered)

### GraphSeer ([Launch the app](https://graphseer.com), [Learn more](https://graphops.xyz/our-work/graphseer-explorer))

* Continued significant codebase improvements that are near completion
* Implemented GraphSeer account (soon in the app!)
* Implemented autopagination for queries which allows us to display complete data for deployments and allocations SEO and styling improvements
* Bug fixes 
    * Indexers with no allocations or performance data missing and 
    * ENS name for Subgraph Deployment Allocations table
    * Deployments with no allocations
* Backend work for average statistics for Delegators, yet to be included in the frontend
* Enhancing developer experience
* Local developer environment development
* Improved CI/CD

### Launchpad ([Documentation](https://docs.graphops.xyz/launchpad/intro), [Starter](https://github.com/graphops/launchpad-starter), [Charts](https://github.com/graphops/launchpad-charts), [Namespaces](https://github.com/graphops/launchpad-namespaces))

* Added a new Launchpad component: [launchpad-taskfiles](https://github.com/graphops/launchpad-taskfiles), which implements [remote taskfiles](https://taskfile.dev/experiments/remote-taskfiles/) thus modularizing our taskfiles out of [launchpad-starter](https://github.com/graphops/launchpad-starter/pull/48/files)
* Introduction of metric relabelings for better accuracy in Arbitrum service monitors and added functionality to proxyd, alongside fixes in Lighthouse service for improved reliability
* Chart updates for Erigon, Arbitrum-Nitro, Subgraph-Radio, Listener-Radio, Lighthouse, Celo, Nimbus, Generic-App Proxyd all with stable releases
* New stable namespaces versions of Ethereum, Gnosis, Polygon, Arbitrum, Celo, Graph, Monitoring, Ingress, Postgres-Operator
* Pre-release version of graph-network-indexer chart, with support for TAP agent and new indexer-service version out
* Pre-release version of firehose-evm chart (chart for all fireeth based chains)
* We have changed the format of Launchpad Office Hours: We decided to move to hosting launchpad related session on an ad-hoc basis in IOH and have an additional Launchpad watch biweekly IOH segment

[details="Launchpad Development Activity"]

- [Launchpad Charts](https://github.com/graphops/launchpad-charts) pull requests merged:
  - [PR #339](https://github.com/graphops/launchpad-charts/pull/339), [PR #340](https://github.com/graphops/launchpad-charts/pull/340), [PR #341](https://github.com/graphops/launchpad-charts/pull/341), [PR #342](https://github.com/graphops/launchpad-charts/pull/342): Released updates for various products including Listener Radio v0.2.5, Celo v0.1.5, Subgraph Radio v0.2.13, and Nimbus v0.5.16.
  - [PR #345](https://github.com/graphops/launchpad-charts/pull/345): Implemented conditional hook annotations for the generic app.
  - [PR #343](https://github.com/graphops/launchpad-charts/pull/343), [PR #346](https://github.com/graphops/launchpad-charts/pull/346): Updated dependencies for proxyd and Arbitrum.
  - [PR #344](https://github.com/graphops/launchpad-charts/pull/344), [PR #351](https://github.com/graphops/launchpad-charts/pull/351): Advanced the capabilities of the graph-network-indexer with the addition of Scalar TAP support and updated documentation and tap-agent.
- [Launchpad Starter](https://github.com/graphops/launchpad-starter) pull requests merged:
  - [PR #48](https://github.com/graphops/launchpad-starter/pull/48): Incorporates Launchpad Taskfiles for enhanced project management and workflows
- [Launchpad Namespaces](https://github.com/graphops/launchpad-namespaces) pull requests merged:
  - Dependency Updates:
    - Monitoring Dependencies: A series of updates to the kube-prometheus-stack, progressively through versions from 61.7.1 to 62.6.0 across [PR #862](https://github.com/graphops/launchpad-namespaces/pull/862) to [PR #930](https://github.com/graphops/launchpad-namespaces/pull/930), and promtail from 6.16.4 to 6.16.5 in [PR #910](https://github.com/graphops/launchpad-namespaces/pull/910).
    - Graph Network Indexer Dependencies: Updates were applied from version 0.2.7 to 0.5.0-canary.2, through [PR #926](https://github.com/graphops/launchpad-namespaces/pull/926) and [PR #931](https://github.com/graphops/launchpad-namespaces/pull/931).
    - Proxyd and Various Blockchain Dependencies: A comprehensive update, applied across Ethereum, Gnosis, Polygon, Arbitrum, and Celo environments, effected through a series of PRs from [PR #856](https://github.com/graphops/launchpad-namespaces/pull/856) to [PR #919](https://github.com/graphops/launchpad-namespaces/pull/919).
    - Miscellaneous Helm Dependencies: Included updates for ingress controller, cert-manager, nginx, and the postgres-operator, [PR #891](https://github.com/graphops/launchpad-namespaces/pull/891) and [PR #903](https://github.com/graphops/launchpad-namespaces/pull/903).
  - Feature Enhancements and Maintenance:
    - [PR #918](https://github.com/graphops/launchpad-namespaces/pull/918) introduces support for hyphen (-) in flavor names.
    - [PR #922](https://github.com/graphops/launchpad-namespaces/pull/922) focuses on updating yarn packages and ensuring compatibility with husky v10.
[/details]

### Network Operations ([Graph Network Subgraph](https://github.com/graphprotocol/graph-network-subgraph), [Graph Network Substreams](https://github.com/graphops/graph-network-substreams))

* QoS Oracle V2
    * Implemented consumer for all Kafka topics
    * Orchestrated testing environment
    * Implemented processing pipeline
    * Started work on IPFS Publishing pipeline
* SMART (subgraph monitoring)
    * Full refactor to use the decentralized network instead of the deprecated hosted service implementation

### Graphcast SDK ([Documentation](https://docs.graphops.xyz/graphcast/intro), [SDK Crate](https://crates.io/crates/graphcast-sdk), [SDK Source](https://github.com/graphops/graphcast-sdk))

* Improved performance of the active Indexers query on Listener Radio


### Ecosystem Relations

- [Recordings](https://www.youtube.com/channel/UCQ7G_cCufIVUdUUUf-jdoVA) and [agendas](https://graphops.notion.site/Indexer-Office-Hours-952e0b50a65144768aab922e2c9d102a) for Indexer Office Hours are available. Follow updates on Twitter [@TheGraphIOH](https://twitter.com/TheGraphIOH).

## :rocket: Looking Ahead (upcoming priorities)
- GraphSeer
  - Continue progressing on backend development
- Launchpad
  - Continue with testing and release stable versions of `graph-network-indexer` and `firehose-evm charts`
  - Namespaces support for firehose EVM chains
  - Updated Graph Namespace with TAP support and new graph-network-indexer chart

- Ecosystem Relations
  - Please join the community for Indexer Office Hours on Tuesday every week at 6pm UTC in the [Graph Protocol Discord](https://thegraph.com/discord)

-------------------------

