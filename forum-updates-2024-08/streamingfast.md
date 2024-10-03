abourget | 2024-09-10 15:52:51 UTC | #1

Hey Graph land!

Lots of work here at StreamingFast to turn Substreams into an extraordinary product. We're nearing some breakthroughs here.


## Looking back

- Chains:
	- We've announced Sei network integration: https://x.com/graphprotocol/status/1821273883464626467
	- We've been working on deep decoding of Polkadot, Cosmos, StarkNet data structures, to bridge the worlds into Substreams.
- More Solana subgraphs hitting production: https://x.com/streamingfastio/status/1828432257888969129 
- We've been getting our hands dirty, dogfooding, writing Substreams modules for Hivemapper.  https://github.com/streamingfast/substreams-hivemapper
- Lots of work on Substreams, the engine, the CLI, and the experience around. The development flow has been extremely improved. You can now try it by starting at: https://github.com/streamingfast/substreams-starter .. let us know what you think.
	- The GUI has seen massive improvements, allowing you to edit most parameters, build directly from in there, navigate much more clearly and easily, switch modules, explore data about them, etc.. And you can now just start it with `substreams gui`, no parameters. That's simpler :)
	- We've made improvements to the Rust libraries for `substreams` and to our Solana-specific libaries.
	- We've fixed a bunch of issues with metering related to billing (those running services connected to thegraph.market, please update), as well as issues with certain optimization flows (blockIndexes, skip_empty_output, etc..)
- See also the https://substreams.streamingfast.io/reference-and-specs/change-log for both Server and Client.
	- One new feature of the WASM machine is `skip_empty_output` which allows great performance improvements, when dealing with sparse data along the chain history. When you call this, it won't send blocks over the wire, if the module's output is an empty byte array. Combined with `blockIndex` modules introduced recently, the engine has multiplied by 10 the performances in some situations.
- We've pushed great performance improvements for the Solana Foundational Modules (like 4-8x perfs inc.), and recached those modules, so that you don't have to pay for it.

## Looking ahead

- We're heads down for the last few weeks of the quarter, to achieve our goals (as stated [last month](https://forum.thegraph.com/t/streamingfast-july-2024-update/5936)) to:
	- provide an extraordinary onboarding experience for new developers,
	- on all chains supported, 
	- with a variety of code-generation templates, 
	- provide quality Foundational Modules for all layer 1s we support
	- provide a pristine Substreams-powered subgraph experience
- Please reach out if you can help us reach those goals.
	- We'll be very interested in the next few days, to have you guys try the [onboarding](https://github.com/streamingfast/substreams-starter) flow and experience, and give us your feedback.
	- Try it down to `substreams codegen subgraph`, and tell us what you think, what's missing, what's still heavy.
- We want to see massive growth of Substreams-powered subgraphs on the Network, as soon as possible. That's our goal!

Thanks all of you for your continuous enthusiasm and support for what we're doing!

-------------------------

