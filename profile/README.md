# Likho

**Likho** (लिखो, "write it down") turns Hindi, Urdu and English call recordings into text a
team can read, search and correct. Every line is kept twice: in the script that was spoken,
and in Hinglish.

## Repositories

| Repository | What it is | State |
| --- | --- | --- |
| [likho-infra](https://github.com/likho-ai/likho-infra) | The local stack (PostgreSQL, MongoDB, Redis, NATS JetStream, S3 store, Meilisearch, gateway) and the shared CI workflows | working |
| [likho-contracts](https://github.com/likho-ai/likho-contracts) | gRPC definitions, event schemas, NATS stream layout | v0.1 |
| [likho-docs](https://github.com/likho-ai/likho-docs) | The documentation site | first pages |
| likho-transcription | The speech engine: chunking, language detection, both text layers | engine exists, service in Wave 1 |
| likho-language, likho-media, likho-api, likho-search | The other services | Wave 1 and 2 |
| likho-web-shell, likho-mfe-*, likho-ui, likho-web-sdk | The web app as micro-frontends | Wave 1 and 2 |

## How to start

1. Clone `likho-infra` and run `.\stack.ps1 up` (Docker Desktop must be running).
2. Read the docs site, starting with Introduction.
3. Every repository has a README that says how to run it alone.
