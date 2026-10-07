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

## Releases, dependencies, reviews

* **Releases** are release-please's: it keeps a pull request "chore(main): release x.y.z" open with
  the next version and the changelog, worked out from the commit titles since the last release
  (`fix:` a patch, `feat:` a minor, `feat!:` or a `BREAKING CHANGE:` footer a major; before 1.0 a
  breaking change is a minor). Merging it tags the version, makes the GitHub release and builds
  the image (`ghcr.io/likho-ai/<repo>:x.y.z`) or the package. Commits without a type are not in
  the changelog. likho-contracts is still tagged by hand (its Go module needs its own tag).
* **Dependencies** are Renovate's (settings in this repository's `default.json`): one pull request
  a week per repository for minor and patch updates, one per image and per major update, Likho's
  own packages at once, a Dependency Dashboard issue in each repository.
* **Reviews**: `.github/CODEOWNERS` in each repository names who is asked.
* **`main`** takes changes only through pull requests whose CI is green; no force pushes, no
  deletion. Release pull requests are opened by a bot, so CI does not run on them: an admin
  merges them past the check (they change only the version and the changelog).

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
