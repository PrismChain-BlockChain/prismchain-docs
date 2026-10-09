
# Rainbow Ring — Sepolia Native ETH Execution Experiment

**Status:** Executed successfully on Ethereum Sepolia testnet
**Purpose:** Document a bounded, independently verifiable native ETH execution experiment.

## 1. Objective

This experiment evaluates a prototype Ethereum Native Conduit that accepts test ETH, executes an intent-bound native ETH transfer, emits an execution event, and records the intent as executed.

This is an implementation experiment, not a claim that the complete PrismChain or Rainbow Ring architecture has been implemented, independently audited, or production-certified.

## 2. Network and Deployment

* **Network:** Ethereum Sepolia
* **Chain ID:** `11155111`
* **Conduit address:** `0x0298252Ff65Ed6087c6cC7122Ca0f7ae4448953A`
* **Deployment transaction:** `0x206cd87cc9959fb4bfaf7f917a0ba63f011a10d9112a6f36d342c9b75d3cd020`
* **Deployment block:** `11874727`
* **Deployment receipt:** Successful
* **Runtime bytecode:** Confirmed present by an RPC code query

## 3. Experiment Transactions

### Funding

* **Transaction:** `0x07635481829122bbe691d0847d089b850b16df8cc31582c45afd429e4e6e5b7d`
* **Block:** `11874728`
* **Value:** `0.001 ETH`
* **Receipt:** Successful

### Intent-bound execution

* **Transaction:** `0xb5aeba33813a99df00f55ca906afc3c2878a291d8210d62120fa2cdd4763fb06`
* **Block:** `11874729`
* **Value transferred:** `0.001 ETH`
* **Gas used:** `151260`
* **Receipt:** Successful

The recipient was the same wallet that deployed the conduit. This was a round-trip test, not a payment to an independent recipient.

## 4. Execution Evidence

The execution transaction emitted `NativeEthTransferred` with the following values:

* **Intent commitment:** `0x399ab7f0912cddba9fdaf8db585c224dff62e3da5d51574ae163243e21767de1`
* **White Light Block ID:** `0x45e593f3f777201de30825b648637ac23e7107d246a4da16953ba7af5a9695ad`
* **Recipient:** `0x83Eaa81792cE364bA765002494B6Ed33aD098614`
* **Amount:** `1000000000000000 wei` (`0.001 ETH`)

These values identify the event recorded by the deployed prototype. Their presence does not independently establish the correctness of the upstream PrismChain computation or the full authorization architecture.

## 5. Post-Execution Checks

After execution, read-only RPC calls returned:

| Check                         | Observed result                                                      |
| ----------------------------- | -------------------------------------------------------------------- |
| Conduit owner                 | `0x83Eaa81792cE364bA765002494B6Ed33aD098614`                         |
| Conduit chain identifier      | `0xf9b1779dd736d62f9a5815f9f11cb752f6342e8584a01f22e1b19b9a8cb5694e` |
| Executed intent mapping       | `true`                                                               |
| Remaining conduit ETH balance | `0 ETH`                                                              |

The transaction receipts reported status `1` for deployment, funding, and execution.

## 6. Independent Verification

An independent reviewer can use a Sepolia-compatible Ethereum RPC endpoint or the public Sepolia explorer to inspect the contract and transaction receipts.

* [View deployed contract on Sepolia Etherscan](https://sepolia.etherscan.io/address/0x0298252Ff65Ed6087c6cC7122Ca0f7ae4448953A)
* [Inspect deployment transaction](https://sepolia.etherscan.io/tx/0x206cd87cc9959fb4bfaf7f917a0ba63f011a10d9112a6f36d342c9b75d3cd020)
* [Inspect funding transaction](https://sepolia.etherscan.io/tx/0x07635481829122bbe691d0847d089b850b16df8cc31582c45afd429e4e6e5b7d)
* [Inspect execution transaction and event](https://sepolia.etherscan.io/tx/0xb5aeba33813a99df00f55ca906afc3c2878a291d8210d62120fa2cdd4763fb06)

Explorer links provide public chain evidence; they do not constitute a source-code audit. Source verification on the explorer has not been asserted here.

## 7. Scope and Limitations

This prototype is owner-controlled and intended for testnet experimentation.

* Execution requires the conduit owner.
* The legacy execution interface cannot authorize a transfer and reverts.
* The tested intent includes operation, target, value, deadline, output commitment, and replay protection.
* The current prototype is not yet integrated with the complete Ethereum execution gate, authorization decision/state registry, and replay registry architecture.
* The `gasConstraints` and `executionConstraints` fields are included in the intent commitment but are not enforced as execution policies by this prototype.
* The experiment does not establish resistance to all adversarial conditions, independent audit findings, or production readiness.
* Sepolia ETH is testnet currency and has no intended mainnet monetary value.

## 8. Disclosure Boundary

This report publishes reproducible transaction identifiers and observed results. It intentionally excludes internal Solidity source, private deployment configuration, secrets, unpublished research, and internal build artifacts.

The deployed contract's bytecode is public and may be inspected or analyzed independently. This report does not claim that deployed implementation details are secret.

## 9. Result

The recorded Sepolia experiment demonstrates a successful deployment, funding transaction, intent-bound native ETH transfer, execution event, and post-execution replay-state check for this specific prototype.

It is a bounded experimental milestone toward the broader PrismChain and Rainbow Ring design, not evidence that the entire architecture is complete or audited.
