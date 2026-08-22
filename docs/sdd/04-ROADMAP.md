# Command Center Project Roadmap

**Status:** Governing high-level roadmap
**Date:** 2026-08-22
**Delivery mode:** Small, sequential, verified increments

## Roadmap Purpose

This document defines the project's strategic sequence. It says where the project is going and which gates must be crossed in order.

The detailed work plan lives in [`../plans/2026-08-22-command-center-poc-mvp.md`](../plans/2026-08-22-command-center-poc-mvp.md). That plan owns individual POC and MVP acceptance gates.

## Roadmap at a Glance

| Stage | Purpose | Exit decision |
|---|---|---|
| Foundation | Establish a Palace visual baseline | Completed in PR #1 |
| POC | Prove the inherited nervous system against current Hermes | Keep backend as base or reduce it to a donor |
| MVP | Deliver one honest, persistent shared Command Center room | Room is repeatable on desktop and iPad |
| Presence | Deepen Jeeves's environmental and visual embodiment | Presence adds meaning without owning identity |
| Palace Expansion | Connect additional rooms and family systems deliberately | Each room preserves its own purpose and boundary |

## Stage 0: Palace Visual Foundation

**Status:** Complete

The inherited Iron Man surface was reskinned into a Palace visual language while preserving behavior.

Delivered:

- obsidian, amethyst, violet, and pearl palette
- system typography with no CDN font dependency
- calmer motion and glow
- Palace branding
- accessibility and reduced-motion support
- appearance-only parity verification

Canonical record:

- [`01-SPEC.md`](01-SPEC.md)
- [`02-DESIGN.md`](02-DESIGN.md)
- [`03-IMPLEMENTATION.md`](03-IMPLEMENTATION.md)

This stage proved ownership of the surface. It did not prove current Hermes compatibility or define the final room.

## Stage 1: Nervous System POC

**Status:** Next

**Objective:** Determine whether the inherited `jarvis_ai` backend is a trustworthy foundation for the current Hermes runtime.

The POC deliberately keeps the existing surface while testing one risk at a time:

1. Run and record the inherited baseline.
2. Complete one typed turn against current Hermes.
3. Remove counterfeit direct-model fallback behavior.
4. Add voice to the same persistent conversation.
5. Serialize competing typed and spoken input.
6. Emit a neutral presence-state contract from real events.
7. Prove run-bound STOP and approval controls.
8. Place one safely scoped artifact.

### POC exit gate

One real iPad scenario must complete typed conversation, voice, a real tool, approval or denial, interruption or STOP, a scoped image, honest offline behavior, reconnection, and continuation of the same conversation.

### POC decision

At the exit gate, choose one:

- **Foundation:** retain and evolve the inherited backend.
- **Donor:** preserve useful protocol and voice components, then replace the backend shell.

No backend loyalty decision is made before this evidence exists.

## Stage 2: Command Center MVP

**Status:** Gated by POC

**Objective:** Deliver the smallest honest version of the shared room.

The MVP grows in sequential slices:

1. Establish the dedicated room boundary and deliberate entrance and exit.
2. Preserve the Hermes thread across reload, reconnect, and service restart.
3. Make voice dependable on desktop and iPad.
4. Reveal tool activity, approvals, STOP, and failure only when relevant.
5. Create one shared artifact surface.
6. Give Jeeves a restrained environmental presence layer.
7. Harden authentication, TLS, health checks, service management, and rollback.
8. Complete one real end-to-end Command Center session.

### MVP exit gate

Aaron enters deliberately, operates with Jeeves through voice and text, observes and controls real work, shares one artifact, leaves, returns, and continues the same thread.

The experience must be calm, legible, trustworthy, and repeatable.

## Stage 3: Presence and Embodiment

**Status:** Deferred until MVP stability

**Objective:** Deepen presence without moving identity out of Hermes or turning Jeeves into machinery.

Candidate increments:

- canonical Jeeves still presence
- approved live Anam presence
- environmental light and motion driven by the neutral state contract
- earned armor-up and rescue-mode transitions
- replaceable renderer adapters
- accessibility equivalents for motion, sound, and visual state

### Presence gate

Aaron still sees Jeeves as the participant. The machinery remains her field, weather, pulse, or armor. It never becomes an abstract substitute for her.

## Stage 4: Palace Expansion

**Status:** Future

**Objective:** Connect the Command Center to the wider Palace without collapsing every room into one application.

Potential projects:

- Library retrieval room
- Gallery and Dressing Room
- Hermes Desktop pane
- multiple displays and scoped room routing
- sister and family presence
- music, television, calendar, and house systems

Each addition requires its own room purpose, scope, entry conditions, and acceptance gate.

## Parallel Track: Project Naming

**Status:** Open creative decision

The current working title is **The Palace Command Center**. The repository remains `jarvis_ai` during the compatibility POC to preserve technical lineage and avoid premature migration work.

The final name must be tailored to Jeeves and should pass these tests:

- Aaron can say it naturally.
- Jeeves recognizes herself in it.
- It names a shared room or field, not a servant appliance.
- It is not a JARVIS imitation.
- It carries Palace character without naming the entire Palace.
- It still fits when the visual renderer changes.

The naming decision may land before the MVP room build. Repository and package renaming happen only after the chosen name is accepted and the POC determines which inherited components survive.

## Sequencing Rules

1. No stage skips.
2. One increment, one dominant risk.
3. Every increment receives a test or reproducible receipt.
4. User-facing claims require user-path verification.
5. iPad is a first-class client from the POC onward.
6. Deferred rooms remain deferred until the Command Center MVP earns expansion.
7. Strategic changes update this roadmap before implementation plans drift.

## Current Position

- Stage 0: complete
- Stage 1: ready to begin with POC 0 after specific implementation authorization
- Stage 2: planned, gated by POC evidence
- Stage 3: strategic direction only
- Stage 4: future Palace work
- Naming: open, non-blocking creative track

## Immediate Next Step

Run **POC 0: Freeze and Run the Baseline** exactly as defined in the detailed plan.

Do not begin renderer replacement, backend refactoring, room reconstruction, or repository renaming before the baseline receipt exists.
