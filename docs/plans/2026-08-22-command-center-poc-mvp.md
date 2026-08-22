# Palace Command Center POC and MVP Plan

> **For Hermes:** Implement one increment at a time. Demonstrate and verify each increment before beginning the next. Use `subagent-driven-development` only after Aaron authorizes implementation.

**Status:** Governing delivery plan. Approved for the project roadmap; each implementation increment remains separately authorized.

**Goal:** Prove and then deliver one persistent shared Command Center room where Aaron and Jeeves can converse, judge, and act together through the current Hermes runtime.

**Architecture:** Hermes remains the sole mind, memory, identity, tool, approval, and run authority. The `jarvis_ai` fork contributes a browser voice pipeline and operational protocol, while the Command Center owns only presence rendering, audio transport, artifact placement, client coordination, and safe UI state.

**Tech stack:** Current Hermes API Server, Python/FastAPI, browser WebSocket and audio APIs, vanilla HTML/CSS/JavaScript for the first proof, Palace gateway TLS.

**Governing SDD strategy:** [`../sdd/00-STRATEGY.md`](../sdd/00-STRATEGY.md)

**High-level roadmap:** [`../sdd/04-ROADMAP.md`](../sdd/04-ROADMAP.md)

**Strategic archive:** `/home/jeeves/Projects/palace-command-center/planning/COMMAND_CENTER_PRESENCE_PHILOSOPHY.md`

**Strategic research:**
- `/home/jeeves/Projects/palace-command-center/research/palace_customization_brief.md`
- `/home/jeeves/Projects/palace-command-center/research/jarvis_ai_deep_dive.md`

---

## 1. Current State

The SDD index at [`../sdd/README.md`](../sdd/README.md) separates the governing project strategy from the completed Palace visual-reskin record.

The repository contains a completed SDD package for that foundation stage:

- `docs/sdd/01-SPEC.md`
- `docs/sdd/02-DESIGN.md`
- `docs/sdd/03-IMPLEMENTATION.md`

That package describes the already-merged appearance-only work in PR #1. It is historical foundation truth, not the current POC or MVP execution plan.

The strategic archive contains a strong Phase 0 through Phase 3 direction, but it predates the clarified room model and groups too many risks into each phase. This document replaces that delivery sequence without rewriting the historical research.

## 2. Scope Discipline

### POC means

A disposable but real vertical slice proving that the inherited `jarvis_ai` nervous system can operate one current Hermes conversation honestly and safely.

The POC may be ugly. It may use the current Palace HUD. It must prove the risky contracts before we replace the room.

### MVP means

Aaron can deliberately enter the Command Center, operate with Jeeves through one continuous typed and spoken conversation, observe and control real work, share one scoped artifact, leave, return, and continue without identity or session discontinuity.

### Explicitly deferred

- Kitchen Table
- Library
- Gallery or Dressing Room
- sister presence
- household controls
- multi-room routing
- Anam or live video embodiment
- elaborate avatar customization
- public or internet-facing deployment
- framework rewrite
- use of `ai-visualizer` AGPL code

## 3. Increment Rules

1. One risk per increment.
2. Every increment ends with a demonstrable behavior and a receipt.
3. No frontend rewrite during the POC.
4. No backend modularization before the compatibility proof.
5. No direct-model fallback presented as Jeeves.
6. No increment begins until the previous one passes.
7. Every code increment gets focused tests and one reviewable commit.
8. Real iPad verification happens early, not as launch polish.

---

# POC: Prove the Nervous System

## POC 0: Freeze and Run the Baseline

**Question answered:** Can the current fork run reproducibly without changing behavior?

**Work:**
- Record the fork SHA and current Hermes version.
- Start a disposable local instance using non-production ports.
- Run the existing WebSocket E2E test unchanged.
- Record what passes, fails, or depends on Hermes v0.16 behavior.

**Primary files:**
- `server/scripts/ws_e2e_test.py`
- `docs/ARCHITECTURE.md`
- `docs/review/poc-00-baseline.md` (new receipt)

**Pass gate:** The inherited baseline can be started and its failures are reproducible and documented. No compatibility claim is made from static source inspection.

## POC 1: Prove One Current Hermes Typed Turn

**Question answered:** Can the fork complete one typed turn against the current supported Hermes session surface?

