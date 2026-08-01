# foundational-thinking

Two methods of critical thinking, fixed for centuries, codified here as agent skills:
the **Socratic method** and **Scholastic disputation**. Both are packaged for Claude
Code, Gemini CLI, and Codex.

## What this is

Plato's early dialogues and Aquinas's *Summa Theologiae* already solved two different
halves of the thinking problem: how to take a confidently-held but ill-formed belief apart
(Socratic), and how to build a decision that survives its strongest objections
(Scholastic). This repo codifies the underlying principles once, in
[`principles/`](principles/), and derives from them two short, loadable agent skills in
[`skills/`](skills/). The principles are the stable substrate; the skill wording is tuned
empirically against recorded agent behavior — see [Provenance](#provenance) below.

## The two skills

### `socratic-inquiry`

> Use when a request turns on an abstract quality word — reliable, scalable, secure,
> robust, maintainable, clean, fast, simple, better, production-ready — and nobody has said
> what would count as achieving it, so acting would mean deciding for yourself what the
> word means. Also use when a cause is asserted rather than demonstrated ("the bug is X, go
> fix X"), or when a question presupposes its own answer. Not for choosing between named
> options — that is `scholastic-disputation`.

Dissolvent: takes an ill-formed belief or request apart before any work is done on it.
Produces *aporia* — a better question, with its terms defined. See
[`principles/socratic-method.md`](principles/socratic-method.md) and
[`skills/socratic-inquiry/SKILL.md`](skills/socratic-inquiry/SKILL.md).

### `scholastic-disputation`

> Use when a choice between two or more named options is owed — "X or Y?", "which should we
> use?", "we need to pick one" — including when their success criteria are still vague.
> Also use when adjudicating conflicting reports or recommendations, when your own
> recommendation is challenged or overruled, when writing up a decision that will be
> defended later, or when you are about to give a verdict without having stated the losing
> case.

Constructive: builds a defensible position by stating the strongest opposing case first,
then deciding. Produces *determinatio* — a decision that survived its objections. See
[`principles/scholastic-disputation.md`](principles/scholastic-disputation.md) and
[`skills/scholastic-disputation/SKILL.md`](skills/scholastic-disputation/SKILL.md).

The two are not interchangeable: running disputation on a question whose terms are still
equivocal produces a rigorously-argued wrong answer. The one case that needs a stated rule
is the overlap — *"we need a more maintainable state layer, Redux or Zustand?"* has both an
undefined quality word and a named choice. **A choice between named options goes to
disputation even when the criteria are vague**; the *distinguo* is where the equivocal term
gets split, so the method has somewhere to put it. Socratic inquiry is for the undefined
term when there is no choice on the table. See [`principles/README.md`](principles/README.md)
for the full routing logic and how the methods chain (`ill-formed question → Socratic →
well-formed question → Scholastic → determination`).

## Install

The remote-URL forms below assume the repo is published at
`github.com/sudeepgupta90/foundational-thinking`; until then, use the local-path or manual
routes. Whether the skills are *discovered* inside a live installed session — as opposed to
inside a simulated harness, which is where discovery was tested — is untested on all three
runtimes. The manual copy is the route with the fewest moving parts if a plugin install
does not surface both skills.

### Claude Code (plugin)

From this repo's directory:

```
/plugin marketplace add /path/to/foundational-thinking
/plugin install foundational-thinking
```

Or point `/plugin marketplace add` at the GitHub repo once published
(`sudeepgupta90/foundational-thinking`).

### Gemini CLI (extension)

[`gemini-extension.json`](gemini-extension.json) at the repo root makes this an extension:

```
gemini extensions install https://github.com/sudeepgupta90/foundational-thinking
```

[`GEMINI.md`](GEMINI.md) is declared as the extension's `contextFileName`, so the two skill
descriptions are in context from session start and the bodies load on demand. That file is
loaded in whatever directory the session starts in, which is not where the skills are, so
it names `skills/` and `principles/README.md` relative to the extension's install directory
(`~/.gemini/extensions/foundational-thinking/`) rather than linking to them.

The manifest declares no skills path — unlike the Codex one — on the expectation that
Gemini CLI discovers `skills/` from the extension root by itself. That has not been
verified against a live install. If both skills do not show up, use the manual copy below.

### Codex (plugin)

[`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) declares `"skills": "./skills/"`,
which is what a Codex plugin needs to expose both skills.

**Use the manual copy below.** The only marketplace manifest in this repo is
[`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json), which is Claude Code's;
there is no equivalent under `.codex-plugin/`, so a `/plugin marketplace add` pointed at
this repo has nothing to resolve from Codex. The plugin manifest is shipped so that the repo
is ready to be listed once a Codex marketplace source exists, but no Codex install path has
been verified here.

### Manual copy

Any runtime that reads skills from a directory can use these without the plugin machinery.
Copy or symlink both skill directories into wherever that runtime looks — `~/.claude/skills/`,
`~/.codex/skills/`, or the cross-runtime `~/.agents/skills/`:

```
ln -s "$PWD/skills/socratic-inquiry"       ~/.codex/skills/socratic-inquiry
ln -s "$PWD/skills/scholastic-disputation" ~/.codex/skills/scholastic-disputation
```

Install by exactly one route per runtime. A manual copy alongside a plugin install puts two
skills with the same `name` in front of the same agent.

## Repo layout

```
.
├── skills/                         the two loadable skills — self-contained
│   ├── socratic-inquiry/           SKILL.md + references/
│   └── scholastic-disputation/     SKILL.md + references/
│
├── principles/                     sources, arguments, failure modes
│   ├── README.md                   which method when, and how the two chain
│   ├── socratic-method.md
│   └── scholastic-disputation.md
│
├── .claude-plugin/                 Claude Code plugin + marketplace manifests
├── .codex-plugin/                  Codex plugin manifest
├── gemini-extension.json           Gemini CLI extension manifest
│
├── GEMINI.md                       loaded from session start (Gemini extension)
├── CLAUDE.md                       same content, for work inside this repo
├── AGENTS.md                       same content, cross-tool convention
├── charter.md                      the original problem statement
├── README.md
└── LICENSE
```

Two things worth stating, because both are easy to assume and neither is true. Nothing in
`skills/` links into `principles/` — the skills are self-contained, and the principles are
there to be read by people. And a plugin's root `CLAUDE.md` is *not* loaded as context by a
Claude Code install, so `GEMINI.md` is the only one of the three that a runtime picks up on
its own.

## Provenance

The skill wording in `skills/` is not a paraphrase of the principles documents. It was
derived empirically. Each scenario was first run against a fresh agent with **no skill
loaded**, and the failure it actually produced was recorded. Skill content exists only
where such a run showed a real failure — guidance without a demonstrated failure is
treated as bloat rather than added. Three of the eight baseline scenarios showed no failure
and therefore contributed nothing to either skill. A fourth, socratic-01, passed on
substance but asked its clarifying question *after* committing to work; that ordering
defect is the only thing it contributed.

The skills were then re-run against *fresh* scenarios — not the baseline ones — against
no-skill controls, which is where one leak took two attempts to close. A third set of runs
covers the separate question of whether a skill *fires* at all, since the `description`
field is the whole trigger; it caught a routing bug where a decision between two named
options was being claimed by the wrong skill.

Results that contradicted the authors' predictions are recorded alongside the ones that
confirmed them.

**The run records are not published with this repo.** They state each scenario's expected
behavior, and an agent that can read them is no longer the unaided agent every one of these
measurements depends on.

## License

MIT. See [`LICENSE`](LICENSE).
