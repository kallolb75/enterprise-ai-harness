# Evals: the definition of done

Nothing in this repo is done until an eval says so.

## The rule

1. Every piece has a Gherkin feature in `specs/` before any code is written for it.
2. Every feature has at least one eval here that exercises it against the running piece.
3. A pull request that changes behaviour without changing a spec or an eval is sent back.
4. CI runs the suite on every pull request. A red suite blocks the merge. There is no override flag.
5. When the model is swapped, the whole suite runs again before the swap is accepted. The suite is how the freedom to swap the model is proven rather than claimed.

## Why it comes first

In the public agent builds I have read, tests and evals are the exception, and a before-and-after measurement of a change is rarer still. A harness without evals is a harness that nobody can safely change, which means it will be changed carelessly or never. Either way it rots.

Writing the eval before the piece also forces the question the design most needs answered: what does correct look like for this piece, observably, and who decided that?

## What an eval checks

Three kinds, and every piece gets at least the first two.

- **Behaviour.** The piece does what its feature says, with the inputs the feature names.
- **Attribution and replay.** Every call the piece made is in the trace log, attributed to both the human and the agent principal, and the run can be replayed from the log alone.
- **Cost and latency**, once the gateway exists: the request stayed inside the budget the configuration set.

## Layout

```
evals/
  README.md        this file
  conftest.py      shared fixtures, when there is something to fix
  test_<piece>.py  one file per piece, named after its feature
```

The suite is empty. When CI is added it will fail until the first eval exists, on purpose, so that the first green run is a real event rather than the default.
