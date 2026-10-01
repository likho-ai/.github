# Working in the Likho repositories

These rules apply to every repository in the organisation.

## Branches and pull requests

* `main` is always releasable. Work on a branch (`feat/short-name`, `fix/short-name`) and open
  a pull request. A pull request is merged when CI is green.
* Keep a pull request to one change. If the description needs the word "and", split it.

## Commit messages

[Conventional Commits](https://www.conventionalcommits.org): `feat: …`, `fix: …`, `docs: …`,
`refactor: …`, `test: …`, `chore: …`. The first line says what changed for the user of the
code; the body says why. Versions and changelogs are generated from these messages.

## Interfaces

* A gRPC service, an event or a REST path is changed in `likho-contracts` first, then in the
  service. Released fields are never removed or renumbered.
* A service reads only its own database. To get another service's data, call it or listen to
  its events.

## Every service

* Configuration comes from environment variables; `.env.example` lists them all.
* `GET /healthz` (alive), `GET /readyz` (its dependencies answer), `GET /metrics`.
* Logs are JSON, one line per event, with the request or trace id.
* A README that says what the service does and how to run it alone.

## Secrets and data

* No password, key, token or connection string in git, in a Postman file or in the docs.
  `.env` files are never committed.
* These repositories are public. Nothing about a customer's systems, call volumes, people or
  recordings goes into code, tests, screenshots or documentation. Test audio and sample text
  are invented.
* Phone numbers are masked wherever they are shown or logged.
