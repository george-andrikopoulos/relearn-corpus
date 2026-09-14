+++
tag = "R:doc-currency"
title = "Update the doc in the same change as the thing it describes"
error_class = "A checked-in list or example (hygiene set, format sample, doc snippet) drifting from the reality it describes, so a reader trusts it and acts on stale guidance"
home = { kind = "global" }
created = "2026-07-16"
origin = "mined"
status = { kind = "active" }
authority = { kind = "local", version = 1 }
incident = "A checked-in list of a project's standard files still named an entry the workflow had moved on from, and a new project was scaffolded from that stale list — so the drift propagated into a repository that then had to be corrected. A document that lags what it describes is worse than no document: a reader trusts it and acts on it, and the more authoritative the document the further the stale guidance travels before anyone checks."
+++

When you change a process, format, or artifact, update every checked-in description of it -- list, example, doc snippet -- in the same change. A doc that lags the code it describes is worse than no doc: a reader trusts it and acts on stale guidance. The behavior contract and its examples are only load-bearing if they are true.

Not to be confused with R:revision-integrity, the sibling on a document's
*internal* consistency after an edit -- antecedents, cross-references, counts.
This rule is about a document's *external* currency: the text is self-consistent
and still describes a reality that has since moved. A file can pass one and fail
the other.

That sibling was named here in prose rather than by tag from 2026-08-16 until
2026-08-25, because it lived only in the `~/.claude` skill layer -- under the tag
this rule used to carry -- and a real citation would have dangled. It was ported
into this library on 2026-08-25, so the citation above is now a live reference
and this paragraph is the record of why it was not one before.
