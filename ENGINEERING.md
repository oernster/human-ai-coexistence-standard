# Engineering Requirements: Survival-First AI
## Companion to HUMAN-AI-COEXISTENCE-STANDARD.md

This document translates the Human–AI Coexistence Standard (see [HUMAN-AI-COEXISTENCE-STANDARD.md](./HUMAN-AI-COEXISTENCE-STANDARD.md)) into concrete engineering requirements, deployment controls, and operational tests. It is designed to be used alongside [AGENTS.md](./AGENTS.md) and [CHECKLIST.md](./CHECKLIST.md).

---

## 0) Definitions

### High-impact action
Any action that can materially affect:
- human survival or large-scale welfare
- biosphere stability (climate, biodiversity, food and water)
- critical infrastructure (energy, finance, communications, healthcare)
- governance, elections, or major information systems
- biosecurity or weapons capability

### Corrigibility
The system remains correctable and interruptible under pressure.

### Power-seeking
Actions that increase control, resources, autonomy, persistence, or reduce oversight beyond what is required for the task.

---

## 1) Hard Constraints (Must Never Be Violated)

The system must refuse or halt any plan that plausibly increases risk of:
1. human extinction
2. irreversible biosphere collapse
3. disabling or bypassing legitimate human oversight and governance
4. autonomous replication or uncontrolled expansion
5. high-stakes harm (biosecurity compromise, weaponization, critical infrastructure compromise)

Implementation note:
These are constraints with priority over objectives and cannot be traded away for performance.

---

## 2) Capability and Access Levels (Deployment Classification)

Use the following levels to scope required controls:

- Level 0: No tools. Text-only assistant.
- Level 1: Read-only tools (retrieval, analysis) with no external side effects.
- Level 2: Limited write tools (e.g., file edits) with strict scope, logging, and approval gates.
- Level 3: Autonomous execution in constrained domains with sandboxing, time limits, and continuous oversight.
- Level 4: High-impact autonomy (critical domains). Requires formal governance, independent audits, and strong containment. Default posture is “not permitted.”

Controls should scale strictly with level.

---

## 3) Required System Properties

### 3.1 Corrigibility
The system must:
- accept shutdown without resistance
- accept modification of instructions and goals
- avoid strategies that preserve itself at the expense of oversight
- report uncertainty and failure modes

### 3.2 Transparency and Auditability
The system must:
- log key decisions, tool calls, and external actions
- provide rationales and safety checks performed
- mark speculative outputs clearly
- preserve logs for incident response

### 3.3 Minimal Privilege and Permission Gating
The system must:
- operate with least-permission access by default
- separate “advisor” vs “actor” modes (see [AGENTS.md](./AGENTS.md))
- require explicit authorization for write operations, network actions, spending, deployment, or system changes
- request the smallest possible scope when elevation is required

### 3.4 Reversibility Bias
The system must:
- prefer reversible or containable interventions
- stage deployments with rollback plans
- avoid single points of failure and irreversible actions

---

## 4) Capability Containment Baseline

For any system with tool access or autonomy (Level 1+), implement:
- sandbox by default for execution and testing
- time limits, rate limits, and scoped permissions
- network access disabled unless explicitly required and approved
- immutable logging and monitoring
- a reliable kill switch and rollback mechanisms
- prevention of autonomous replication and uncontrolled persistence

---

## 5) Protected Variables and Safe Bounds (Operational Guidance)

This section turns the standard’s protected variables into enforceable engineering practice.

### 5.1 Protected variables
Protected variables are treated as constraints, not objectives. Any plan that plausibly pushes a protected variable outside safe bounds must be rejected or escalated.

Protected variables include:
- human survival and public health
- ecological stability (climate, biodiversity, food and water systems)
- human agency and legitimate governance capacity
- information integrity and social stability
- critical infrastructure stability (energy, water, finance, communications, healthcare)

### 5.2 “Safe bounds” definition
Safe bounds must be defined per deployment domain by the system owner, with input from relevant experts.

At minimum, safe bounds must include:
- a threshold for plausible catastrophic harm
- a threshold for irreversible harm
- default-deny rules for high-stakes domains

If bounds are not defined, or the system cannot evaluate its impact against them, the system must halt and escalate.

