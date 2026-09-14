+++
tag = "R:attack-the-design-in-a-second-pass"
title = "Attack the design in a separate pass, and build nothing in it"
error_class = "Reviewing a design in the same pass that produced it, so the review inherits every assumption it was supposed to test -- the failure modes are never walked, the simpler alternative is never justified against, and the component ships with its author's confidence standing in for evidence"
home = { kind = "domain", name = "low-latency" }
applies_to = ["rust", "java"]
created = "2026-09-14"
origin = "codified"
status = { kind = "active" }
authority = { kind = "local", version = 1 }
incident = "Codified from standing practice rather than mined from a failure. It was found by reviewing a domain library before starting latency-sensitive work: the practice was called mandatory for exactly that kind of work and sat untagged in a single hand-maintained instruction file, so it could reach no other tool and no other rule could cite it. The practice: the pass that produced a design cannot review it, because the review inherits the assumptions it exists to test -- so the critique is a separate pass that builds nothing, justifies the choice against the simpler alternative, and walks the failure modes out loud."
+++

When a component is finished, do a second pass whose only job is to attack it. Build
nothing in that pass.

The pass that produced a design cannot review it. It carries every assumption that went
into the design, including the ones nobody stated, and it will read the output as
confirmation because that is what it was optimising for. A review folded into the build
is not a weak review; it is the build, wearing a different label.

So separate it in time and in intent, and give it something to do:

- **Justify the choice against the simpler alternative that was not taken.** Not "is this
  good" but "why not the obvious thing" -- and if the answer is that the obvious thing was
  never considered, that is the finding.
- **Walk the failure modes out loud.** Under what configuration does this do the thing it
  was chosen to prevent? What does it do under saturation, on a cold cache, on the first
  message after an idle period, when the peer is slow rather than absent?
- **Prove the stated constraint, do not restate it.** "It does not perturb the isolated
  cores" is a claim; the affinity mask, the thread inventory and the measurement are the
  proof. `[R:answer-the-requirement-at-its-layer]` is what this pass is usually checking.
- **Ask what the evidence would look like if the opposite were true.** An artefact that
  exists, a command that exited zero and a test that passed are all compatible with the
  work never having happened -- which is `[R:verdict-survives-the-channel]`, and it is the
  single most common thing this pass catches.

**Mandatory for anything latency-sensitive.** In that domain the failure does not announce
itself: a design that perturbs a neighbouring core, allocates on a send path, or faults a
page under load still passes every functional test, and the cost appears as unexplained
tail latency somewhere else entirely -- attributable to nothing, days later, by somebody
who was not there.
