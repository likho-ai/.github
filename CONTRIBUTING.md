# Working in the Likho repositories

These rules apply to every repository in the organisation.

## Branches and pull requests

Every repository has three long-lived branches, and a change travels through them in order:

```
feat/… fix/… ──squash──▶ development ──merge──▶ staging ──merge──▶ main
                         (default)               (staging env)      (production, releases)
hotfix/… ────────────────────────────────────────────────────────▶ main ──back-merge──▶ development
```

| Branch | What it is | Into it come | Merge | Needs |
| --- | --- | --- | --- | --- |
| `development` | the default branch; where work lands | feature branches, back-merges from `main` | squash | CI green |
| `staging` | what the staging environment runs (`:staging` images) | `development`, `hotfix/…` | merge commit | CI green, 1 approval |
| `main` | production; releases are cut here (`:latest`, `:x.y.z`) | `staging`, `hotfix/…`, the release pull request | merge commit | CI green, 1 approval |

* Start every change from `development`: `git switch development && git pull && git switch -c feat/short-name`.
* Promote with a pull request `development → staging`, then `staging → main`. Never squash a
  promotion: the branches would drift apart.
* A fix production cannot wait for: `hotfix/short-name` from `main`, a pull request into `main`;
  after it merges, the back-merge pull request brings it into `development`.
* The `branch-flow` check fails a pull request that skips a stage (`development → main`, say).
* Nobody pushes to the three branches directly, and none of them can be force-pushed or deleted.
  A pull request into `staging` or `main` needs the approval of a code owner who is not its author;
  approvals are dismissed when new commits arrive, and every review conversation must be resolved.
  An admin may merge past the rules in an emergency, and only through a pull request.
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
* **Dependencies** are Renovate's (settings in this repository's `default.json`), into
  `development`: one pull request a week per repository for minor and patch updates, one per image
  and per major update, Likho's own packages at once, a Dependency Dashboard issue in each repository.
* **Security**: Dependabot opens a pull request into `development` as soon as a dependency has a
  published vulnerability (`fix(deps): …`, labelled `security`); CodeQL scans every pull request
  for security bugs; secret scanning with push protection refuses a push that contains a password,
  key or token - remove it from the commit, never bypass the block.
* **Checks on every pull request**: the branch flow and a Conventional Commit title; then the
  repository's CI - TypeScript: ESLint (oxlint in the NestJS services), Prettier, `tsc`, tests;
  Python: ruff, ruff format, mypy, pytest; Go: gofmt, go vet, golangci-lint, tests. Format before
  you push: `pnpm format`, `uv run ruff format .`, `gofmt -w .`.
* **Reviews**: `.github/CODEOWNERS` in each repository names who is asked.
* **Bot pull requests** (the release pull request into `main`, the back-merge into `development`)
  are opened with the workflow's own token, so CI does not run on them: an admin merges them past
  the check. They change only versions, changelogs and what `main` already has.
* **Images**: every push to `development`, `staging` or `main` publishes `ghcr.io/likho-ai/<repo>`
  tagged with the branch and `sha-<commit>`; `main` also `latest`, a release `x.y.z` and `x.y`.

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
