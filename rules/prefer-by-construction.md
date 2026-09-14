+++
tag = "R:prefer-by-construction"
title = "Prefer by-construction impossibility over after-the-fact controls"
error_class = "Reaching for a runtime control (a check, a guard, a review step) to catch a mistake after it occurs when the design could have made that mistake impossible to express in the first place"
home = { kind = "global" }
created = "2026-08-13"
origin = "mined"
status = { kind = "active" }
authority = { kind = "local", version = 1 }
incident = "The recurring observation behind a family of rules rather than a single failure: the weaker the layer a guarantee lives at, the more it must be remembered. Making an illegal state unrepresentable is the type-level form; removing a deploy step so there is nothing to forget is the process form. A guarantee held by construction is the only one that survives the person who knew about it leaving, and every instance where one was held by prose instead has eventually been paid for."
+++

When a class of mistake can be designed out, design it out, rather than adding a control that catches it after the fact. A control that catches a mistake still admits the mistake; a design that cannot express the mistake retires the whole class. Rank the options by how little must be remembered for them to hold: a type the compiler enforces beats a test that samples beats a review step that relies on attention. R:make-illegal-states-unrepresentable is this rule in the type system.
