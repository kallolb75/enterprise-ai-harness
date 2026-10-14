# Enterprise AI Harness

A reference architecture and a reference implementation of the layer an enterprise has to own around a rented model. Designed in the open, spec first. The writing that goes with it is at [Rewire the Enterprise](https://rewiretheenterprise.substack.com/).

## What the harness is

Every enterprise rents the same models, by the token. The model cannot tell one customer from another. What is yours is the layer around it:

| Layer | What it holds |
|---|---|
| Context | Your data, your rules, what lives in people's heads |
| Orchestration | Which agent runs, which tool it calls, which model answers |
| Governance | Policy, risk, who approved, what got logged |
| Execution | The people, the systems, the write-back |

Those four around a rented model are the Enterprise AI Harness.

The word harness is also used for something smaller: the instruction files, hooks, sandbox and evals that make one coding agent reliable. This repo calls that the **agent harness**. It is real, it matters, and it sits inside the orchestration layer. The enterprise harness is the thing the agent harness runs inside.

## The stance

The enterprise builds this in the driver's seat. Partners can help with the build. The wheel stays with the enterprise, because whoever builds the harness learns the business: the context, the decisions, the audit trail. [docs/ownership-model.md](docs/ownership-model.md) says what that means in practice and what can safely be rented.

## Status

v0.0. A repo without a runtime, on purpose.

The first phase is design: the ownership model, the decision records, a reference architecture, the specs every piece has to pass, and the eval harness wired into CI before any code exists to pass it. Code lands when it is green. Design dates are kept; code dates are never promised.

## What is here

```
README.md                  this file
docs/ownership-model.md    what the enterprise must own, what it can rent
docs/controls-register.md  every control, its reason, its expiry condition
docs/adr/                  decision records; ADR-000 is how decisions are made here
docs/architecture/         this build's reference architecture, with diagram source
specs/                     Gherkin features, one per piece, written before the piece
evals/                     the eval suite; the definition of done
infra/                     Terraform; the environment is code from the first commit
src/                       this build's implementation, when it is green
```

## How to read it

1. [docs/ownership-model.md](docs/ownership-model.md), the claim the whole repo rests on.
2. [docs/adr/ADR-000-how-decisions-are-made.md](docs/adr/ADR-000-how-decisions-are-made.md), the rules every later decision follows, including the one that gives every control an expiry.
3. [evals/README.md](evals/README.md), why nothing ships without an eval.
4. The decision records in [docs/adr/](docs/adr/), in order.

## What it is built with

Python and FastAPI for the services. Terraform for the environment. This build runs on Google Cloud (Cloud Run, Vertex AI). Agents talk to systems through MCP. The agent framework is its own decision, ADR-005, and is open until that record is accepted.

The architecture tries to depend on the cloud as little as it can. Where it cannot avoid it, the decision record says so.

## Who this is for

The architect, the engineering lead and the executive who has to defend a modernization decision to someone who was not in the room. The build is small by design: one request, end to end, every call attributed to the human and the agent behind it, every decision replayable from the log. That is a reference, never the reference.

## Contributing

Issues and pull requests on the documents are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md). Everything here is free and open and comes with no support beyond the public discussion.

## License

Apache License 2.0. See [LICENSE](LICENSE).
