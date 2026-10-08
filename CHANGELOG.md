# Changelog

All notable changes to the StemJSON specification are recorded in this file.
Normative content for each release lives in [`spec/`](spec/).

This project follows [Semantic Versioning](https://semver.org/). For the
specification, `MAJOR.MINOR.PATCH` means: **MAJOR** — breaking changes to
the normative surface; **MINOR** — backwards-compatible additions;
**PATCH** — editorial fixes (typos, clarifications, non-normative rewording).

## [1.2.0] — 2026-10-08

Minor version: backwards-compatible language additions, plus editorial
clarifications. Modules targeting `1.1` are unaffected; a module that uses a
1.2 feature SHOULD declare `"version": "1.2"`.

Added:

- **`slice()`, array `prefix()` / `suffix()`, and math functions** (§8.6) —
  `slice(array, start, end?)` returns the elements from `start` up to but not
  including `end` (negative indices count from the tail, out-of-range bounds are
  clamped), `prefix` / `suffix` on an array return its first / last `n`
  elements, and `pow(base, exponent)`, `sqrt(x)`, `log(x, base?)` (natural
  logarithm by default) return a double, or none for a non-numeric argument,
  an undefined result, or overflow. *(Runtime support lands in stem-runtime 1.2.0.)*

- **`onChange` with several observers** (§9.2) — an array of
  `{ "observed", "actions" }` objects registers one observer per element; an
  array of bare actions never fired and is now reported by validation, as is
  mixing the two shapes. *(Runtime support lands in stem-runtime 1.2.0.)*

- **`navigate` operation `open`** (§10.8) — hands `input.url` (`https://`,
  `http://`, `mailto:`, `tel:`) to the platform's default handler outside the
  module; `output.failure` fires when the URL is invalid or no handler exists,
  and no `navigation` ancestor is required. *(Runtime support lands in
  stem-runtime 1.2.0.)*

- **`chart` component** (§4.2, §7.28) — plots an array of dictionaries through
  one or more series (`bar`, `line`, `area`, `point`, `pie`) that name the `x`
  and `y` fields of each element; all series share axes whose type follows the
  data or an explicit `type`, `_xAxis` / `_yAxis` set title and bounds, and `style.chart` sets legend,
  grid lines, animation and palette. Chart chrome is platform-native.
  *(Runtime support lands in stem-runtime 1.2.0.)*

- **`web` component** (§4.2, §7.29) — embeds a web page from an `https://`,
  `http://` or `file://` source, with `_allowsNavigation` and `_scrollEnabled`
  on the context and `javaScript` in `style.web`. *(Runtime support lands in
  stem-runtime 1.2.0.)*

- **Forward-compatibility contract** (§18.2) — a runtime degrades every
  construct introduced by a later minor revision (a component type, an event
  name, an action kind, a `navigate` operation, an expression function, a
  dependency kind) to a non-blocking warning instead of
  failing validation or decoding: an unrecognised `navigate` operation completes
  through `output.failure`, an unrecognised function evaluates to none, an
  unrecognised component renders the placeholder with its `children`, and an
  unrecognised dependency kind is omitted with a warning. §18.1 adds that a
  host rendering modules from sources it does not control SHOULD compare the
  module's `version` with the runtime's supported revision before rendering.
  *(Runtime support lands in stem-runtime 1.2.0.)*
  Degraded rendering is documented as a safety net, not a compatibility promise: hosts SHOULD check `version` and refuse or warn (§18.1, §18.2).
  Runtimes SHOULD offer a strict mode that rejects higher-minor modules outright.

Changed:

- **`navigate` operation `push` runs `output.failure`** (§10.8) — when its
  source is missing or cannot be loaded as a module, no screen is pushed and
  `output.failure` fires. *(Runtime support lands in stem-runtime 1.2.0.)*

- **`image` `_placeholder`** (§4.2) — shown when the load fails; while the
  picture loads, the runtime shows its loading state. *(Runtime support lands
  in stem-runtime 1.2.0.)*

Clarified (editorial; runtime behavior unchanged):

- **Repository and service kinds are open** (§5.3, §5.5). A runtime resolves a
  kind against a host-populated registry; a listed kind means the language
  defines its contract, not that every runtime ships it. `firebase` and `ai`
  are not built into either official runtime — the `ai` kind is host-provided.
- **Storage partition** (§5.3). A host MAY pass a storage namespace when it
  validates a module; `local` and `secured` stores open inside it. Without one,
  stores are keyed by repository id alone and shared by every un-namespaced
  module, so hosts rendering more than one module SHOULD pass a stable
  namespace per module.
- **One list per enumeration** (§2, Appendix B). The glossary rows for
  Repository and Style now point at §5.3 and §7 instead of repeating the
  repository-kind and style-domain lists.
- **Conformance tables** (§17.1, §17.2). `interval` and `ai` are listed among
  the core action kinds; executing `ai` depends on a `remote` repository or a
  host-provided `ai` repository.
- **`dynamic` laziness** (§4.1, §4.6). A `dynamic` is rendered lazily only as a
  direct child of `list`, or of a `vstack` / `hstack` with `_lazy: true` that is
  itself a direct child of a same-axis `scroll`; any other placement — a plain
  stack, a `zstack`, a `conditional` between the container and the `dynamic` —
  instantiates every row eagerly, and a remote-fed collection MUST sit in a
  lazy placement.
- **`style.picker` and `style.datePicker` take a bare string** (§7.14, §7.20).
  Both runtimes read the enum value directly; the dictionary form shown for
  `datePicker` was never honoured.

## [1.1.0] — 2026-07-02

Minor version: backwards-compatible language additions (`switch()`,
`random()` / `range()`, the collection functions, and the `ai` action), plus
editorial clarifications. Modules targeting `1.0` are unaffected; a module
that uses a 1.1 feature SHOULD declare `"version": "1.1"`.

Added:

- **`switch()` expression function** (§8.6) — a flat multi-way conditional:
  `switch(test1, value1, test2, value2, …, default)`. Returns the value paired
  with the first truthy test, or the trailing default. Eliminates deeply nested
  ternaries for 3+-way logic, the dominant source of unbalanced-paren syntax
  errors in generated modules. *(Runtime support lands in stem-runtime 1.1.0.)*

- **`random()` and `range()` functions** (§8.6, §8.6.1) — `random()` → a double
  in `[0, 1)`, `random(min, max)` → an inclusive integer; `range(n)` / `range(start, end)`
  build an integer sequence. `range` pairs with `map` to generate structured data
  declaratively. `random` is nondeterministic and must be used in an action/lifecycle
  value, never a render binding. *(Runtime support lands in stem-runtime 1.1.0.)*

- **Collection functions** (§8.6) — positional array edits `setAt(arr, i, v)`,
  `removeAt(arr, i)`, `insertAt(arr, i, v)` (negative indices count from the tail;
  out-of-range returns the value unchanged), and dictionary utilities `keys(dict)`
  (ascending-sorted), `values(dict)` (key-aligned), `removeKey(dict, k)`. All return
  a new value. Positional array editing is the missing piece for piece-moving board
  games and index-addressed grids; appending and dict-merge already exist via `+`.
  *(Runtime support lands in stem-runtime 1.1.0.)*

- **`ai` action** (§10.11) — calls an AI provider and binds the result into the
  module, the foundation for AI-driven backends (a game opponent, summarization,
  on-the-fly data shaping). The action POSTs a literal provider request `body`
  through a host-registered `remote` repository and optionally unwraps the
  response (`responsePath` plus a default `parseJson` JSON-parse), so the chained
  `@{id}` is the clean answer. Provider-agnostic: the model, prompt, and response
  schema live in `body`; the API key is injected by the host repository's auth
  interceptor, never in JSON. *(Runtime support lands in stem-runtime 1.1.0.)*

Clarified (editorial; runtime behavior unchanged):

- **Chained ternaries take no parentheses** (§8.5). The ternary is
  right-associative with lowest precedence, so `a ? b : c ? d : e` chains
  natively. The parenthesized form `a ? b : (c ? d : e)` is equivalent but is
  the #1 cause of unbalanced-`)` errors; the spec now states the flat form is
  canonical.
- **`style.shape.stroke`** (§7.9): `content` accepts the same value forms as
  `fill` — including `{ "gradient": ... }` directly as the discriminator. The
  previous shorthand `{ content: { color } }` misled authors into nesting
  gradients inside `color`, which is invalid.

## [1.0.2] — 2026-06-12

Editorial clarification. No breaking changes; modules targeting `1.0` are unaffected.

- Component `type` is matched **case-insensitively**; the canonical form is lowercase (§3.2). Normalized the type catalogue accordingly (`gridRow` → `gridrow`, `roundedRectangle` → `roundedrectangle`) and stated the convention: component types are lowercase, style domains are camelCase.

## [1.0.1] — 2026-06-01

Editorial clarifications and one new appendix. No breaking changes; modules targeting `1.0` are unaffected.

- Clarified state propagation (a `state` action's write does not propagate through an action chain) and cross-module context inheritance.
- Clarified expression and date-casting rules; tightened the closed color list; added anti-pattern callouts.
- Documented the `photos.read` return contract (always an array) and the `map` position/region shape.
- Added Appendix C — common iOS/SwiftUI assumptions that do not hold in StemJSON.

## [1.0.0] — 2026-04-24

Initial release.
