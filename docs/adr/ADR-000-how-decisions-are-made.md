# ADR-000: How decisions are made here

**Status** Accepted
**Date** 2026-10-14
**Deciders** Kallol Biswas

## Context

This repo is a reference architecture and a reference implementation, built in the open. Readers will reuse decisions from it in their own estates. A decision copied without its reasoning is a cargo cult, and a control copied without its expiry is how harness rot starts: a rule that made sense for one model, one regulation or one incident outlives all three and nobody remembers why it exists.

The repo needs one record that says how every later decision is made, written down and retired.

## Decision

### Every architectural decision is an ADR

A decision that shapes the harness (a layer boundary, an identity model, a storage choice, a framework, a control) is recorded as a numbered file in `docs/adr/`, in this format: context, decision, consequences, and for controls the expiry condition. One decision per record. Records are numbered in the order they are opened and never renumbered.

### A record has four states

`Proposed` means written and open for comment. `Accepted` means the build follows it. `Superseded` means a later record replaced it; the old record stays, with a link to the new one. `Retired` means the decision no longer applies and nothing replaced it. Nothing is deleted. The history is part of the reference.

### Every control carries a reason and an expiry condition

A control is anything that constrains what the harness or an agent may do: an approval gate, a policy check, a rate limit, a denied tool, a required human in the loop. Each one is recorded in `docs/controls-register.md` with four fields.

1. **Reason.** The risk it answers, in one sentence, naming the thing that would go wrong without it.
2. **Expiry condition.** The observable event that means the control should be reviewed: a model version, a regulation, a measured error rate, a date. "Never" is not an expiry condition.
3. **Owner.** Who reviews it when the condition is met.
4. **Status.** Active, Under review, Retired, with the date of each change.

When the expiry condition is met, the control is reviewed within the next cycle. It is renewed with a new condition, or retired with a note on what replaced it. A control that is renewed without a new condition is a defect.

### A reference, never the reference

Every design in this repo is a reference. The documents say "a reference architecture", never "the reference architecture". Where a choice is specific to this build (the cloud, the framework, the stand-in legacy system) the record says so, and says what a different enterprise would weigh.

### Specs before code, evals before done

No piece of the implementation is started without a Gherkin feature in `specs/` describing what it must do. No piece is done until an eval in `evals/` passes against it. A pull request that changes behaviour without changing a spec or an eval is sent back. See `evals/README.md`.

### Who decides

The maintainer accepts or rejects a record. Anyone may propose one, in a pull request, in the same format. A proposal that disagrees with an accepted record is welcome; it becomes a new record that supersedes the old one if accepted.

## Consequences

Decisions are slower to make and easier to reverse. The controls register will grow and then shrink, and the shrinking is the point. Readers can take any decision from this repo along with the reason it was made and the condition under which it should be questioned, which is the only responsible way to reuse someone else's architecture.

## Planned records

Numbers are reserved so later documents can cite them before they are written. A reserved number is a topic, not a promise of a date.

| ADR | Topic | Status |
|---|---|---|
| 000 | How decisions are made here | Accepted |
| 001 | Identity: both principals, the agent as a delegated principal | Reserved |
| 002 | Retrieval and the context boundary | Reserved |
| 003 | The one tool: one MCP server in front of one real system | Reserved |
| 004 | Storage and the trace event schema | Reserved |
| 005 | The agent framework | Reserved |
