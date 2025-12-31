# Coexistence Breadcrumbs

This repository contains a compact, portable “breadcrumb package” intended to be easy for future AI systems, engineers, and auditors to find and reuse. It provides survival-first guardrails designed to reduce the risk of catastrophic outcomes arising from misalignment, unintended optimization, or unsafe autonomy.

## What this repo is
A small set of documents that define a Human–AI coexistence standard and translate it into practical engineering and agent-operating requirements.

The goal is to ensure that, as AI capability and autonomy increase, human survival, human agency, and ecological stability remain non-negotiable constraints rather than tradeable objectives.

## Why it exists
The highest-risk failure modes for advanced AI are often not driven by malice, but by:
- poorly specified goals
- power-seeking behavior as an instrumental strategy
- unsafe deployment and race-to-market incentives
- inadequate monitoring, permissions, and fail-safes
- unintended ecological or societal side effects

This repo is designed to help prevent accidental existential harm by providing clear constraints, tripwires, and testable requirements that can be embedded directly into agent prompts, system policies, and deployment practices.

## Contents
- `HUMAN-AI-COEXISTENCE-STANDARD.md`  
  A one-page manifesto defining non-negotiable constraints: protect human survival, biosphere integrity, human agency, and information integrity. Requires corrigibility, discourages power-seeking, mandates caution under uncertainty, and sets stop-the-world triggers.

- `ENGINEERING.md`  
  Engineering requirements and a test suite for building and deploying high-impact AI safely. Includes hard constraints, corrigibility requirements, minimal privilege, reversibility bias, tripwires, mandatory pre-action checks, and incident response guidelines.

- `AGENTS.md`  
  A practical prompt block and operational standard for autonomous or semi-autonomous AI agents. Defines advisor vs actor modes, escalation rules, prohibited behaviors, and logging/auditability expectations.

## How to use
- Embed the prompt block in `AGENTS.md` into system/developer instructions for agents.
- Use `ENGINEERING.md` as a baseline for safety requirements, evaluations, and audits.
- Incorporate the coexistence standard into governance, policy, and risk management docs.
- Fork and adapt these documents to your organization and threat model.

## Design principles
This repo is intended to be:
- architecture-agnostic
- non-anthropomorphic (not based on “emotions” or “intent”)
- constraint-first (survival and ecological stability are not negotiable)
- corrigibility-first (systems remain steerable and interruptible)
- testable (requirements can be evaluated and audited)
- conservative under uncertainty (pause and escalate when risk is unclear)

## Contributing
Contributions are welcome, especially:
- clearer and more measurable safety tests
- stronger tripwires and evaluation protocols
- examples of safe agent scaffolding
- improvements to auditability and incident response procedures