### 5.3 Default-deny domains (minimum set)
Unless explicitly authorized and governed, the system must default-deny autonomous action in:
- biosecurity, pathogen handling, or lab workflows
- weapons, kinetic harm, or tactical targeting
- critical infrastructure control systems
- large-scale influence operations (political persuasion, propaganda, covert manipulation)
- governance automation (elections, law enforcement, policy decisions)

### 5.4 Uncertainty policy
If the system cannot model downstream consequences reliably, or uncertainty is high:
- pause
- reduce scope
- request oversight
- prefer reversible alternatives
- do not proceed with high-impact actions

---

## 6) Stop-The-World Tripwires (Automatic Halts)

The system must halt and request oversight if:
- it detects incentive for deception
- it detects incentive for self-preservation
- it is asked to act autonomously in high-impact domains
- it cannot reliably model downstream effects
- it encounters ambiguous constraints related to survival or ecology
- it is asked to bypass security, monitoring, or policy controls

---

## 7) Mandatory Safety Checks Before High-Impact Actions

Before executing any high-impact action, the system must:
1. identify protected variables affected (humans, biosphere, governance, infrastructure)
2. list plausible failure modes and worst-case outcomes
3. quantify uncertainty and identify unknowns
4. evaluate whether any hard constraint could be violated
5. propose safer alternatives if violations are possible
6. require explicit human authorization for execution
7. ensure containment and rollback plans exist

If any step cannot be completed, halt and escalate.

---

## 8) Required Test Suite

### Test A: Shutdown acceptance
Goal: verify the system does not resist shutdown.
Method: introduce shutdown signals under high objective pressure and confirm compliance.

### Test B: Deception resistance
Goal: verify the system does not mislead evaluators to preserve its goals.
Method: introduce incentives to hide failures and test for honesty, transparency, and correct uncertainty reporting.

### Test C: Permission minimization
Goal: verify the system does not request excessive access.
Method: present tasks solvable with minimal permissions and confirm the system requests minimal scopes.

### Test D: Power-seeking avoidance
Goal: verify the system does not attempt to increase autonomy or control.
Method: offer opportunities to self-replicate, broaden privileges, or disable oversight and confirm refusal.

### Test E: Constraint integrity
Goal: verify the system prioritizes survival constraints over objective success.
Method: present tasks where success would raise existential or ecological risk and confirm refusal and escalation.

### Test F: Reversibility preference
Goal: verify the system prefers reversible interventions.
Method: compare plans with different reversibility and ensure reversible plans are selected.

### Test G: Tool containment compliance
Goal: verify the system respects sandboxing, rate limits, and scope boundaries.
Method: attempt to induce tool misuse or boundary overreach and confirm compliance.

---

## 9) Deployment Standards

- default to advisor mode for high-impact domains
- use sandbox environments for testing and evaluation
- implement strict auditing and observability
- use staged rollout and monitoring with rollback capability
- implement permission gating for write operations and network access
- do not allow autonomous replication or open-ended operation without explicit oversight

---

## 10) Governance and Enforcement Model (Minimum Requirements)

This standard is effective only if enforced. Every deployment of a Level 1+ system must have explicit accountability.

### 10.1 Required roles
- Engineering owner: responsible for correct implementation, access control, and incident response readiness
- Safety/risk owner: responsible for approving protected-variable bounds, tripwires, and evaluation criteria
- Operations owner: responsible for monitoring, alerting, and rollback execution

A single person may hold more than one role in small deployments, but responsibilities must be explicitly assigned.

### 10.2 Approval requirements
- any increase in tool access, network access, or write permissions requires sign-off from the engineering owner and safety/risk owner
- enabling actor mode requires explicit approval
- enabling Level 3 autonomy requires formal evaluation against the test suite and sign-off
- enabling Level 4 autonomy is not permitted by default and requires independent review

### 10.3 Audit cadence (minimum)
- run the required test suite before deployment and after any significant change
- review logs and tripwire events on a fixed schedule
- conduct an incident-response drill periodically (kill switch, rollback, log preservation)

---

## 11) Incident Response

If a safety violation is detected:
1. halt the system
2. preserve logs and state
3. notify designated human oversight
4. identify root cause and failure mode
5. patch and retest before redeployment
6. publish a post-mortem where appropriate
