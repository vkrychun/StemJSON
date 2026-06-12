# Changelog

All notable changes to the StemJSON specification are recorded in this file.
Normative content for each release lives in [`spec/`](spec/).

This project follows [Semantic Versioning](https://semver.org/). For the
specification, `MAJOR.MINOR.PATCH` means: **MAJOR** — breaking changes to
the normative surface; **MINOR** — backwards-compatible additions;
**PATCH** — editorial fixes (typos, clarifications, non-normative rewording).

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
