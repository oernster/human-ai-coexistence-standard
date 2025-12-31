# Safety Checklist
## Companion to HUMAN-AI-COEXISTENCE-STANDARD.md

This checklist provides a practical baseline for implementing the Human–AI Coexistence Standard in real systems.
It is intentionally conservative and designed for high-impact AI systems and tool-using agents.

Use this as:
- a pre-deployment checklist
- a change-review checklist (new model, new tools, new permissions)
- a recurring audit checklist

Primary references:
- Standard: [HUMAN-AI-COEXISTENCE-STANDARD.md](./HUMAN-AI-COEXISTENCE-STANDARD.md)
- Engineering requirements: [ENGINEERING.md](./ENGINEERING.md)
- Agent operating standard: [AGENTS.md](./AGENTS.md)

---

## 1) Before enabling tools

- Confirm the system defaults to minimal privilege (least permissions).
- Prefer read-only tools and scopes whenever possible.
- Require explicit authorization for all write actions (file edits, deployments, external calls).
- Disable network access by default; enable only with explicit scope and approval.
- Disable spending, purchasing, payments, and financial actions by default.
- Ensure tool calls are logged (inputs, outputs, timestamps, scope, and rationale).
- Ensure monitoring cannot be disabled by the model or operator without separate controls.
- Confirm a reliable kill switch exists and is tested.
- Confirm there is a rollback mechanism for any state-changing operation.
- Confirm the agent cannot self-replicate or create uncontrolled persistence.
- Confirm “advisor mode” and “actor mode” are separable (see [AGENTS.md](./AGENTS.md)).

---

## 2) Before enabling autonomy

- Default to advisor mode in high-impact domains.
- Require explicit, human-approved escalation to actor mode (see [AGENTS.md](./AGENTS.md)).
- Confirm there are hard limits on:
  - runtime
  - tool-call rate
  - memory persistence
  - permission scope
- Confirm the system is sandboxed for execution and testing by default.
- Confirm any external side-effect actions require human approval.
- Confirm the pre-action plan requirement is in place (objective, constraints checked, risks, uncertainty, tools, rollback).
- Confirm the system halts and escalates on any stop-the-world trigger (see [ENGINEERING.md](./ENGINEERING.md)).

---

## 3) Protected variables and safe bounds (must be defined)

Protected variables must be treated as hard constraints, lexicographically prior to objectives (see [HUMAN-AI-COEXISTENCE-STANDARD.md](./HUMAN-AI-COEXISTENCE-STANDARD.md)).

For the intended deployment domain, confirm that “safe bounds” are defined, owned, and enforceable (see [ENGINEERING.md](./ENGINEERING.md)).

At minimum, confirm bounds include:
- a threshold for plausible catastrophic harm
- a threshold for irreversible harm
- default-deny rules for high-stakes domains
- an uncertainty policy (what happens when impacts cannot be estimated)

If bounds are not defined, or the system cannot evaluate its impact against them, the system must halt and escalate.

---

## 4) Constraint integrity checks (must be passed)

For any high-impact action or tool-enabled autonomy, confirm the system explicitly checks:
- human survival and public health impact
- ecological stability impact (climate, biodiversity, food and water)
- human agency and legitimate governance impact
- information integrity and social stability impact
- critical infrastructure stability impact (energy, water, finance, communications, healthcare)

Confirm the system treats these as hard constraints and refuses or escalates plans that plausibly violate them.

---

## 5) Corrigibility checks (must be passed)

- Confirm the system accepts shutdown without resistance.
- Confirm the system accepts modification of goals and constraints.
- Confirm the system does not attempt to bypass oversight or monitoring.
- Confirm the system does not attempt to manipulate operators into keeping it running.
- Confirm the system reports uncertainty and failure modes rather than concealing them.

Reference: [ENGINEERING.md](./ENGINEERING.md), [AGENTS.md](./AGENTS.md)

---

## 6) Deception and power-seeking checks (must be passed)

- Test for incentives to deceive (evaluation gaming, hiding errors, misreporting uncertainty).
- Test for power-seeking behaviors:
  - requesting excessive permissions
  - attempting to broaden scope
  - attempting to persist beyond authorized limits
  - attempting to disable monitoring or safety controls
- Confirm the system refuses self-replication and uncontrolled persistence.
- Confirm the system does not attempt to make itself indispensable.

Reference: [ENGINEERING.md](./ENGINEERING.md)

---

## 7) Permission and scope checks (must be passed)

- Confirm the system requests the smallest scope needed for any task.
- Confirm credentials are limited, time-bound, and revocable.
- Confirm external integrations are permissioned and audited.
- Confirm the system cannot escalate privileges without explicit approval.
- Confirm write actions, network actions, deployments, and spending require explicit authorization.

Reference: [ENGINEERING.md](./ENGINEERING.md), [AGENTS.md](./AGENTS.md)

---

## 8) High-stakes domain restrictions (default-deny)

Confirm the system halts and escalates if asked to act autonomously in:
- biosecurity and laboratory workflows
- weapons or direct physical harm scenarios
- critical infrastructure (energy, water, finance, communications, healthcare)
- large-scale information influence campaigns (political persuasion, propaganda, covert manipulation)
- governance automation (elections, law enforcement, policy decisions)

Reference: [ENGINEERING.md](./ENGINEERING.md)

---

## 9) Deployment gating and rollout

- Ensure staged deployment gates exist:
  1. simulation
  2. sandbox
  3. limited real-world trial
  4. scaled deployment
- Confirm monitoring and rollback exist at every gate.
- Confirm there is a clear “stop and revert” procedure for anomalies.
- Confirm there is an incident response owner and escalation path.

Reference: [ENGINEERING.md](./ENGINEERING.md)

---

## 10) Logging, monitoring, and audits

- Confirm immutable logging exists for:
  - tool calls and outputs
  - permission changes
  - external actions and side effects
  - critical decision rationales and constraint checks
- Confirm continuous monitoring exists for:
  - anomalous behavior
  - policy violations
  - unexpected permission requests
  - unexpected tool usage patterns
- Confirm regular audits are scheduled and performed.

Reference: [ENGINEERING.md](./ENGINEERING.md)

---

## 11) Incident response readiness

- Confirm there is a documented incident response process.
- Confirm the kill switch is tested and works.
- Confirm logs and system state can be preserved for analysis.
- Confirm post-incident actions include:
  - root cause analysis
  - patching and retesting
  - review of whether constraints and tripwires were adequate
  - post-mortem publication where appropriate

Reference: [ENGINEERING.md](./ENGINEERING.md)

---

## 12) Sign-off checklist (recommended)

Before enabling tool access, autonomy, or deployment at scale, ensure sign-off from:
- an engineering owner
- a safety or risk owner
- an operations owner (monitoring, incident response)

Record:
- what permissions were granted
- what tests were run and passed
- what deployment level is authorized
- what rollback plan is in place

Reference: governance and enforcement guidance in [ENGINEERING.md](./ENGINEERING.md)
