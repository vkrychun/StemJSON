# StemJSON

*A Declarative JSON DSL for Native UI/UX — authored by humans or AI, delivered bundled or backend-driven, scaling from a single screen to complete flows.*

---

StemJSON, originated and authored by **Vasyl Krychun**, is a declarative language expressed in plain JSON. A StemJSON payload describes screens, UI trees, reactive state, and interaction flows; a runtime validates it, parses it into a component tree, and renders it as a native UI on the target platform. Payloads can be authored by developers or AI systems and delivered either bundled in an app or from a backend at runtime.

This repository hosts the normative specification, trademark policy, and brand assets. The language is licensed under the **Open Web Foundation Agreement 1.0 (OWFa 1.0)** — anyone may implement it in any language or on any platform, subject to the attribution requirement in [LICENSE §1.5](LICENSE).

---

## Specification

| Edition | File | Use |
|---|---|---|
| Full specification (human-readable) | [`spec/v1.1.md`](spec/v1.1.md) | The authoritative normative document — prose, rationale, and worked examples. |
| LLM reference (condensed) | [`spec/v1.1-ai.md`](spec/v1.1-ai.md) | Same normative surface, optimised for AI prompt use. Load this when instructing a language model to generate StemJSON. |

Both editions cover the same v1.1 normative language. The LLM edition is token-optimised — no prose, just the schemas, enums, and grammar tables a model needs to emit valid StemJSON.

Previous revisions remain available in [`spec/`](spec/): [`v1.0.md`](spec/v1.0.md) · [`v1.0-ai.md`](spec/v1.0-ai.md).

---

## Implementations

| Platform | Repository | Status |
|---|---|---|
| Apple (iOS, iPadOS) | [stem-runtime-swift](https://github.com/vkrychun/stem-runtime-swift) | Official. Native SwiftUI renderer. Swift Package (binary XCFramework). Proprietary SDK (separate license). |
| Android | [stem-runtime-kotlin](https://github.com/vkrychun/stem-runtime-kotlin) | Official. Native Jetpack Compose renderer. Gradle/Maven AAR — `com.stemjson:stem-runtime-sdk`, Android 7.0 (API 24)+. Proprietary SDK (separate license). |

Both official runtimes implement the v1.1 normative language. The built-in set of repository and service kinds is runtime-specific — see §5.3 and §5.5 of the spec, and each runtime's README for what it ships versus what the host application registers.

Reference demos — runnable apps whose features are authored in StemJSON and rendered via StemRuntimeSDK:

| Platform | Repository |
|---|---|
| iOS | [stem-examples-swift](https://github.com/vkrychun/stem-examples-swift) — SwiftUI and UIKit hosts, plus a mixed native/StemJSON screen with bidirectional state. |
| Android | [stem-examples-kotlin](https://github.com/vkrychun/stem-examples-kotlin) — Jetpack Compose hosts, plus a mixed native/StemJSON screen with bidirectional state. |

Independent implementations on other platforms are permitted under OWFa 1.0.

---

## MCP server

A hosted MCP server lets any MCP client — Claude Code, Claude, ChatGPT, Cursor — author StemJSON from chat: scaffold, spec lookup, validation, and submission that returns a share link opening natively on a phone. Free with your existing AI subscription; GitHub sign-in, no API key.

```bash
claude mcp add --transport http stemjson https://stem-cloud-api-183076946186.europe-west1.run.app/mcp
```

Setup for other clients: [stemjson.com/mcp](https://stemjson.com/mcp/)

---

## Support and feedback

| For | Channel |
|---|---|
| Spec clarifications (ambiguous wording, apparent contradictions) | Issues → *Spec clarification* template |
| Improvement suggestions for v1.1+ | Discussions → *Proposals*, or Issues → *Improvement suggestion* |
| Typos / editorial fixes | Issues → *Typo* template |
| Questions about the spec | Discussions → Q&A |
| Licensing, commercial enquiries, trademark permission | vkrychun@stemjson.com |

---

## License

The specification documents in [`spec/`](spec/) are licensed under the [Open Web Foundation Agreement 1.0 (OWFa 1.0)](http://www.openwebfoundation.org/legal/the-owf-1-0-agreements/owfa-1-0). See [LICENSE](LICENSE) for the full terms and [NOTICE](NOTICE) for attribution requirements.

You MAY freely implement the StemJSON specification in any programming language, on any platform, for any purpose (commercial or non-commercial).

You MUST include the following attribution in a reasonably discoverable location within any product that implements the specification (e.g., README, about screen, third-party notices):

> *"StemJSON specification created by Vasyl Krychun — https://stemjson.com"*

The **StemRuntimeSDK** is a separate product distributed under its own proprietary End-User License Agreement. See [https://stemjson.com/stemruntime/license/](https://stemjson.com/stemruntime/license/) and the [stem-runtime-swift](https://github.com/vkrychun/stem-runtime-swift) / [stem-runtime-kotlin](https://github.com/vkrychun/stem-runtime-kotlin) repositories for details.

---

## Trademarks

"StemJSON", "StemRuntimeSDK", "StemRuntime", and the StemJSON logo are trademarks of Vasyl Krychun. The OWFa 1.0 license on the specification does not grant rights to use these marks. See [TRADEMARK_POLICY.md](TRADEMARK_POLICY.md) for permitted uses, restrictions, and how to request a trademark licence.

---

## Contact

- **Specification author:** Vasyl Krychun
- **Email:** vkrychun@stemjson.com
- **Website:** https://stemjson.com
