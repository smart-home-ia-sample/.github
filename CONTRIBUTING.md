# Contributing to Smart Home AI

Thanks for your interest! This is a portfolio / reference project, so the bar is
"clear, tested, and consistent with the architecture" rather than feature volume.

## Where things live

Each service is its own repo; the full stack, architecture docs, design specs and
end-to-end tests live in [`sh-infra`](https://github.com/smart-home-ia-sample/sh-infra).
Open issues and PRs in the repo that owns the code you're changing. Cross-cutting
or architectural proposals go to `sh-infra`.

## Getting set up

```sh
git clone https://github.com/smart-home-ia-sample/sh-infra && cd sh-infra
./bootstrap.sh     # clones every sh-* repo as a sibling
docker compose -f docker-compose.yml -f docker-compose.build.yml up --build -d
```

Per-repo test and build commands are in each repo's README (Python services:
`pip install -r requirements-dev.txt && pytest`).

## Making a change

1. **Open an issue first** for anything bigger than a small fix, so the approach
   can be agreed before you write code. Significant design changes should come
   with (or update) a spec in `sh-infra/spec/`.
2. Branch from `main`, keep the PR focused on one change.
3. **Add or update tests.** CI enforces a coverage floor (`fail_under` in
   `pyproject.toml`) — a PR that drops below it fails.
4. Keep CI green: tests, CodeQL and the image build all run on every PR.
5. If you change a contract between services (A2A skills, MCP tools, MQTT topics,
   BFF API), update the consumers and the end-to-end suite in `sh-infra/e2e`.
6. Changes to `sh-common` are released as a new `vX.Y.Z` tag; consumers then bump
   their pinned ref.

## Commit messages

Short imperative subject line (`Add energy threshold to identify_critical_devices`),
with a body explaining *why* when it isn't obvious.

## Security issues

Please **don't** open a public issue — see [SECURITY.md](SECURITY.md).

## License

By contributing, you agree that your contributions are licensed under the
[MIT License](LICENSE).
