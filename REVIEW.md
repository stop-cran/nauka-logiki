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

**Вставки в готовый текст возвращают раунд к началу.** Позднее добавление в уже вычитанный выпуск —
глосса, цитата, абзац в ответ на вопрос автора — **считается сломанным, пока пара рецензентов его
не увидела**. Это самый надёжный источник дефектов в проекте: из четырёх добавлений к §25 одно было
вырезано целиком, три переписаны за два раунда. Типичная беда не ложь, а **столкновение**: вставка
повторяет то, что готовый текст говорит ниже и лучше, и они начинают расходиться — о характере, о
причине или об **уровне** одного и того же хода (черновик §25 вёл абсолютизированный случай *вниз*,
в формальную необходимость, тогда как готовый текст и Кода ведут его *вверх*, в абсолютную).
**Режь, а не латай.**

**Верное возражение ещё не требует новой прозы.** Сильнейший вид этой беды — вставка философски
*правая* и всё же непечатная, ибо возражение, на какое она отвечает, уже отведено в другом месте
выпуска. Прежде чем писать, ищи ответ в самом файле; если он там, всё средство есть одно
предложение, указывающее на него.

**Схождение двух рецензентов есть знак достоверности** — в том числе когда оба говорят «вырезать»;
**расхождение — знак идти к источнику или считать по корпусу**, а не выбирать рецензента (обычно
каждый прав наполовину, а иногда верное средство не принадлежит ни одному из них).

**Rotate reviewer models across rounds.** Use at least two *different vendors* (e.g. Claude + GPT +
Gemini) over a piece's review life: a **cross-model** pass catches canon and grammar errors a
same-model pass tends to *rationalize away* (a cross-model pass caught «степенное отношение» and
«категориальный дом»); a **same-model regression** pass catches consistency drift from the previous
round's own edits. Run reviewers at high/xhigh reasoning with long context (the full translation +
settled English + every cross-referenced sibling + both READMEs at once). Enforce routing
operationally where the interface supports it (Copilot CLI `/subagents`, `/model`); otherwise rotation
is a manual discipline.

**Хотя бы один рецензент ≠ модель автора.** При первой вычитке (проход вширь) хотя бы один рецензент
должен отличаться от модели, которой выпуск был *написан*; одновендорный рецензент всё равно полезен
как **регрессионный / дополнительный** проход (ловит дрейф, внесённый правками прошлого раунда).
Закреплённая пара Claude + GPT гарантирует это для черновика, написанного на GPT, Claude или Gemini:
каким бы вендором ни писал автор, хотя бы один из двух рецензентов отличается. Маршрутизация —
**единственный источник истины** в `.github/copilot/settings.json` (`subagents.agents.<name>`):
`translation-reviewer-claude` (Claude Opus 5) и `translation-reviewer-gpt` (GPT-5.6 Sol), оба при `xhigh` +
`long_context`. У них разделение труда — Claude чаще ловит структуру, перенос канона и регрессионный
дрейф; GPT — идиоматику и качество перевода, — поэтому при первой вычитке запускай **обоих** (проход
вширь), а затем, после правок, — одновендорный **регрессионный** проход, пока раунд не станет чистым.
Добавь третьего агента на Gemini как тай-брейкер / гарантированный кросс-модельный проход, когда автор
сам на GPT или Claude.

## How to review (discipline)

- Review the **current** file, not a remembered one. Prefer a **word-diff against the
  last-reviewed commit**: `git --no-pager diff --word-diff=plain <prev>..HEAD -- <file>`.
- After fixes are applied, **re-read** the changed spans and **verify** — don't assume.
- When introducing a **new rendering of a recurring phrase**, check how the **settled siblings**
  already render it (the mirror of retrofit-ripple): e.g. "the claim is categorial" was settled as
  «утверждение … категориальное» in §18, so §19 had to match it, not invent «притязание».
- An optional **cold / no-context reviewer pass** (a reviewer given only the file, no project
  framing) is worth running once per piece: it reliably catches false friends, register slips, and
  over-reach that the project-anchored reviewers read past (it caught «подлежит»/«притязание» here).
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

**Плюс разбор зеркальности — чекер его не делает.** Строки соответствуют английскому 1:1, поэтому
расхождение считается механически. Прогоняй перед каждым коммитом (PowerShell):

```powershell
$en='..\science-of-logic\synopsis\NN-....md'; $ru='.\конспект\NN-....md'
$e=[System.IO.File]::ReadAllText($en) -replace "`r`n","`n" -split "`n"
$b=[System.IO.File]::ReadAllBytes($ru)
$r=[System.Text.Encoding]::UTF8.GetString($b) -replace "`r`n","`n" -split "`n"
for($i=0;$i -lt $e.Count;$i++){
  $eb=([regex]::Matches($e[$i],'\*\*')).Count; $rb=([regex]::Matches($r[$i],'\*\*')).Count
  $es=(([regex]::Matches($e[$i],'§\d+'))|%{$_.Value}|Sort-Object -Unique) -join ','
  $rs=(([regex]::Matches($r[$i],'§\d+'))|%{$_.Value}|Sort-Object -Unique) -join ','
  if($eb -ne $rb -or $es -ne $rs){ "L$($i+1): bold EN=$eb RU=$rb | EN=[$es] RU=[$rs]" }
}
```

Должно быть: равное число строк, ноль расхождений, и целость файла — **только CRLF, ни одного
одиночного LF, без BOM**. Этот разбор ловит то, чего не ловит чтение: им был пойман лишний жирный
«**Кант**» в §25, какого нет в подлиннике (эмфаза протекла в файл из рабочей переписки). Правь
только побайтово — в `README.md` есть застарелый одиночный CR.

## 2 — Translation review (RU-specific)

- **Mirror the settled English exactly**: same structure (`## I.`–`## N` contiguous Roman run + `## Кода`), the same
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
  - «подлежит» = *is subject to*, **not** "underlies" → «лежит под / лежит в основе».
  - «кажущая / кажущийся» = *seeming*, **not** "shows itself" → «показывает себя» (for *Scheinen*).
- **Двусмысленности, каких английский не допускает** (проверяй в каждой новой вставке):
  - **обратная агентность в придаточном** — «какое производит сам непокой случайности» по
    умолчанию читается наоборот (им. = вин. и у «какое», и у «непокой»); для «X порождает Y»
    ставь страдательный залог с творительным: «какое производится самим беспокойством»;
  - **голые отглагольные существительные** — «обращение» (переворот / обращение к),
    «признание» (признание / исповедь): бери однозначное слово, тем более если соседний выпуск
    приучил к другому смыслу;
  - **непереходное в переходной рамке** — «что кончает здесь» вместо «что здесь кончается».
- **Цитаты — по каноническому русскому изданию, а не по зеркалу английского** (Столпнер для
  Гегеля, Иванцов для Спинозы); расхождение с подлинником отмечается явно. Прежде чем спорить о
  формулировке — **проверь издание**: в §25 один рецензент дал верный заголовок и неверного
  Спинозу, другой наоборот, а сверка с изданием дала третье, снявшее самый спор.
- **Регистр относительных местоимений**: сосчитай «какой» против «который» в самом файле перед
  вставкой (§25 — 78 против 3).
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
