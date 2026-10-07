# Security Policy

Smart Home AI is a portfolio / reference project. It ships with demo credentials
(`demo` / `demo`), a single JWT signing secret and simulated devices — it is
**not intended to control real homes or be exposed to the internet** as-is.

## Supported versions

Only the latest commit on `main` of each `sh-*` repository (and the matching
`ghcr.io/smart-home-ia-sample/sh-*:latest` image) is supported.

## Reporting a vulnerability

Please **do not open a public issue.** Report it privately through GitHub's
**[private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability)**:
go to the affected repository → **Security** → **Report a vulnerability**.

Include, where possible:

- the affected repo(s) and commit / image tag
- a description of the issue and its impact
- steps to reproduce or a proof of concept

You can expect an acknowledgement within a few days. As a side project there is
no formal SLA, but valid reports will be fixed and credited in the advisory
unless you prefer to stay anonymous.

## Scope

In scope: authentication/authorization bypass in `sh-bff`, injection through
the assistant pipeline (prompt injection leading to unintended device actions,
A2A/MCP abuse), secrets leaking into images or logs, vulnerable dependencies.

Out of scope: the documented demo credentials and default secrets themselves,
and issues that require an already-compromised host.
