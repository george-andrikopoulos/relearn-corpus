+++
tag = "R:guarantee-needs-a-reader"
title = "A stated guarantee names what enforces it, or is deleted"
error_class = "A safety claim written in prose -- a header comment, a docstring, a promise in a readme, a ledger line -- with nothing in the system reading the state it asserts, so the sentence stops people looking at the very thing it fails to protect"
home = { kind = "global" }
created = "2026-08-16"
origin = "mined"
status = { kind = "active" }
authority = { kind = "local", version = 1 }
incident = "A one-time sweep answered a question about a repository, and a sentence recording the all-clear was written into a document. Six weeks later the thing the sweep had looked for was present both in the working tree and through most of the repository's history. Nothing in the system read the state that sentence asserted, and it was believed precisely because it was written down, which is what stopped anyone looking again. The sweep did not produce a control and the sentence was not one; the control that eventually held it reads the state on every push."
+++

Every safety claim in prose names the line, test, or check that enforces it -- or the sentence is deleted. A guarantee with no reader is worse than no guarantee, because it is read as coverage and it ends the inquiry.

A claim of completeness must also state what the check actually consumed. Not "verified", but "verified by grepping `model:` across N agent files" -- so the gap between the scope of the check and the scope of the claim is visible on the face of the entry rather than reconstructable only by rerunning it. Most false completeness claims are not lies; they are a narrow check reported in wide language.

**Error paths are where these hide.** A message asserting a state must be produced by *checking that state*, not by which branch printed it. The failure path is the one nobody exercises, so a confident sentence with nothing behind it survives there longest, and it is read at exactly the moment the reader is least able to question it. Ask of every error message: *did anything read the world before this printed?*

Where a mechanical reader exists, use it and leave the prose to what it cannot see: an unread binding is already a hard error under a compiler run with warnings denied. What no linter can see is a true-looking sentence with nothing behind it, and that is what this rule is for.

The test: *what would have to be true for this sentence to be false, and what reads that?* R:wired-artifact is the neighbouring failure -- there a check exists and accepts forgeable evidence; here there is no check at all.
