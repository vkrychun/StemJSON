# StemJSON

*A Declarative JSON DSL for Native UI/UX — authored by humans or AI, delivered bundled or backend-driven, scaling from a single screen to complete flows.*

---

StemJSON, originated and authored by **Vasyl Krychun**, is a declarative language expressed in plain JSON. A StemJSON payload describes screens, UI trees, reactive state, and interaction flows; a runtime validates it, parses it into a component tree, and renders it as a native UI on the target platform. Payloads can be authored by developers or AI systems and delivered either bundled in an app or from a backend at runtime.

This repository hosts the normative specification, trademark policy, and brand assets. The language is licensed under the **Open Web Foundation Agreement 1.0 (OWFa 1.0)** — anyone may implement it in any language or on any platform, subject to the attribution requirement in [LICENSE §1.5](LICENSE).

---

## Specification

| Edition | File | Use |
|---|---|---|
| Full specification (human-readable) | [`spec/v1.0.md`](spec/v1.0.md) | The authoritative normative document — prose, rationale, and worked examples. |
| LLM reference (condensed) | [`spec/v1.0-ai.md`](spec/v1.0-ai.md) | Same normative surface, optimised for AI prompt use. Load this when instructing a language model to generate StemJSON. |

Both editions cover the same v1.0 normative language. The LLM edition is token-optimised — no prose, just the schemas, enums, and grammar tables a model needs to emit valid StemJSON.

---

## Implementations

| Platform | Repository | Status |
|---|---|---|
| Apple (iOS, iPadOS) | [stem-runtime-swift](https://github.com/vkrychun/stem-runtime-swift) | Official. Native SwiftUI renderer. Proprietary binary SDK (separate license). |

Reference demos: [stem-examples-swift](https://github.com/vkrychun/stem-examples-swift) — runnable iOS apps whose features are authored in StemJSON and rendered via StemRuntimeSDK.

Independent implementations on other platforms are permitted under OWFa 1.0.

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

The **StemRuntimeSDK** is a separate product distributed under its own proprietary End-User License Agreement. See [https://stemjson.com/sdk/license](https://stemjson.com/sdk/license) and the [stem-runtime-swift](https://github.com/vkrychun/stem-runtime-swift) repository for details.

---

## Trademarks

"StemJSON", "StemRuntimeSDK", "StemRuntime", and the StemJSON logo are trademarks of Vasyl Krychun. The OWFa 1.0 license on the specification does not grant rights to use these marks. See [TRADEMARK_POLICY.md](TRADEMARK_POLICY.md) for permitted uses, restrictions, and how to request a trademark licence.

---

## Contact

- **Specification author:** Vasyl Krychun
- **Email:** vkrychun@stemjson.com
- **Website:** https://stemjson.com
