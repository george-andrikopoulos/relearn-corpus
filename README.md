# relearn-corpus

A shared rule corpus. Installs publish into it and take copies from it; nothing
runs here but a recompute.

It is **a directory, not a service**. There is no server, no account, no API. An
install addresses it by path — a common drive, a mounted share, or a clone of
this repository — and `relearn` never speaks to it over a network. That is not a
simplification to be outgrown: `tests/solo_mode.rs` in the tool fails the build
on a socket, a spawned process, an ambient read or a networking crate anywhere
in the tree, so the shape cannot drift.

## Layout

```
rules/            contributed rules, one file per tag
reports/          one anonymous recurrence report per install, named by its pseudonym
aggregate.toml    the recompute over reports/, written by a scheduled job
```

## Publishing a rule into it

```sh
relearn contribute --rules <your-rules> --tag R:some-rule \
    --terms <your-term-list> --version 1 --out <this>/rules --confirm
```

Two things that will stop you, and both are the point.

**A rule needs a `published_incident` before it can be published.** A rule's
`incident` is a verbatim quotation from a private working session — it names
people, dates, repositories and paths, and it may never travel. What travels is
a separate field you write by hand: the error class, what went wrong, and what
it cost, with no quotation and no identifiers. Nothing derives one from the
other, and nothing ever should — an automatic scrubber leaks what it did not
recognise and, worse, stops people reading the output because something appears
to be handling it.

**A republication must go forwards.** `--version` says which revision you are
publishing, and a revision at or below the one already here is refused. Every
install holding a copy decides staleness by comparing those two numbers, so
going backwards would make every copy read as current forever — and the check
that would have caught it is exactly the comparison that had been corrupted.

A rule whose home never leaves a machine cannot be published at all: a project
home names a filesystem path, and an org layer is an organisation's own.

## Taking rules from it

```sh
# What would change here? Writes nothing — run this before starting work.
relearn pull --rules <your-rules> --upstream <this> --all --from corpus --on <date>

# Apply it, dropping caches that are gone or retired upstream.
relearn pull --rules <your-rules> --upstream <this> --all --prune \
    --from corpus --on <date> --confirm
```

A rule you take is a **cache**: it compiles into your instruction layer exactly
like your own rules, because it keeps the home it arrived with, but it is not
yours to edit and the write path refuses. To change one, `adopt` it — a
deliberate fork that records what it came from — or contribute the change back.

`--scope` bounds what a bulk pull takes, so a corpus can grow past what any one
install wants to compile.

## Reporting recurrences

Anonymous, always. A report carries an upstream tag, a bucketed count, a
month-level date, a status kind and a control kind — no title, no incident, no
body, no path, no name, and no day-level date anywhere. Recurrence is somebody
writing down that a rule of theirs failed, and nobody does that with their name
on it.

```sh
relearn report --rules <your-rules> --aggregate <this> \
    --generated 2026-09 --install <8 hex chars> --confirm
```

Your pseudonym is the filename in `reports/`, and it lives **here rather than on
your machine** — delete your clone and the pseudonym is gone. Type `--install`
once; after that this directory supplies it.

**The aggregate publishes nothing about a rule until five distinct installs have
reported it**, and below that floor the rule does not appear at all — not its
count and not its tag, because naming a rule while withholding its number points
at the same person. One person filing under two pseudonyms is the obvious way to
fake that population, and it is the thing the floor exists to detect: please
don't.

## The recompute

```sh
relearn aggregate --clone <this> --generated 2026-09 --confirm
```

Run on a schedule; commit the result. It reads only this directory — there is no
fetch and there must never be one. Every published figure carries both confounds
beside it, unconditionally: cross-install recurrence measures frequency *and*
diligence inseparably, and it counts only classes somebody has published a rule
for, which is a bias toward the cheap incidents rather than mere sparseness.

## Status

**Forty-five rules, one contributor, no reports.** That is every rule its
contributor holds that *can* travel: the rest are homed to an organisation or to
a project, and those never leave a machine in either direction. Each published
incident was written by hand — the raw ones quote private working sessions and
name people, repositories, products and paths, and none of that crossed.

**Twenty of the forty-five are `codified`, and have never been observed to fire.**
That is not a defect in them, and it is the number to read first: a rule written
down from standing practice has prevented nothing yet that anyone has measured,
and a corpus made mostly of them would be sharing doctrine rather than
experience. `relearn lint` prints it beside the recurrence count for that reason.

**One dangling citation survives and cannot be published away.** A rule here
cites one that is homed to a project, so no corpus can ever carry it. A
subscriber sees it as a dangling reference, and the default lint threshold makes
that fatal — run `lint --deny error`, or ask the contributor whether the cited
rule was ever really project-specific.

**No install has reported a recurrence, and `aggregate.toml` does not exist yet.**
The floor is five distinct installs and there is one, so there is nothing the
aggregate could honestly publish. That is the measurement working, not a gap.

Publishing more is writing, not running: each rule needs its published incident
authored by the person whose session produced it, and that is the real cost of a
shared corpus.
