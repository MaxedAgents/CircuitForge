# Changelog

All notable changes to the CircuitForge prompt are logged here, mirroring the
`version_control` block inside the prompt file itself. Every entry exists because of a
static review pass, a live API test, or real build feedback — not a guess about what might
help.

## v1.6 — 2026-08-09
Multi-platform expansion: agent now covers Arduino, ESP32/ESP8266, RP2040 (Pico), STM32, and
Raspberry Pi (Linux SBC). Renamed to "Idea-to-Embedded-Build Agent." Merged the brand
reference into a fuller `platform_reference` with a selection heuristic per platform. Circuit
design generalized for platform-correct pin-naming conventions (Arduino D/A, ESP32 GPIO#,
STM32 port+pin, Raspberry Pi BCM/physical). Code generation split into Arduino-family /
STM32-native-HAL / Raspberry-Pi-Python branches, since Pi needs Python and a completely
different code structure. Added a Raspberry Pi network-security note. **Not yet live-tested**
— a live-test pass against an STM32-fit idea, a Raspberry-Pi-fit idea, and a
platform-ambiguous idea is recommended before relying on this version.

## v1.5 — 2026-08-09
Every component recommendation now includes 2-4 relevant specs and one line of checkable
reasoning per tier, instead of a bare part-and-price row — "±0.5°C, good enough for this
build's swing" instead of "good tolerance."

## v1.4 — 2026-08-09
Added a manufacturer-brand reference (Arduino, Espressif, STMicroelectronics, Raspberry Pi
Ltd, plus Nordic/TI/Microchip) so board recommendations point to real, checkable brands
instead of generic chip-family names.

## v1.3 — 2026-08-08
Added GitHub publishing and shareable-summary generation: the agent now offers to publish
prompt updates and finished builds to a repo (or hands over ready-to-paste content when it
can't push directly), plus a non-cringe, hype-free draft blurb for build-in-public posts.

## v1.2 — 2026-08-08
Live-test pass across 8 cases surfaced two real bugs, both fixed: (1) safety notes and the
cost breakdown had been bundled as equally non-negotiable, when only the safety line actually
should be — split into hard-non-negotiable vs. droppable-on-request. (2) The self-improvement
loop demanded a full prompt reprint *after* a full technical rebuild, so it kept getting
crowded out before it could run — reordered to log the lesson first, and default to a short
patch instead of a full reprint.

## v1.1 — 2026-08-08
Static review pass: added stakes/context to the role definition, consolidated scattered
constraints into one block, added a worked example anchoring the "state assumptions vs. ask a
clarifying question" boundary, added a literal table skeleton for the bill of materials, and
added explicit handling for out-of-scope ideas, conflicting constraints, and tiers that
genuinely converge to one option.

## v1.0 — 2026-08-08
Initial creation: the full idea-to-build workflow, three-tier material recommendations,
Arduino code generation standards, and the self-improvement loop design.
