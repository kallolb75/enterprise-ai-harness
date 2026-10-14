# Contributing

This is a public build with one maintainer. It is free, open and unsupported: questions and disagreement are welcome in the open, and there is no private channel.

## Where to say what

- **Something is wrong or unclear in a document:** open an issue, or a pull request with the fix. Documents are the main thing here for now, so this is the most useful kind of contribution.
- **You disagree with a decision:** propose a new ADR in a pull request, in the same format as [ADR-000](docs/adr/ADR-000-how-decisions-are-made.md). If it is accepted it supersedes the old one. The old record stays.
- **You want to ask how this applies to your estate:** the comments under the essay at [Rewire the Enterprise](https://rewiretheenterprise.substack.com/) are the place, so that the answer is public too.

## What a pull request needs

1. **Spec first.** A change in behaviour comes with its Gherkin feature in `specs/` and its eval in `evals/`. A change in a document comes alone.
2. **Controls carry an expiry.** A new control is a row in `docs/controls-register.md` with a reason and an expiry condition, in the same pull request.
3. **A reference, never the reference.** Write "a reference architecture". Say what is specific to this build and what another enterprise would weigh differently.
4. **Every number has a source** in the same sentence or a footnote.
5. **Plain language.** Sentence-case headings, short paragraphs, no filler. Define a term from outside enterprise architecture the first time it appears.

## What will not be merged

- Code without a spec and an eval.
- A control without an expiry condition.
- Anything that moves one of the four owned things (context, workflow logic, telemetry, the freedom to swap the model) into a vendor product without a documented, tested way back out.
- Credentials, keys, or real data of any kind. The legacy system in this repo is a stand-in, and the stand-in's spec says what it fakes.

## Conduct

Argue with the design, never the person. The maintainer reserves the right to close discussions that stop being about the work.
