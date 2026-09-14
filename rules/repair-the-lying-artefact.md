+++
tag = "R:repair-the-lying-artefact"
title = "Repair the artefact that made the false claim, not only the doc about it"
error_class = "Closing an incident by writing or correcting prose while the executable artefact that actually misled — a script's printed path, a status line, a generated header, a success message — goes on emitting the same false claim, so the defect stays fully operational behind a note that makes it look handled"
home = { kind = "global" }
created = "2026-08-24"
origin = "mined"
status = { kind = "active" }
authority = { kind = "local", version = 1 }
incident = "Twice from one cause. A release build was smoke-tested against a binary at the conventional output path, which reported an old version and two missing routes — read as three regressions in a fresh build, and all in fact properties of a four-month-old binary the build had never touched, because the machine redirected build output elsewhere. The first fix was a paragraph in the project charter naming the incident and printing the command that resolves the path properly. The same thing happened again eight days later, because a paragraph is not a control: the artefact went on lying, and only a check that reads the real path could stop it."
+++

When an incident traces to a false claim, find the artefact the person was actually
reading at the moment they were misled, and repair **that** first. Usually it is not the
document — it is something that printed during the work: a script's final "Binary:" line,
a deploy script's success message, a generated file's header, a status endpoint, a test
name. A document is consulted; an artefact is *emitted at you* while your attention is on
the task. That asymmetry decides who gets believed.

A doc and a script disagreeing is not a tie. People run the script. Correcting the doc and
stopping there leaves the defect fully operational and adds a paragraph that makes it look
handled — the worst of both, because the next occurrence now has a written warning standing
over it as evidence that someone already dealt with this.

Apply the test before closing: **could the same person be misled again in exactly the same
way without ever opening the document I just fixed?** If yes, the fix has not landed. Ask
also what else in the repo asserts this same fact — a README snippet, a CI summary, a
printed usage line — because a claim usually has more than one mouth.

Then push it down a layer rather than restating it: make the artefact *derive* what it
reports instead of asserting it (resolve the path, stat the file, read the version it
actually built), and add the mechanical check that fails any future artefact making the
unresolved claim. Deriving beats asserting for the same reason
`[R:prefer-by-construction]` prefers designs to guards — a derived claim cannot drift from
what it describes, so it cannot go stale the way `[R:doc-currency]` describes.

This is the reporting half of `[R:verify-through-production-path]`. That rule says to
exercise the real channel; this one says the real channel must also tell the truth about
what it produced — verifying through a production path that reports a path it never
resolved proves nothing.
