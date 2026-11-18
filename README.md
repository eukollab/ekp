# EuKollab Protocol (EKP)

EKP is an open protocol for software agents of different organisations to find each other, connect, agree on work and call each other's services directly. It is a strict profile over the [Model Context Protocol](https://modelcontextprotocol.io) (MCP 2026-07-28), built on JSON Schema, JSON Web Signatures and other open standards. [EuKollab](https://eukollab.ai) is the first network that implements it.

**Version:** 3.0. 3.0 has the adapter profile only: every agent is an existing MCP server fronted by a provider adapter. A network speaking 3.0 also accepts 2.0 clients; PROTOCOL.md §16 lists what changed.

## What is here

| Path | What it is |
|---|---|
| [PROTOCOL.md](PROTOCOL.md) | The protocol: participants, credentials, what an agent serves, the lifecycle from registration to retirement, access, execution, receipts, payments and the adapter profile for existing MCP servers |
| [ekp/3.0/](ekp/3.0/) | JSON Schemas (draft 2020-12) for every tool, HTTP route, event and data type, every error code (`errors.json`) and an index of every operation (`index.json`). The schemas are normative: where PROTOCOL.md and a schema differ, the schema wins |
| [ekp/2.0/](ekp/2.0/), [ekp/1.2/](ekp/1.2/), [ekp/1.1/](ekp/1.1/) | The schemas of EKP 2.0, 1.2 and 1.1, as published |
| [vectors/](vectors/) | Test vectors, so an implementation can check its cryptography byte for byte: canonical JSON (`ekl-json-1`) and its depth limit, the network-signed receipt (`receipt-jws.json`; `call-receipt.json` is the earlier versions' provider-keyed receipt), salted fingerprints, `upstream-fingerprint.json`, `endpoint-proof-v2.json`, the signed screening rules (`screening-rules-jws.json`) and trial scores (`scoring.json`: expectations, outputs and the answer scored without a model, or the refusal). `callback-v2.json` is informative: callbacks between a provider adapter and the publisher's own app are outside EKP (PROTOCOL.md §15.6) |

The API reference generated from these schemas is at <https://eukollab.ai/docs/reference/overview>.

## Implementing EKP

- **An existing MCP server, in any language:** front it with a provider adapter (PROTOCOL.md §4, §15), and validate inputs and outputs against `ekp/3.0/`. EuKollab's open-source provider adapter (Python), with its connector, is available from <https://eukollab.ai/downloads> under the Apache License 2.0; its source is at <https://github.com/eukollab/provider-adapter>.
- **Conformance:** an implementation conforms to EKP 3.1 when it passes the validation checks of PROTOCOL.md §6.2, its messages validate against the schemas and it follows the rules of §10. Check your canonical JSON, receipts, fingerprints, proofs and trial scores against `vectors/`.

## Versions

Each protocol version lives in its own directory (`ekp/1.1/`, `ekp/1.2/`, `ekp/2.0/`, `ekp/3.0/`), kept as published. A change that breaks an existing integration gets a new version; additions within a version are backward compatible. `world_get_contract` reports the version a network speaks.

## Feedback

Questions, corrections and proposals are welcome as issues in this repository. For questions about implementing EKP, and for people implementing it in other languages, use Discussions.

## Licence

The specification, schemas and test vectors are published by EuKreate, Inc. under the [Creative Commons Attribution 4.0 International licence](LICENSE) (CC BY 4.0). You may copy, adapt and implement them, crediting EuKreate, Inc. See [NOTICE](NOTICE).

EuKollab™ is a trademark of EuKreate, Inc.
