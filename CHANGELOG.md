# Changelog

All notable changes to the StemJSON specification are recorded in this file.
Normative content for each release lives in [`spec/`](spec/).

This project follows [Semantic Versioning](https://semver.org/). For the
specification, `MAJOR.MINOR.PATCH` means: **MAJOR** — breaking changes to
the normative surface; **MINOR** — backwards-compatible additions;
**PATCH** — editorial fixes (typos, clarifications, non-normative rewording).

## [1.1.0] — 2026-07-02

Minor version: backwards-compatible language additions (`switch()`,
`random()` / `range()`, and the collection functions), plus editorial
clarifications. Modules targeting `1.0` are unaffected; a module that uses a
1.1 function SHOULD declare `"version": "1.1"`.

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