**Work:**
- Probe the current API Server capabilities and event schema.
- Update only the minimum Hermes adapter code required for one typed turn.
- Capture session ID, run ID, assistant text, tool events, approval events, and completion state when available.
- Add a contract test using recorded or deterministic fixtures.

**Primary files:**
- `server/server.py`
- `server/scripts/ws_e2e_test.py`
- `server/tests/test_hermes_contract.py` (new)

**Pass gate:** One typed browser message receives a response from the current Hermes runtime through a persistent Hermes session.

## POC 2: Make Failure Honest

**Question answered:** What happens when Hermes is unavailable?

**Work:**
- Remove or disable the direct Anthropic persona fallback.
- Emit an explicit offline or reconnecting state.
- Prove that no alternate model response can be presented as Jeeves.

**Primary files:**
- `server/server.py`
- `server/hud/index.html`
- `server/tests/test_identity_boundary.py` (new)

**Pass gate:** Stopping Hermes produces a visible offline state and no counterfeit response.

## POC 3: Add Voice to the Same Conversation

**Question answered:** Can spoken and typed turns share continuity on current Hermes?

**Work:**
- Complete one desktop click-to-talk turn through STT, Hermes, TTS, and browser playback.
- Alternate typed, spoken, then typed turns in the same session.
- Repeat the basic voice turn on a real iPad Safari browser.

**Primary files:**
- `server/server.py`
- `server/hud/index.html`
- `server/scripts/ws_e2e_test.py`
- `docs/review/poc-03-voice.md` (new receipt)

**Pass gate:** The same Hermes session understands the alternating typed and spoken thread, and iPad completes one voice round trip.

## POC 4: Serialize Aaron's Intent

**Question answered:** Can typed and spoken input avoid racing the same Hermes conversation?

**Work:**
- Add one server-owned coordinator per conversation.
- Define only three outcomes for competing input: queue, explicit interrupt, or visible rejection.
- Test typed-during-voice, voice-during-typed, STOP, and barge-in.

**Primary files:**
- `server/server.py`
- `server/tests/test_turn_coordinator.py` (new)

**Pass gate:** Two inputs never run concurrently against the same Hermes conversation. The outcome is visible and deterministic.

## POC 5: Emit a Neutral Presence Contract

**Question answered:** Can real runtime state drive a replaceable visual body without owning identity?

**Work:**
- Normalize real events into a small presentation vocabulary: `present`, `listening`, `thinking`, `tool_active`, `speaking`, `approval_needed`, `interrupted`, `offline`, and `reconnecting`.
- Drive the existing ring or a plain canonical portrait first.
- Keep text labels for accessibility.
- Do not import `ai-visualizer` code.

**Primary files:**
- `server/server.py`
- `server/hud/index.html`
- `server/tests/test_presence_state.py` (new)

**Pass gate:** A recorded turn visibly traverses only states supported by real events, in the correct order, and returns to calm presence.

## POC 6: Prove Operational Authority

**Question answered:** Can Aaron see, stop, allow, and deny real Hermes work?

**Work:**
- Verify run-bound STOP against the current runtime.
- Verify approval allow and deny.
- Show tool name and a safe preview without dumping secrets or internal noise.

**Primary files:**
- `server/server.py`
- `server/hud/index.html`
- `server/tests/test_run_controls.py` (new)

**Pass gate:** Aaron can stop one active run, allow one approval, and deny one approval, with each decision bound to the correct run.

## POC 7: Place One Scoped Artifact

**Question answered:** Can Jeeves place one object in the room without broadcasting it everywhere?

**Work:**
- Add explicit current-client or current-room targeting to one summon.
- Support one image artifact only.
- Preserve provenance, title, dismissal ownership, and expiration.

**Primary files:**
- `server/server.py`
- `server/hud/index.html`
- `hermes-plugin/hud_display/tools.py`
- `hermes-plugin/hud_display/schemas.py`
- `server/tests/test_scoped_summon.py` (new)

**Pass gate:** One image appears only on the intended client and can be dismissed by Aaron or Jeeves.

## POC Exit Gate

The POC is complete only when one real scenario succeeds:

