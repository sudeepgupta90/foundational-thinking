# Foundational Principles

Two methods, codified from their primary sources.

- **[The Socratic Method](./socratic-method.md)** — Plato's early dialogues, c. 4th century BCE
- **[Scholastic Disputation](./scholastic-disputation.md)** — Abelard and Aquinas, 12th–13th century CE

These documents are the substrate. They carry the sources, the arguments, and the failure
modes, so that the skills in [`../skills/`](../skills/) can stay short enough to actually
be loaded and followed.

They are deliberately stable. The methods have been fixed for centuries; what changes with
experience is the *skill wording*, which is derived empirically from recorded agent
behavior — not from these documents.

---

## Which method, when

The two are not competing approaches to the same job. They handle opposite halves of
thinking, and each one fails badly in the other's territory.

| | **Socratic** | **Scholastic** |
|---|---|---|
| **Motion** | Dissolvent — takes a belief apart | Constructive — builds a defensible position |
| **Precondition** | A claim held with confidence | A question that is already well-formed |
| **Product** | *Aporia* — a better question | *Determinatio* — a decision that survived its objections |
| **Central move** | *Elenchus*: derive a contradiction from the holder's own premises | *Distinguo*: split the equivocal term the dispute was hiding |
| **Fails by** | Regress; questioning as obstruction; numbness with no reconstruction | Rigorously deciding a malformed question |

**Reach for Socratic** when the question is not yet worth answering: an abstract success
term nobody has defined, a diagnosis asserted as an observation, a goal with no
falsifiable success condition, a frame smuggled into a request.

**Reach for Scholastic** when the question is sharp and a decision is owed: two viable
options, a disagreement that needs adjudicating, a recommendation being challenged, a
decision that has to be written down and defended later.

### The overlap case

A request can carry both an undefined success term *and* a choice between named options —
*"we need a more maintainable state layer, Redux or Zustand?"* On the rule above, both
methods have a claim on it, and that ambiguity has produced a live routing bug: a forced
choice between two named options went to elenchus, on the ground that its success criteria
were still vague.

**It goes to disputation.** Once options are named, the *distinguo* is the instrument built
for exactly this: the equivocal term is split inside the determination rather than before
it, and the losing option is what forces the split into the open. Elenchus first would only
return the same choice with a longer preamble.

Socratic inquiry keeps the case where the undefined term stands alone with nothing yet to
choose between — which is where an agent will otherwise silently define the term for the
person who used it.

## How they chain

They compose in one direction:

```
ill-formed question ──Socratic──▶ well-formed question ──Scholastic──▶ determination
```

The elenchus produces the *utrum*. That is the handoff. Aporia is where the Socratic
method stops and where disputation can finally start, because a question that survives
elenchus is one whose terms are defined and whose premises have been made explicit — which
is exactly what the *utrum* requires.

Running them in the other order is the characteristic expensive mistake: a decision made
with full rigor, complete with steelmanned objections and careful replies, about a question
whose central term two parties were using in two different senses. The rigor makes the
wrong answer *more* persuasive.

**The three questions that route between them, in this order:**

1. *Are named options on the table?* If yes, **disputation** — even when the success
   criteria are still vague. The *distinguo* splits the equivocal term inside the
   determination.
2. *Otherwise: is a decision owed at all?* A disagreement to adjudicate, your own
   recommendation being challenged, a call that will be defended later. If yes,
   **disputation**.
3. *Otherwise: do we know what we are asking?* If no, **elenchus**. If yes, **neither
   method applies** — the question is well-formed and no decision is in dispute, so the
   request is for work. Do the work.

Question 1 comes first because it is the one that settles the overlap case; asking only
question 3 is the routing bug. Question 2 is what keeps question 3 from sending every
well-formed request to disputation: most requests are neither, and a method that fires on
everything is as broken as one that fires on nothing.
