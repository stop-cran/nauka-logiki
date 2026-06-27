# Review checklist & critique loop — *nauka-logiki*

Operational companion to `.github/copilot-instructions.md`. **Single source of truth** for two
roles: the **translator** self-checking *before submitting*, and the **`translation-reviewer-claude`** +
**`translation-reviewer-gpt`** agents (a two-vendor review pair).
Mirrors the English repo's `REVIEW.md`, plus a translation-specific section. Run every
round.

## The critique loop

1. **Translator** translates/edits an installment (only after its English is settled), runs the
   mechanical checker, submits.
2. **Reviewer** — ideally a *different model*; cross-model rounds reliably catch what a single
   model misses — critiques against this file and the settled English counterpart.
3. **Translator** applies genuine fixes *with judgment*, **holds** the rest *with explicit
   rationale*, propagates any canon change to all installments and both READMEs, re-runs the
   checker, and **verifies**.
4. Repeat until a round is **clean**: no Blocker / High / Medium findings and all mechanical
   gates green. **Stop condition:** once a round yields only **Low / Optional single-word polish**,
   the translation is *settled* — don't spin further rounds chasing taste (diminishing returns).

Never batch ahead of the author's authorization.

**Rotate reviewer models across rounds.** Use at least two *different vendors* (e.g. Claude + GPT +
Gemini) over a piece's review life: a **cross-model** pass catches canon and grammar errors a
same-model pass tends to *rationalize away* (a cross-model pass caught «степенное отношение» and
«категориальный дом»); a **same-model regression** pass catches consistency drift from the previous
round's own edits. Run reviewers at high/xhigh reasoning with long context (the full translation +
settled English + every cross-referenced sibling + both READMEs at once). Enforce routing
operationally where the interface supports it (Copilot CLI `/subagents`, `/model`); otherwise rotation
is a manual discipline.

**Рецензент ≠ модель автора — твёрдый инвариант.** Модель рецензента должна отличаться от модели,
которой выпуск был *написан*; иначе это однопроходная проверка той же моделью, теряющая весь смысл
кросс-модельной вычитки. Маршрутизация закреплена в репозитории в `.github/copilot/settings.json`
(`subagents.agents.<name>`): **два** рецензента, каждый на своём вендоре — `translation-reviewer-claude`
(Opus) и `translation-reviewer-gpt` (GPT-5.5), оба при `xhigh` + `long_context`. У них разделение труда
— Claude чаще ловит структуру, перенос канона и регрессионный дрейф; GPT — идиоматику и качество
перевода, — поэтому при первой вычитке запускай **обоих** (проход вширь), а затем, после правок, —
одновендорный **регрессионный** проход, пока раунд не станет чистым. Сменив вендора автора через
`/model`, переключи модели так, чтобы автор не совпал ни с одним рецензентом.

## How to review (discipline)

- Review the **current** file, not a remembered one. Prefer a **word-diff against the
  last-reviewed commit**: `git --no-pager diff --word-diff=plain <prev>..HEAD -- <file>`.
- After fixes are applied, **re-read** the changed spans and **verify** — don't assume.
- Tier every finding by severity; mark each a **fix** or a **hold (rationale)**.
- You are **review-only**: report; the translator edits.

## 1 — Mechanical gates (must be green)

Run from the repo root (resolves `markdown-it` from the sibling `science-of-logic` repo if it
isn't installed locally):

```
node tools/check-synopsis.js
```

For every Section III installment (NN ≥ 10) it checks: **abstract = a single outer `<em>` span**
(a trailing `**bold**` term or stray `*` dropping outside the span is the usual cause); section
skeleton `## I.` … `## Кода`; **no LaTeX math**; a **README entry** links the file. It also enforces
the **canon denylist** (`tools/canon-denylist.json`) across installments **and** the README — locked
terms like «степенное отношение», «дом/седалище» (→ «средоточие»), «впечатлительный», stray `ℏ` fail
mechanically. Wire it to run on every commit: `git config core.hooksPath .githooks` (runs the
committed `.githooks/pre-commit`).

## 2 — Translation review (RU-specific)

- **Mirror the settled English exactly**: same structure (`## I.`–`## IX.` + `## Кода`), the same
  single-`<em>` abstract, the same `§NN` cross-references, the same italic-plain math.
- **Locked-terminology canon** (see `.github/copilot-instructions.md`). A change to any canon term
  must propagate to **all** installments **and both READMEs** — the retrofit ripple (e.g.
  «отношение степеней» not «степенное»; home/seat → «средоточие» not «дом»/«седалище»).
- **False-friend watchlist** (recurring traps):
  - «явление» collides with the Hegelian category *Явление / Appearance* → use «проявление» for
    "exhibition / manifestation".
  - «целое» = *integer* near math → «единое целое» for *das Ganze*.
  - «впечатлительный» = *impressionable*, **not** "impressionistic" → «по впечатлению».
  - «определитель» = *matrix determinant* → «определяющий принцип отношения» for *Exponent*.
  - «содержится» = *has content*, **not** *is restrained* → «сдерживается / удерживается».
  - «сваренный» → «спаянный» for "welded to a quality".
- **Register markers** to preserve: указует, счисляется, зараз, надолго отложенное.
- **EN ↔ RU parallelism**: README entries and abstracts stay parallel.
- **Improvements over the English** (a clearer phrasing, a corrected fact) must be **fed back to
  the English**, never left as a silent divergence.

## 3 — Consistency & fidelity

- Cross-references (§NN threads, ordinal counts) accurate against the cited installments.
- Categorial-not-empirical guardrail preserved wherever physics appears.

## Severity rubric

- **Blocker** — breaks a mechanical gate, factual error, or canon violation.
- **High** — mistranslation, fidelity error, broken cross-reference.
- **Medium** — terminology drift, register slip, inconsistency with a sibling installment.
- **Low** — idiom, grammar, polish.
- **Optional** — taste; offer, don't press.

## Review output format

1. **Verdict** — publishable? any blockers?
2. **Verified ✓** — the gates and spot-checks you actually ran (incl. EN↔RU mirror).
3. **Findings** — grouped by severity, each marked *fix* or *hold (rationale)*.
4. **Questions** — judgment calls for the author.
5. **Handoff** — the author applies the agreed fixes; offer to re-review the next iteration.
