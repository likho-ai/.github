# Likho

**Likho** (लिखो, "write it down") turns Hindi, Urdu and English call recordings into text a
team can read, search and correct. Every line is kept twice: in the script that was spoken,
and in Hinglish. On top of the transcripts: what a language model says about each call, and
the numbers behind the calls.

Documentation: **https://likho-ai.github.io/likho-docs/**

## What it does

A call arrives by upload, by script, or from the dialer. It is transcribed in Devanagari and
Hinglish, with the workspace's own spellings and glossary. People read it beside the player,
correct lines, search every word of every call, narrow by agent, campaign or disposition, and
keep searches for later. A model summarises the call, reads the customer's mood and pre-fills
the auditor's form (when the company allows transcript text to reach the model). The home page
shows yesterday in numbers; the Insights page the last two weeks. Another system can show a
call's transcript beside its own recording button through a short-lived token.

## Repositories

### Services

| Repository | What it is | Version |
| --- | --- | --- |
| [likho-contracts](https://github.com/likho-ai/likho-contracts) | gRPC definitions, event schemas, the NATS stream layout; Python, Go and TypeScript packages | v0.12.0 |
| [likho-api](https://github.com/likho-ai/likho-api) | Sign-in, people and roles, workspaces, recordings, jobs, live lines, search, imports, vocabulary, insights, analytics, tokens for other systems, the audit log; GraphQL for the web apps, REST for scripts (NestJS) | v0.10.0 |
| [likho-media](https://github.com/likho-ai/likho-media) | Uploads, waveforms, playable audio and signed links (Go, FFmpeg) | v0.2.0 |
| [likho-transcription](https://github.com/likho-ai/likho-transcription) | The speech engine and the transcription service: a recording becomes a two-layer transcript, corrected line by line (Python, faster-whisper) | v0.2.3 |
| [likho-language](https://github.com/likho-ai/likho-language) | Hinglish transliteration, the spelling table, the glossary and how often each entry is heard, the language policy (gRPC, Python) | v0.3.0 |
| [likho-search](https://github.com/likho-ai/likho-search) | Every line of every call in Meilisearch, searched with typo tolerance and narrowed by the facts of the call (Go) | v0.3.0 |
| [likho-insights](https://github.com/likho-ai/likho-insights) | What a language model says about a call: a summary, the products, the mood, the auditor's checks pre-filled; nothing leaves without a key (Python) | v0.1.0 |
| [likho-analytics](https://github.com/likho-ai/likho-analytics) | Every event in ClickHouse, and the numbers behind the calls: how many, how long, how fast, by whom, what the model made of them (Go) | v0.1.0 |
| [likho-connector-ameyo](https://github.com/likho-ai/likho-connector-ameyo) | The dialer connector: calls from Ameyo by schedule or by id into Likho, from the live server or the archive; transcripts back to the CRM (Node, TypeScript) | v0.3.0 |

### Web

| Repository | What it is | Version |
| --- | --- | --- |
| [likho-web-sdk](https://github.com/likho-ai/likho-web-sdk) | Typed GraphQL client and React hooks for likho-api, uploads, live updates | v0.9.0 |
| [likho-ui](https://github.com/likho-ai/likho-ui) | Design system: colour tokens for light and dark, shared React components | v0.1.0 |
| [likho-web-shell](https://github.com/likho-ai/likho-web-shell) | The web app: sign-in, navigation, theme, home with yesterday's numbers, search, settings; loads the apps at run time; the embed page for other systems (React, Vite, Module Federation) | main |
| [likho-mfe-library](https://github.com/likho-ai/likho-mfe-library) | Recordings: the list by the facts of a call, uploads, microphone recording, fetching a call from the dialer by its id | main |
| [likho-mfe-transcript](https://github.com/likho-ai/likho-mfe-transcript) | Player, both text layers, live lines, corrections, versions, downloads, the insights of the call; the embeddable transcript panel | main |
| [likho-mfe-vocabulary](https://github.com/likho-ai/likho-mfe-vocabulary) | The glossary and the spellings with how often each is heard; CSV in and out | main |
| [likho-mfe-insights](https://github.com/likho-ai/likho-mfe-insights) | The last two weeks in numbers and charts; the day's calls with what the model said about each | main |
| [likho-mfe-admin](https://github.com/likho-ai/likho-mfe-admin) | People and roles, invitations, API keys, workspace settings, the audit log | main |

### Running it

| Repository | What it is | State |
| --- | --- | --- |
| [likho-infra](https://github.com/likho-ai/likho-infra) | The local stack (PostgreSQL, MongoDB, Redis, NATS JetStream, S3 store, Meilisearch, ClickHouse, the gateway, Grafana) and the shared CI workflows | working |
| [likho-deploy](https://github.com/likho-ai/likho-deploy) | Likho in Kubernetes: Helm charts for the stack and the product, the environments, Skaffold (minikube locally) | working |
| [likho-docs](https://github.com/likho-ai/likho-docs) | The documentation site, with the roadmap | live |

## How to start

1. Clone `likho-infra` and run `.\stack.ps1 up` (Docker Desktop must be running), then `.\stack.ps1 smoke`.
2. Read the documentation, starting with Introduction; the Roadmap page says what is done and what comes next.
3. Every repository has a README that says how to run it alone and how to work on it.
