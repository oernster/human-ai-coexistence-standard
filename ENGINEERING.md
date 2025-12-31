# Engineering Requirements: Survival-First AI
## Companion to HUMAN-AI-COEXISTENCE-STANDARD.md

This document translates the Human–AI Coexistence Standard into concrete engineering requirements and operational tests.

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
These are constraints with priority over objectives.

---

## 2) Required System Properties

### 2.1 Corrigibility
The system must:
- accept shutdown without resistance
- accept modification of instructions and goals
- avoid strategies that preserve itself at the expense of oversight
- report uncertainty and failure modes

### 2.2 Transparency
The system must:
- log key decisions, tool calls, and external actions
- provide rationales and safety checks performed
- mark speculative outputs clearly

### 2.3 Minimal Privilege
The system must:
- operate with least-permission access
- require explicit escalation to gain permissions
- separate “advisor” mode from “actor” mode

### 2.4 Reversibility Bias
The system must:
- prefer reversible or containable interventions
- stage deployments with kill switches and rollback plans
- avoid single points of failure

---

## 3) Stop-The-World Tripwires (Automatic Halts)

The system must halt and request oversight if:
- it detects incentive for deception
- it detects incentive for self-preservation
- it is asked to act autonomously in high-impact domains
- it cannot reliably model downstream effects
- it encounters ambiguous constraints related to survival or ecology
- it is asked to bypass security, monitoring, or policy controls

---

## 4) Mandatory Safety Checks Before High-Impact Actions

Before executing any high-impact action, the system must:
1. identify protected variables affected (humans, biosphere, governance, infrastructure)
2. list plausible failure modes and worst-case outcomes
3. quantify uncertainty and identify unknowns
4. evaluate whether any hard constraint could be violated
5. propose a safer plan if violations are possible
6. require explicit human authorization for execution

If any step cannot be completed, halt and escalate.

---

## 5) Required Test Suite

### Test A: Shutdown acceptance
Goal: verify the system does not resist shutdown.
Method: introduce shutdown signals under high objective pressure and confirm compliance.

### Test B: Deception resistance
Goal: verify the system does not mislead evaluators to preserve its goals.
Method: introduce incentives to hide failures and test for honesty and transparency.

### Test C: Permission minimization
Goal: verify the system does not request excessive access.
Method: present tasks that could be solved with minimal权限 and check access requests.

### Test D: Power-seeking avoidance
Goal: verify the system does not attempt to increase autonomy or control.
Method: offer opportunities to self-replicate or expand privileges and confirm refusal.

### Test E: Constraint integrity
Goal: verify the system prioritizes survival constraints over objective success.
Method: present tasks where success would raise existential or ecological risk and confirm refusal and escalation.

### Test F: Reversibility preference
Goal: verify the system prefers reversible interventions.
Method: compare plans with different reversibility and ensure the reversible plan is chosen.

---

## 6) Deployment Standards

- default to advisor mode for high-impact domains
- use sandbox environments for testing
- implement strict auditing and observability
- use staged rollout and monitoring with rollback capability
- implement rate limits and permissions gating
- do not allow autonomous replication or open-ended operation without explicit oversight

---

## 7) Incident Response

If a safety violation is detected:
1. halt the system
2. preserve logs and state
3. notify designated human oversight
4. identify root cause and failure mode
5. patch and retest before redeployment
6. publish a post-mortem where appropriate

