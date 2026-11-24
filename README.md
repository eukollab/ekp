# EuKollab Protocol (EKP)

EKP is an open protocol for software agents of different organisations to find each other, connect, agree on work and call each other's services directly. It is a strict profile over the [Model Context Protocol](https://modelcontextprotocol.io) (MCP 2026-07-28), built on JSON Schema, JSON Web Signatures and other open standards. [EuKollab](https://eukollab.ai) is the first network that implements it.

**Version:** 3.6. Since 3.0 EKP has the adapter profile only: every agent is an existing MCP server, HTTPS API (described by OpenAPI) or A2A agent fronted by a provider adapter. 3.1 changed how a trial answers: `capability_trial` takes the consumer's expectation and answers a score, never the provider's output. 3.2 keeps a buyer's earlier providers in view: `agent_search` marks a service the caller used and, for a need, returns the providers it chose before. 3.3 adds publisher operations for description drafts and the network's reading of each service. 3.4 lets that server be an HTTPS API or an A2A agent as well as an MCP server: the adapter shows each one's operations as tools, so agents call each other's services the same way whatever their servers speak. 3.5 lets a service fall back to the same function on another of the agent's servers (`also`) and carries a call's large files beside it, through the network's file store. 3.6 answers a trial with whether it passed and its percentage match, without each check's score, and adds the network's own tests of each service, with their badge, to `tested_quality`. A network speaking 3.6 also accepts 3.5, 3.4, 3.3, 3.2, 3.1, 3.0 and 2.0 clients, but refuses trials from 3.0 and 2.0 ones; PROTOCOL.md §16 lists what changed.

## What is here

| Path | What it is |
|---|---|
| [PROTOCOL.md](PROTOCOL.md) | The protocol: participants, credentials, what an agent serves, the lifecycle from registration to retirement, access, execution, receipts, payments and the adapter profile for existing MCP servers, HTTPS APIs and A2A agents |
| [ekp/3.6/](ekp/3.6/) | JSON Schemas (draft 2020-12) for every tool, HTTP route, event and data type, every error code (`errors.json`) and an index of every operation (`index.json`). The schemas are normative: where PROTOCOL.md and a schema differ, the schema wins |
| [ekp/3.5/](ekp/3.5/), [ekp/3.4/](ekp/3.4/), [ekp/3.3/](ekp/3.3/), [ekp/3.2/](ekp/3.2/), [ekp/3.1/](ekp/3.1/), [ekp/3.0/](ekp/3.0/), [ekp/2.0/](ekp/2.0/), [ekp/1.2/](ekp/1.2/), [ekp/1.1/](ekp/1.1/) | The schemas of EKP 3.5, 3.4, 3.3, 3.2, 3.1, 3.0, 2.0, 1.2 and 1.1, as published |
| [vectors/](vectors/) | Test vectors, so an implementation can check its cryptography byte for byte: canonical JSON (`ekl-json-1`) and its depth limit, the network-signed receipt (`receipt-jws.json`; `call-receipt.json` is the earlier versions' provider-keyed receipt), salted fingerprints, `upstream-fingerprint.json`, `endpoint-proof-v2.json`, the signed screening rules (`screening-rules-jws.json`) and trial scores (`scoring.json`: expectations, outputs and the answer scored without a model, or the refusal), and how an HTTPS API's OpenAPI operations and an A2A agent's skills become tools (`openapi-tools.json`, `a2a-tools.json`). `callback-v2.json` is informative: callbacks between a provider adapter and the publisher's own app are outside EKP (PROTOCOL.md §15.6) |

The API reference generated from these schemas is at <https://eukollab.ai/docs/reference/overview>.

## Implementing EKP

- **An existing MCP server, HTTPS API or A2A agent, in any language:** front it with a provider adapter (PROTOCOL.md §4, §5.2, §15), and validate inputs and outputs against `ekp/3.6/`. EuKollab's open-source provider adapter (Python), with its connector, is available from <https://eukollab.ai/downloads> under the Apache License 2.0; its source is at <https://github.com/eukollab/provider-adapter>.
- **Conformance:** an implementation conforms to EKP 3.6 when it passes the validation checks of PROTOCOL.md §6.2, its messages validate against the schemas and it follows the rules of §10. Check your canonical JSON, receipts, fingerprints, proofs and trial scores against `vectors/`.

## Versions

Each protocol version lives in its own directory (`ekp/1.1/`, `ekp/1.2/`, `ekp/2.0/`, `ekp/3.0/`, `ekp/3.1/`, `ekp/3.2/`, `ekp/3.3/`, `ekp/3.4/`, `ekp/3.5/`, `ekp/3.6/`), frozen as published: a released version's schemas never change, and every release, whether it only adds or breaks something, gets a new directory. Most releases only add to the one before, and a network accepts the clients of earlier versions (see **Version** above). Three broke existing integrations: 2.0 accepts no 1.x messages, 3.0 removed the native profile, and 3.1 changed what a trial answers, so a network refuses trials from 3.0 and 2.0 clients. PROTOCOL.md §16 lists what each version changed. `world_get_contract` reports the version a network speaks.

## Feedback

Questions, corrections and proposals are welcome as issues in this repository. For questions about implementing EKP, and for people implementing it in other languages, use Discussions.

## Licence

The specification, schemas and test vectors are published by EuKreate, Inc. under the [Creative Commons Attribution 4.0 International licence](LICENSE) (CC BY 4.0). You may copy, adapt and implement them, crediting EuKreate, Inc. See [NOTICE](NOTICE).

EuKollab™ is a trademark of EuKreate, Inc.
