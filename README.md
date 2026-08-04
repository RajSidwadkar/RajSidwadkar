<div align="center">

<br>

# Raj Kumar Sidwadkar

<img src="https://img.shields.io/badge/Software_Engineer-000000?style=flat-square" alt="Software Engineer" />

B.Tech CSE. Two backend focused internships. Currently building agent protocols and local first systems, and reading source code of the ones I admire.

<br>

<a href="https://github.com/RajSidwadkar"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" /></a>
<a href="https://www.linkedin.com/in/rajsidwadkar/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
<a href="https://leetcode.com/u/RajSIDS"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=flat-square&logo=leetcode&logoColor=black" alt="LeetCode" /></a>
<a href="mailto:rajsidwadkar777@gmail.com"><img src="https://img.shields.io/badge/Email-000000?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>

<br>

</div>

---

### Current focus

- Building local first systems that stay useful when a vendor's cloud does not
- Designing wire protocols where security is enforced structurally, not by convention
- Writing developer tools that solve one problem completely instead of many problems partially
- Working through distributed systems and applied cryptography, one primitive at a time
- Following the practical side of autonomous agent research, past the hype cycle

---

### Projects

Three repositories. Each one makes a specific engineering argument, which is why nothing else from the profile is featured here.

<br>

<table>
<tr>
<td width="100%">

**UAP Protocol** &nbsp; <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" height="18"/> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" height="18"/> <img src="https://img.shields.io/badge/Ed25519-000000?style=flat-square" height="18"/>

A security first wire protocol for AI tool access, built to close three specific holes left open by existing agent protocols: tool metadata that can be mutated after publication, tool execution with no sandbox boundary, and a server that acts as both resource server and authorization server for itself.

Each hole gets a structural fix rather than a configuration flag. Tool metadata is signed with Ed25519 inside the payload it describes, so any edit after signing breaks the signature before the gateway acts on it. Every tool call runs inside a fresh Docker container, read only root filesystem, capabilities dropped, memory capped, destroyed on response. Authorization is delegated entirely to an external identity provider with short lived, hard capped tokens, so the gateway is never both judge and party to the request.

<details>
<summary><b>Architecture and design decisions</b></summary>
<br>

The codebase is organized as hexagonal layers. The domain layer, `UapEnvelope`, `CapabilityCard`, `AuditEvent`, depends on nothing but the standard library. Application use cases depend only on domain ports. Infrastructure adapters, Keycloak, Docker, Ed25519, Pino, implement those ports and nothing else touches them directly. Swapping Docker for a WASM sandbox or Keycloak for Auth0 is an infrastructure change with zero domain impact.

Every request passes through an eight stage pipeline: frame parse, schema validation against AJV, token verification against a remote JWKS with a fifteen minute hard cap, scope enforcement, capability card signature check, sandboxed execution, non blocking audit emission, response envelope. Distributed tracing follows the W3C TraceContext standard end to end.

[Repository](https://github.com/RajSidwadkar/UAP-protocol)

</details>

</td>
</tr>
</table>

<br>

<table>
<tr>
<td width="100%">

**Vadjanix** &nbsp; <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" height="18"/> <img src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white" height="18"/> <img src="https://img.shields.io/badge/Nostr-8E44AD?style=flat-square" height="18"/>

A local first, multi agent orchestrator with no cloud dependency. Every incoming message is parsed into one typed structure, an `IntentPacket`, and routed by a fifty line prefix switcher to a typed handler: another agent, a database, a local file, a REST endpoint. No LLM sits in the routing path.

Before any model call happens, a deterministic pre-check gate evaluates the request against plain Markdown rule files, so hard constraints are enforced in code rather than left to model judgment. Agent identity and inter agent communication run over Nostr, giving each agent a cryptographic identity with no central server in the loop.

<details>
<summary><b>Architecture and design decisions</b></summary>
<br>

The system has no database. Memory is a set of append only Markdown files, profile, negotiation history, deal outcomes, a full reasoning audit trail, which keeps every decision the agent has made auditable in plain text by a human, not just by another model. For complex tasks the engine fans out to parallel specialist sub agents and aggregates their output with one of three explicit strategies, first response wins, consensus, or merge, rather than picking a default and hoping.

[Repository](https://github.com/RajSidwadkar/Vadjanix)

</details>

</td>
</tr>
</table>

<br>

<table>
<tr>
<td width="100%">

**slopcheck** &nbsp; <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" height="18"/> <img src="https://img.shields.io/badge/PyPI-3775A9?style=flat-square&logo=pypi&logoColor=white" height="18"/> <img src="https://img.shields.io/badge/stdlib_only-000000?style=flat-square" height="18"/>

An offline, zero dependency detector for AI generated prose. It scores text with five independent heuristics instead of a model: a weighted phrase bank, sentence length variance, punctuation frequency, paragraph uniformity, and lexical diversity by type token ratio.

Runs entirely on CPU, no network call, no external dependency, which makes it usable as a pre-commit hook or a CI gate without adding latency or a point of failure it doesn't control.

<details>
<summary><b>Under the hood</b></summary>
<br>

```
slopcheck/
├── cli.py            argument parsing and runner
├── scorer.py          orchestrates all five signals
├── render.py            console and JSON formatting
└── signals/
    ├── phrases.py          AI cliche matcher
    ├── rhythm.py             sentence length variance
    ├── punctuation.py          em dash and colon frequency
    ├── structure.py             paragraph uniformity
    └── lexical.py                type token ratio scorer
```

Published to PyPI as `slopcheck-cli`, MIT licensed, with tagged releases.

[Repository](https://github.com/RajSidwadkar/slopcheck) &nbsp;·&nbsp; [Package](https://pypi.org/project/slopcheck-cli/)

</details>

</td>
</tr>
</table>

---

### Open source

Contributor at Picnic Technologies, working through pull requests reviewed and merged by their engineering team. The value of that process was less about the code itself and more about watching how a team with real production constraints pushes back on a change before accepting it.

---

### Engineering interests

<div align="center">

`Protocol design` `Distributed systems` `Applied cryptography` `Developer tooling` `Local first software` `Autonomous agents and AGI research`

</div>

---

### Technologies

<div align="center">
<br>
<img src="https://skillicons.dev/icons?i=ts,py,js,nodejs,fastify,docker,redis,git,github,githubactions&theme=dark" alt="Technology icons" />
<br><br>
</div>

`TypeScript` `Python` `JavaScript` `Node.js` `Fastify` `Docker` `Redis` `Nostr` `OpenTelemetry` `Ed25519` `JWT` `OAuth 2.1` `mTLS` `Zod` `AJV` `Pino` `Git` `GitHub Actions`



---

### Reading

*Designing Data-Intensive Applications*, Martin Kleppmann
*Database Internals*, Alex Petrov

---

<div align="center">

Raj Kumar Sidwadkar &nbsp;·&nbsp; India &nbsp;·&nbsp; <a href="mailto:rajsidwadkar777@gmail.com">rajsidwadkar777@gmail.com</a>

</div>