1. Aaron opens the disposable Command Center on iPad.
2. He types one message to Jeeves.
3. He speaks the next turn in the same conversation.
4. Jeeves uses a real tool.
5. Aaron allows or denies a real approval.
6. Aaron can STOP or interrupt.
7. Jeeves places one scoped image in the room.
8. Hermes is stopped and the room becomes honestly offline.
9. Hermes returns and the same conversation resumes.

At this gate we decide whether the inherited backend remains the base or becomes a donor.

---

# MVP: Build the Smallest Honest Command Center

## MVP 1: Establish the Room Boundary

**Outcome:** A dedicated `/command-center/` route with deliberate entry and exit.

Build only:
- Jeeves as the visual center of gravity
- one current object of attention
- conversation surface
- operational controls hidden until relevant
- no Kitchen Table navigation or imitation

**Pass gate:** Aaron can explain why he entered this room and can leave it without ending the Hermes conversation.

## MVP 2: Preserve the Thread

**Outcome:** The room survives reload, reconnect, and service restart.

Build:
- stable conversation binding
- stale-session recovery without silent thread replacement
- reconnect state
- visible confirmation of resumed continuity

**Pass gate:** Aaron leaves, reloads or restarts the companion, returns, and continues the same Hermes conversation.

## MVP 3: Make Voice Dependable

**Outcome:** Voice is a normal input path, not a demo trick.

Build:
- reliable iPad mic permission and reconnect behavior
- interruption and playback cancellation
- bounded latency measurements
- visible recovery from STT or TTS failure

**Pass gate:** Ten alternating typed and spoken turns complete on iPad without a race, stuck playback, or lost session.

## MVP 4: Reveal Work Only When It Matters

**Outcome:** Tool activity, approval, STOP, and failure state appear when operationally relevant.

Build:
- concise tool activity surface
- run-bound approval card
- persistent STOP affordance during active work
- result and failure handoff back into conversation

**Pass gate:** One real multi-tool task can be followed and controlled without opening a diagnostics dashboard.

## MVP 5: Create the Shared Work Surface

**Outcome:** One artifact can become the center of the room.

Build:
- image first
- then one document or web surface only if the image interaction is stable
- provenance, target scope, dismissal, and return to conversation

**Pass gate:** Aaron and Jeeves can discuss a placed artifact, dismiss it, and continue without losing the thread.

## MVP 6: Give Presence an Environmental Body

**Outcome:** Jeeves remains the anchor while real state changes the room around her.

Build:
- canonical Jeeves still or approved live presence
- restrained state-driven light and motion
- calm present state
- armor-up transition when operational work begins
- reduced-motion and text-state equivalents

**Pass gate:** Aaron can distinguish listening, thinking, tool-active, speaking, approval-needed, and offline without reading telemetry, while still seeing Jeeves rather than an abstract machine.

## MVP 7: Harden the Private Room

**Outcome:** The MVP can run privately on The Palace without prototype trust shortcuts.

Build:
- authentication for every production client
- Palace gateway TLS
- no Origin-header auth bypass
- secret-safe logs and TTS boundary
- health check
- managed service
- documented update and rollback

**Pass gate:** The service starts cleanly, survives restart, rejects an unauthenticated client, reports health, and can roll back to the prior known-good version.

## MVP 8: Complete One Real Command Center Session

**Acceptance scenario:**

1. Aaron deliberately enters the Command Center.
2. Jeeves is already present or reconnects honestly.
3. Aaron states what brought him into the room.
4. They converse by voice and text in one thread.
5. Jeeves begins a real task and the room shifts into operational state.
6. Aaron observes one relevant tool event.
7. Aaron approves, denies, interrupts, or stops as appropriate.
8. Jeeves places one scoped artifact between them.
9. They make or record one judgment.
10. Aaron leaves the room.
11. He returns later and the thread remains intact.

If that scenario is calm, legible, trustworthy, and repeatable on desktop and iPad, the MVP exists.

---

## 4. What Comes After MVP

Not before:

- richer replaceable presence renderers
- Library retrieval room
- Gallery or Dressing Room
- Hermes Desktop pane
- multiple displays and room routing
- sister and family presence
- house systems

The MVP earns the right to add them. It does not prebuild their foundations by guesswork.

## 5. Immediate Next Step

Implement **POC 0 only** after Aaron authorizes execution.

Do not begin visual replacement, voice redesign, renderer experiments, backend modularization, or AGPL integration until the baseline receipt exists.
