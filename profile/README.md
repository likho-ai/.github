# Likho

**Likho** (लिखो, "write it down") turns Hindi, Urdu and English call recordings into text a
team can read, search and correct. Every line is kept twice: in the script that was spoken,
and in Hinglish.

Documentation: **https://likho-ai.github.io/likho-docs/**

## Repositories

| Repository | What it is | State |
| --- | --- | --- |
| [likho-infra](https://github.com/likho-ai/likho-infra) | The local stack (PostgreSQL, MongoDB, Redis, NATS JetStream, S3 store, Meilisearch, gateway) and the shared CI workflows | working |
| [likho-contracts](https://github.com/likho-ai/likho-contracts) | gRPC definitions, event schemas, NATS stream layout; Python, Go and TypeScript packages | v0.5.0 |
| [likho-language](https://github.com/likho-ai/likho-language) | Hinglish transliteration, spelling table, glossary and language policy (gRPC, Python) | v0.1 |
| [likho-media](https://github.com/likho-ai/likho-media) | Uploads, waveforms, playable audio and signed links (Go, FFmpeg) | v0.1 |
| [likho-transcription](https://github.com/likho-ai/likho-transcription) | The speech engine and the transcription service: a recording becomes a two-layer transcript (Python, faster-whisper) | v0.1 |
| [likho-api](https://github.com/likho-ai/likho-api) | Sign-in, workspaces, recordings, jobs and live lines; GraphQL for the web apps, REST for scripts (NestJS) | v0.1 |
| [likho-web-sdk](https://github.com/likho-ai/likho-web-sdk) | Typed GraphQL client and React hooks for likho-api | v0.1 |
| [likho-web-shell](https://github.com/likho-ai/likho-web-shell) | The web app: sign-in, navigation, theme, home, vocabulary, settings; loads the apps (React, Vite, Module Federation) | v0.1 |
| [likho-mfe-library](https://github.com/likho-ai/likho-mfe-library) | Recordings list, uploads, microphone recording | v0.1 |
| [likho-mfe-transcript](https://github.com/likho-ai/likho-mfe-transcript) | Player, both text layers, live lines, versions, downloads | v0.1 |
| [likho-ui](https://github.com/likho-ai/likho-ui) | Design system: colour tokens for light and dark, shared React components | v0.1 |
| [likho-docs](https://github.com/likho-ai/likho-docs) | The documentation site | live |
| likho-search | Search across every line of every call | next |
| likho-deploy, likho-connector-ameyo, likho-search | Kubernetes and the environments, the dialer connector, search | next |

## How to start

1. Clone `likho-infra` and run `.\stack.ps1 up` (Docker Desktop must be running), then `.\stack.ps1 smoke`.
2. Read the documentation, starting with Introduction.
3. Every repository has a README that says how to run it alone.
