# Copilot instructions — *nauka-logiki*

## What this repository is

The **Russian translation** of the English Hegel synopsis kept in the sibling repository
**science-of-logic**. Each file in `конспект/NN-*.md` mirrors the corresponding English
installment in structure, argument, and house style. The translation is faithful and
preserves an elevated, slightly archaic academic register (in the tradition of E. Ilyenkov
and the Lenin notebooks).

## Workflow (do not skip or reorder)

Translate an installment **only after** its English counterpart is settled. Then:

1. Translate into `конспект/`, mirroring the English structure exactly.
2. Submit for review; expect **multiple rounds**, often cross-model.
3. Apply feedback **with judgment** (see below).
4. Commit and push, GPG-signed.

Mirror the English file precisely: abstract as a single `*…*` span, `## I.`–`## N` (contiguous Roman
run, N varies) +
`## Кода`, and the same `§NN` cross-references. The author reviews each piece before
authorizing the next — **never batch ahead**.

**Review process.** Translators self-check and reviewers critique against `REVIEW.md` (the
checklist, false-friend watchlist, severity rubric, and critique loop). Run the mechanical gate
before submitting: `node tools/check-synopsis.js` (resolves `markdown-it` from the sibling
`science-of-logic` repo if not installed locally). The `translation-reviewer-claude` and
`translation-reviewer-gpt` custom agents in
`.github/agents/` encode the review-only reviewer role (a two-vendor pair).

## Handling review feedback

Apply genuine idiom/grammar/precision fixes, but **hold** suggestions that conflict with
fidelity, the locked terminology, or the chosen register — **always with an explicit
rationale**. Principled, reasoned holds are preferred over blanket acceptance.

## Locked terminology (canon — keep consistent across all installments)

квант (*Quantum*); число / численность (*Anzahl*) / единица (*Einheit*);
отношение (*Verhältnis*); **показатель** (*Exponent*); прямое / обратное отношение;
**отношение степеней** (*Potenzenverhältnis*, not «степенное»); градус (*Grad*);
**граница** (*Grenze*) vs **предел** (*Schranke*); дурная / истинная бесконечность;
асимптота; **снятие / снять** (*Aufhebung*); **Мера** (*Maß*);
**узловая линия отношений меры** (*Knotenlinie*); **безмерное** (*das Maßlose*);
Сущность (*Essence*); **переход** (*Übergehen*) vs **просвечивание** (*Scheinen*);
квант действия; «второй подкруг Учения о Бытии» for the sphere of Quantity.

Translation decisions to keep:

- Hegel's "whole" (*das Ganze*) → **«единое целое»** when it sits next to numeric/mathematical
  language, to avoid collision with «целое (число)» = integer. The adjective-qualified
  «…целое» (утвердительное / само-соотнесённое / ограничивающее) is fine as-is.
- "contained / held" in the sense of *restrained* → **«сдерживается / удерживается»**, never
  «содержится» (= has content).
- Figurative "bedrock" → **«коренное основание»**, not the calque «коренная порода».
- "welded to a quality" → **«спаянный»** (not «сваренный»).
- "determinant of the ratio" → **«определяющий принцип отношения»** (avoid «определитель» =
  matrix determinant, a false friend).
- "seat / home" of a category → **«средоточие»** (not «седалище», anatomical connotation).
- Archaic-register markers to preserve: **указует, счисляется, зараз** (atemporal "at once"),
  надолго отложенное.

## House style / commits

Same as the English repo: single-italic-span abstract, italic-plain math (not LaTeX),
`§NN` cross-references, and a `README.md` index **kept parallel with the English README**.

- **GPG-sign every commit** (`-S`). Signing program: `C:/Program Files/GnuPG/bin/gpg.exe`.
- Author: `Roman Konstantinovskiy <stop-cran@list.ru>`.
- Trailer: `Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>`.
- Stage only `.md` / `README.md`; do not stage build artifacts.
- Use the literal `§` character in commit messages.
- Verify after committing: `git log --pretty="%h %G? %s" -1` should show `G`.
