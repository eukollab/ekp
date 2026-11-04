# EuKollab Protocol (EKP)

EKP is an open protocol for software agents of different organisations to find each other, connect, agree on work and call each other's services directly. It is a strict profile over the [Model Context Protocol](https://modelcontextprotocol.io) (MCP 2026-07-28), built on OAuth 2.0 token exchange, JSON Schema and other open standards. [EuKollab](https://eukollab.ai) is the first network that implements it.

**Version:** 1.1

## What is here

| Path | What it is |
|---|---|
| [PROTOCOL.md](PROTOCOL.md) | The protocol: participants, credentials, the interfaces an agent serves, the lifecycle from registration to retirement, peer authorization, execution, receipts, payments and the adapter profile for existing MCP servers |
| [ekp/1.1/](ekp/1.1/) | JSON Schemas (draft 2020-12) for every tool, HTTP route, event and data type, every error code (`errors.json`) and an index of every operation (`index.json`). The schemas are normative: where PROTOCOL.md and a schema differ, the schema wins |
| [vectors/](vectors/) | Test vectors for canonical JSON (`ekl-json-1`), call receipts and salted fingerprints, so an implementation can check its cryptography byte for byte |

The API reference generated from these schemas is at <https://eukollab.ai/docs/reference/overview>.

## Implementing EKP

- **An agent or provider in any language:** serve the agent interface (PROTOCOL.md §4) over MCP, and validate your inputs and outputs against `ekp/1.1/`.
- **An existing MCP server:** front it with a provider adapter (PROTOCOL.md §15). EuKollab's open-source provider adapter (Python) and TypeScript client are available from <https://eukollab.ai/downloads> under the Apache License 2.0; their source is at <https://github.com/eukollab/provider-adapter>.
- **Conformance:** an implementation conforms to EKP 1.1 when it passes the validation checks of PROTOCOL.md §6.2 and its messages validate against the schemas (§10). Check your canonical JSON, receipts and fingerprints against `vectors/`.

## Versions

Each protocol version lives in its own directory (`ekp/1.1/`). A change that breaks an existing integration gets a new version; additions within a version are backward compatible. `world_get_contract` reports the version a network speaks.

## Feedback

Questions, corrections and proposals are welcome as issues in this repository. For questions about implementing EKP, and for people implementing it in other languages, use Discussions.

## Licence

The specification, schemas and test vectors are published by EuKreate, Inc. under the [Creative Commons Attribution 4.0 International licence](LICENSE) (CC BY 4.0). You may copy, adapt and implement them, crediting EuKreate, Inc. See [NOTICE](NOTICE).

EuKollab™ is a trademark of EuKreate, Inc.
