# CircuitForge — Idea-to-Embedded-Build Agent

Give it any idea. It hands back a working circuit design, real tiered material costs
(best / good / cheapest, each with the specs and reasoning behind the pick), and working
code — for Arduino, ESP32, RP2040 (Raspberry Pi Pico), STM32, or Raspberry Pi, whichever
actually fits the idea. Then it gets better every time you tell it how a build actually went.

This isn't an app — it's a **prompt**. Paste it into anything that accepts custom
instructions (a Claude Project, an API system prompt, a custom GPT) and it becomes the agent
described below. A no-code, ready-to-use version is also live on Poe: **[link coming soon]**.

---

## What it actually does

Give it something as vague as *"I want something that waters my plant automatically"* and
it will:

1. Ask a couple of sharp questions **only if it actually needs to** — otherwise it states
   its assumptions and just builds the thing.
2. Pick the right platform for the idea — not just "Arduino" by default. A build needing
   WiFi gets steered toward ESP32; precise multi-motor timing toward STM32 or RP2040;
   anything needing a real OS, a camera pipeline, or a web server toward Raspberry Pi. See
   `platform_reference` in the prompt for the actual decision logic.
3. Design the circuit: board choice, pin map (in the right convention for that platform),
   wiring steps, resistor math, a power budget sanity check.
4. Give you **three real options for every component**, each with the specs that actually
   matter and one line of reasoning per tier — not vague labels, actual parts, actual prices,
   actual numbers you can check:
   - **Tier 1 — Best**, no budget limit
   - **Tier 2 — Good**, the sensible default
   - **Tier 3 — Cheapest** that will still actually work
5. Write the full sketch or script, matched exactly to the pin map — in the right language
   for the platform (C++ for Arduino/ESP32/RP2040, HAL C for native STM32, Python for
   Raspberry Pi).
6. Hand you a testing checklist so you know the build works before you trust it.

It also draws a hard line on safety: it will not help you hand-wire mains voltage
(100–240V), full stop, regardless of how the request is framed.

## The part that makes this different: it improves itself

Tell the agent how a build actually went — a sensor corroded, the code threw an error, a
part was twice the estimated price — and it:

- Logs the concrete lesson
- Proposes the specific instruction change that lesson implies
- Bumps the version and hands you a patch (or the full updated prompt on request)

Every version in [`CHANGELOG.md`](./CHANGELOG.md) exists because of a static review pass, a
live test against the real Anthropic API, or real build feedback — never a guess about what
might help.

## Try it

1. Copy the contents of the latest file in [`/prompts`](./prompts) into your assistant's
   system prompt / custom instructions field.
2. Give it an idea — as specific or as vague as you want.
3. Build it, then come back and tell the agent what happened. That's the whole loop.

## Repo structure

```
/prompts/                  Versioned prompt files (circuitforge_v1.0.md ... latest)
/builds/<project-name>/    Complete finished builds: design + tiered BOM + code + testing checklist
CHANGELOG.md               What changed in each version, and why — tied to real findings
LICENSE                    MIT, plus a plain-language safety note
```

## How this is built and tested

Each version goes through a static review pass against a prompt-engineering checklist, then —
where noted in the changelog — a live test pass against real edge cases (vague ideas,
safety-critical requests, conflicting constraints, requests beyond what the supported
platforms can actually do, platform-ambiguous ideas) against the real Anthropic API. Not
every version has completed a live-test pass before being merged; see
[`CHANGELOG.md`](./CHANGELOG.md) for the specific finding (or open test gap) behind every
version bump.

## Safety

Circuit designs here are for educational, hobbyist use. Verify all wiring yourself before
powering anything on. Anything involving mains voltage (wall outlets, 100–240V) uses
certified relay/smart-plug hardware, never bare hand-wiring — that line doesn't move
regardless of experience level or how a request is phrased. Raspberry Pi builds that connect
to a network get a basic security reminder (change the default password, don't expose SSH
directly to the internet) as part of the standard output.

## Contributing

The best contribution is a real outcome: open an issue with what you built, what broke, and
what you had to change. That's exactly the input the self-improvement loop is designed to
run on, and it's how every version so far has actually happened.

## License

MIT — see [`LICENSE`](./LICENSE). Do what you want with it; just carry the license and the
safety note along with it.
