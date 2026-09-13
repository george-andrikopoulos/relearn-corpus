+++
tag = "R:wired-artifact"
title = "A success check consumes a sentinel nothing else can produce"
error_class = "A check that runs, passes, and accepts forgeable evidence -- a date, a header, a log echo, a file's existence, a component's own unit tests -- so an inert or failed thing certifies as working and the check's greenness is what conceals it"
home = { kind = "global" }
created = "2026-07-20"
origin = "mined"
status = { kind = "active" }
authority = { kind = "local", version = 1 }
incident = "Two types shipped in a release with five unit tests each and sat unwired for two months. The tests proved the types worked; nothing proved anything produced or consumed them, and the first behaviour contract cited those tests as the enforcing artefact -- so an inert feature read as an enforced one. A sharper second instance followed: a review wrapper decided success by searching for a date, matched a header its own generator had just written, and cleared the review-due flag on a run that had failed. Evidence a check produces itself is not evidence."
+++

A success check must consume a write-once sentinel that is unique to the artefact class it verifies, emitted as the final act of the success path, and producible by nothing else in the system. Pattern-matching on a date, a header, a log line, or the presence of a file is not verification -- it is a check that something happened, which is a different claim from the one being made.

Ask before wiring any check: *what else in this system can produce the string my check accepts?* If the answer is anything at all, the check accepts forgery, and it will accept it silently on the day it matters -- because the failure path is the one that regenerates headers and re-emits dates.

The same test applies to enforcement claimed on a component: *what produces this, what consumes it, and does the cited artefact cross that seam?* If nothing crosses it, the feature is inert and the honest ledger entry says so rather than naming the component's own tests.

A green check that cannot fail is worse than no check. It converts an open question into a settled one, so nobody looks again, and the thing it was protecting degrades behind a signal that says it is fine. This is the type-level and tooling-level sibling of R:verify-through-production-path, and it shares a family with R:guarantee-needs-a-reader: that rule fires when nothing enforces the claim, this one when something does and accepts the wrong evidence.
