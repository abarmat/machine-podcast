Sam | 2024-09-08 22:49:22 UTC | #1

## 👩‍🚀 Summary

Over the past month, we've made key progress across several areas. We identified and fixed bugs for TAP, releasing two new candidates ahead of `1.0.0`. In verifiability, we are advancing our proof-of-concept to verify post-merge Ethereum data and plan to extend `flat-head` for further verification capabilities next month. Our synthetic dataset generation paper, researching natural language to SQL, has undergone peer review, and we're incorporating feedback while preparing to release the data and code alongside our paper. Lastly, we paused work on the Inference Service to focus on more pressing priorities and will investigate AI applications for The Graph in the coming month.


## TAP

We've been running TAP in prod this past month on our indexer. We've found numerous bugs and paused further external testing while we worked on the various fixes. Consequently, we released two more release candidates, `1.0.0-rc.5` and `1.0.0-rc.6`, before releasing `1.0.0`. 

For the next month, we expect to find new bugs as new Indexers join in and improve the documentation further as Indexers work through their migration.

## Verifiability

We are continuing to work on extending `flat-head` to verify post-merge Ethereum data stored in Firehose flat files. We currently have tooling to verify inclusion proofs for Ethereum Consensus Layer (CL) blocks and states, e.g., to prove that an Ethereum execution layer block hash was included in a CL layer block. We are working on a proof-of-concept to verify that one ERA (8192 execution blocks) is included in a CL state. We are investigating using Pinax's Ethereum CL Firehose implementation to obtain the necessary CL information. We plan to finish this PoC in the coming month and begin extending `flat-head` to support post-merge verification.

## AI 

### Synthetic Datasets for Natural Language to SQL
We recently completed the peer review process for our synthetic data generation research, receiving invaluable feedback that has helped refine our report and inform the future direction of our work. Building on this feedback, we've expanded our initial investigation to explore the effectiveness of our data generation methodology in an in-domain setting using the Spider benchmark. We are currently awaiting results from this latest round of experiments. We plan to update our report with these findings in the coming weeks. Additionally, we look forward to releasing our synthetic datasets, model weights, and open-source code for data generation. These resources will be made available in tandem with the public release of our research.

### Inference Service
Last month, we reprioritized our work. We found that there were higher-priority things we could work on instead of the Inference Service. In the short term, we will pause work on the Inference Service and investigate ways to directly improve The Graph using AI. That investigation is our plan for next month.

-------------------------

