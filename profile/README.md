# Likho

**Likho** (लिखो, "write it down") turns Hindi, Urdu and English call recordings into text a
team can read, search and correct. Every line is kept twice: in the script that was spoken,
and in Hinglish.

Documentation: **https://likho-ai.github.io/likho-docs/**

## Repositories

| Repository | What it is | State |
| --- | --- | --- |
| [likho-infra](https://github.com/likho-ai/likho-infra) | The local stack (PostgreSQL, MongoDB, Redis, NATS JetStream, S3 store, Meilisearch, gateway) and the shared CI workflows | working |
| [likho-contracts](https://github.com/likho-ai/likho-contracts) | gRPC definitions, event schemas, NATS stream layout; Python package | v0.1.0 |
| [likho-language](https://github.com/likho-ai/likho-language) | Hinglish transliteration, spelling table, glossary and language policy (gRPC, Python) | v0.1 |
| [likho-ui](https://github.com/likho-ai/likho-ui) | Design system: colour tokens for light and dark, shared React components | v0.1 |
| [likho-docs](https://github.com/likho-ai/likho-docs) | The documentation site | live |
| likho-transcription, likho-media, likho-api, likho-search | The speech engine and the other services | next |
| likho-web-shell, likho-mfe-*, likho-web-sdk | The web app as micro-frontends | next |

## How to start

1. Clone `likho-infra` and run `.\stack.ps1 up` (Docker Desktop must be running), then `.\stack.ps1 smoke`.
2. Read the documentation, starting with Introduction.
3. Every repository has a README that says how to run it alone.
