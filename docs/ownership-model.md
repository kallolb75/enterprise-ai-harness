# The ownership model

What an enterprise has to own in the harness, what it can rent, and what "partners can help" means when the wheel stays with the enterprise.

## The claim

An enterprise that runs a model in production already has a harness. Most built it by accident, one copilot at a time: the context is whatever got pasted into a prompt, the orchestration is glue code, the governance is an email that said "looks good". That harness leaks in three places. The vendor's platform, which now holds the workflow logic. The employee who leaves and takes the unwritten judgment with them. The run that made a decision and left no log.

Owning the harness means those three leaks are closed on purpose. It comes down to four things.

## The four things the enterprise owns

**The context.** The data the agent is allowed to know, where it lives, who curates it, and the rules that sit on top of it. This is the part a vendor is least able to supply and most eager to hold.

**The workflow logic.** Which agent runs for which request, which tool it may call, which system it may write to, and in what order. If this lives in a vendor's product, the vendor owns the business process.

**The telemetry.** Every retrieval, every tool call, every decision, in an event format the enterprise designed, kept where the enterprise can replay it. A regulator will ask about a decision; the answer has to come from your log, not the vendor's dashboard.

**The freedom to swap the model.** The model is a configuration setting. Changing it is a config change and an eval run, never a rewrite. This is the test of whether the other three are real: if swapping the model is hard, something that should have been yours has leaked into the model layer.

## What can be rented

The model. The hosting. The hands that help build the harness. Tooling that sits inside a layer without owning it (a vector store, a queue, a gateway product) as long as the four things above stay yours and leaving the product is a documented, tested path.

## What "driver's seat" means

Partners can design with you, build with you, and run parts of it for you. Three things do not transfer.

1. The context and the workflow logic are written down in your repo, in a form your own people can read and change.
2. The decision records are yours. A partner can propose a decision; the enterprise accepts it, and the record says who.
3. Someone on your side can explain every line that shipped. If nobody can, the build has been outsourced whatever the contract says.

## How this repo exercises the claim

Each of the four things has a piece of this build whose spec exists before its code:

| Owned thing | Piece | Spec |
|---|---|---|
| Freedom to swap the model | Model gateway | specs/gateway.feature |
| Workflow logic | One MCP server in front of one real system, with its own auth and schema | specs/mcp_server.feature |
| Telemetry | Trace log in an event schema this repo wrote, replayable | specs/trace.feature |
| All four, tested | Eval suite, the definition of done | evals/ |

The context layer arrives as a later ring, once a workflow asks for it. Starting with retrieval before the gateway, the log and the evals exist is how accidental harnesses get built.

## What this document does not claim

It does not claim an enterprise should build its own model, its own cloud or its own agent framework. It does not claim every enterprise needs every layer at the same depth. It claims that the four things above are the enterprise's to own, and that the harness is the place where they live.
