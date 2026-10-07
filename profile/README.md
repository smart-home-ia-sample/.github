# Smart Home AI 🏠🤖

> **Portfolio / reference project** — a working sample built to explore
> multi-agent architectures and open agent protocols. Not a production product.

A multi-agent smart-home assistant, built as a **polyglot, polyrepo** reference
architecture. Ask it in natural language — *"tranca tudo e desliga o que não
for necessário"* (commands are in Portuguese) — and a LangGraph orchestrator
discovers the right agents, dispatches the work over **A2A**, acts on devices
through **MCP**, and streams the result back to the browser over **AG-UI**.

<!-- TODO: add a screenshot or GIF of the Dashboard + assistant chat here, e.g.
<p align="center"><img src="./demo.gif" alt="Smart Home AI demo" width="800"></p>
-->

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./architecture-dark.png">
  <img src="./architecture-light.png" alt="Smart Home AI architecture: the browser talks to sh-bff, which proxies AG-UI to the LangGraph orchestrator; the orchestrator resolves agents via sh-bfa and calls the A2A agents, which act on devices through sh-mcp, the BFF and MQTT.">
</picture>

## Try it

```sh
git clone https://github.com/smart-home-ia-sample/sh-infra && cd sh-infra
docker compose up -d
# http://localhost:8080   (demo / demo)
```

**No API key needed.** By default (`LLM_PROVIDER=mock`) commands are
interpreted deterministically, without an LLM. For a real model, run one locally
with Ollama (`LLM_PROVIDER=ollama`, default `llama3.1:8b`, pulled automatically)
or use Gemini (`LLM_PROVIDER=google`).

Images are published to `ghcr.io/smart-home-ia-sample/sh-*` from each repo's CI.

## Repositories

| Repo | Stack | Role |
| --- | --- | --- |
| [**sh-infra**](https://github.com/smart-home-ia-sample/sh-infra) | Docker Compose | Start here — full stack, architecture, specs, end-to-end tests |
| [sh-frontend](https://github.com/smart-home-ia-sample/sh-frontend) | React 19 + Vite | Dashboard + AG-UI assistant chat |
| [sh-bff](https://github.com/smart-home-ia-sample/sh-bff) | Java / Spring Boot | Edge gateway: SPA, JWT auth, home/device persistence, MQTT read-model, proxy to the AI layer |
| [sh-orchestrator](https://github.com/smart-home-ia-sample/sh-orchestrator) | Python / LangGraph | Interpret → discover → dispatch (A2A) → validate → stream AG-UI |
| [sh-bfa](https://github.com/smart-home-ia-sample/sh-bfa) | Python / FastAPI | Backend-for-Agents: stateless capability catalog + BM25 semantic resolver |
| [sh-agent-security](https://github.com/smart-home-ia-sample/sh-agent-security) | Python / A2A | Locks, alarm, `secure_home` |
| [sh-agent-environment](https://github.com/smart-home-ia-sample/sh-agent-environment) | Python / A2A | Lights, climate, blinds, `switch_off_nonessential` |
| [sh-agent-energy](https://github.com/smart-home-ia-sample/sh-agent-energy) | Python / A2A | Consumption analysis, critical devices |
| [sh-mcp](https://github.com/smart-home-ia-sample/sh-mcp) | Python / MCP | Generic device-verb tools + `home://*` resources over the BFF |
| [sh-device-sim](https://github.com/smart-home-ia-sample/sh-device-sim) | Python / MQTT | Simulated devices that self-announce their capabilities |
| [sh-common](https://github.com/smart-home-ia-sample/sh-common) | Python lib | Shared logging, tracing, auth, A2A and MCP clients |

## Documentation

- [Architecture overview](https://github.com/smart-home-ia-sample/sh-infra/blob/main/ARCHITECTURE.md)
- [Design specs](https://github.com/smart-home-ia-sample/sh-infra/tree/main/spec) — 14 numbered specs, from requirements to catalog-first discovery
- [Architecture & testing notes](https://github.com/smart-home-ia-sample/sh-infra/tree/main/docs)

## Highlights

- **Open agent protocols end to end** — A2A between agents, MCP for tools, AG-UI to the browser.
- **Catalog-first discovery** — agents and tools are found by meaning, not hard-coded routes.
- **Self-describing devices** — each device announces what it can do over MQTT; the system adapts.
- **Independent repos, one stack** — every service has its own CI (tests + coverage gate, CodeQL, image publish).

## Contributing

Issues and pull requests are welcome — see the
[contributing guide](https://github.com/smart-home-ia-sample/.github/blob/main/CONTRIBUTING.md)
and the [security policy](https://github.com/smart-home-ia-sample/.github/blob/main/SECURITY.md).

---

Released under the [MIT License](https://github.com/smart-home-ia-sample/.github/blob/main/LICENSE).
