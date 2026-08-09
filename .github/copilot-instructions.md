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
квант действия; «второй подкруг Учения о Бытии» for the sphere of Quantity;
субстрат (*Substrat*); **абсолютное безразличие** (*absolute Indifferenz*); рефлексия (*Reflexion*);
**снятое бытие** (*aufgehobenes Sein*); положенный / положенность (*gesetzt*); основание (*Grund*).
Определения рефлексии (*Reflexionsbestimmungen*): тождество (*Identität*); различие / различие в себе (*Unterschied*);
**разность** (*Verschiedenheit*, not «разнообразие» = *Mannigfaltigkeit*); равенство / неравенство (*Gleichheit / Ungleichheit*);
противоположность (*Gegensatz*); положительное / отрицательное; противоречие (*Widerspruch*);
«уходить в основание» (*zu Grunde gehen*, the гибель/основание pun); законы мышления (тождества, непротиворечия, исключённого третьего);
существенные отношения (*wesentliche Verhältnisse*, not «соотношения»);
**опосредование** (*Vermittlung* / mediation — default for the category/process, not «опосредствование»).
Сфера Основания и Существования: **обоснованное** (*Begründetes*); **формальное / реальное / полное основание**;
**форма** (*Form*) / **материя** (*Materie*) / **содержание** (*Inhalt*); гилеморфизм; **усыпляющая сила** (*virtus dormitiva*);
**псевдо-объяснение**; принцип **достаточного основания** (*nihil est sine ratione*); **условие** (*Bedingung*);
**сама суть дела** (*die Sache selbst*, женского рода — «она вступает в существование»; **не** «вещь», какая закреплена за *Ding*);
**абсолютно безусловное**; **существование** (*Existenz*, vs **наличное бытие** = *Dasein*); **опосредованная непосредственность**;
**вещь** (*Ding*); **явление** (*Erscheinung*); **действительность** (*Wirklichkeit*); причинность; взаимодействие.
**Беспокойство** (*Unruhe*); **безосновность** (*grundlos*); **акосмизм** (*Akosmismus*).

Translation decisions to keep:

- *Vermittlung* / mediation → **«опосредование»** by default (idiomatic Hegelian Russian; pairs
  with «непосредственность / опосредованное / опосредованность / самоопосредование»). Reserve
  **«опосредствование»** only where the prose deliberately stresses mediation *by a means*
  («средство»); for syllogistic/structural middle-term mediation prefer **«средний термин /
  опосредующий момент»**, and **«опосредованность»** for the *state* of being mediated (not the
  process). Established corpus norm: «опосредование» is uniform across all installments.
- *Reich der Schatten* / "realm of shadows" (Hegel's own name for pure Logic prior to its
  release into Nature) → **«царство теней»** (standard scholarly Russian rendering). Do not
  drift to «мир теней» or «царство призраков».
- *die Sache selbst* / "the fact itself" (the self-grounding totality of ground + all conditions,
  §22) → **«сама суть дела»** (feminine; «она вступает в существование»). Keep it distinct from
  *Ding* → **«вещь»** (§23), mirroring the English fact/thing split. Do **not** render *Sache* as
  «вещь» here, which would collide with the coming *Ding*.
- *Existenz* → **«существование»**, kept distinct from *Dasein* → **«наличное бытие»**; the
  emergence from ground is a **«опосредованная непосредственность»**, not the bare immediacy of §10.
- Methodological *recollection* — an earlier determination reached again immanently in a richer
  element, not remembered by a subject or externally reapplied by analogy — → **«имманентное
  возвращение»**; use objective contextual variants such as **«узнанное вновь»** and
  **«возвращающееся из самого движения»**. Reserve **«вобранное в себя»** for §19's distinct
  inward-withdrawal sense.

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
- "underlies" (a ground underlying its determinations) → **«лежит под / лежит в основе»**, never
  **«подлежит»** (= *is subject to*, which reverses the relation).
- "the claim is categorial" (the guardrail) → **«утверждение … категориальное»**, not
  **«притязание»** (= *pretension / claim-to-validity*).
- "essence shows itself" (in the *Schein* sense) → **«показывает себя»**, not «кажет / кажущая
  себя» (collides with «кажущийся» = *seeming*, inverting the point that essence genuinely shows).
- *Unruhe* / "unrest" → **«беспокойство»** (канон: §10, §11, §24 — шесть употреблений подряд).
  **Не** «непокой», не «непокойность».
- "groundless" / *grundlos* → **«безосновный / безосновность»** (канон: §23, §25).
- **Цитаты и заголовки — по каноническому русскому изданию, а не по зеркалу английского.**
  Заголовки Гегеля — по Столпнеру: «Случайность, или формальная действительность, формальная
  возможность и формальная необходимость» (троекратное «формальная», хотя подлинник несёт одно
  *Formal*). Спиноза — по Иванцову: «по недостатку нашего знания». Для цитируемого верность
  изданию **выше** зеркальности; расхождение с английским отмечается явно, а не молча. Пояснительное
  «или» (= «то есть») внутри заголовка берёт запятую.
- **Регистр относительных местоимений дрейфует по корпусу**: ранние выпуски держатся «который»,
  поздние — «какой». Перед вставкой в готовый файл **сосчитай оба** (в §25 — 78 «какой» против
  3 «которое»), иначе новая вставка садится мимо регистра выпуска, в какой её кладут.
- Archaic-register markers to preserve: **указует, счисляется, зараз** (atemporal "at once"),
  надолго отложенное.

## Двусмысленности, какие ловятся разбором, а не слухом

Русский допускает прочтения, каких английский подлинник не допускает. Эти три класса проверяй
в каждой новой вставке — все три уже давали ошибку:

- **Обратная агентность в придаточном.** «то тождество, какое производит сам непокой случайности»:
  «какое» (ср. р.) и «непокой» (неодуш. м. р.) совпадают в им. и вин. падежах, и русский по
  умолчанию берёт прочтение с подлежащим-«тождеством» — то есть **обратное** нужному. Для
  отношения «X порождает Y» ставь страдательный залог с творительным: «какое **производится**
  самим беспокойством случайности». Залог здесь несёт смысл, а не стиль.
- **Голые отглагольные существительные.** «обращение» (переворот / обращение к кому-либо),
  «признание» (признание / исповедь). Без предлога они двусмысленны; бери однозначное слово
  («переворот»), особенно когда соседний выпуск уже приучил читателя к другому смыслу
  (§23 четырежды даёт «обращение вещи к другим»). Глагольная рамка с предлогом снимает вопрос:
  «обращает **против**» однозначно.
- **Непереходные глаголы в переходной рамке.** «что кончает здесь» — вне нормы (нужно
  «кончается») и вдобавок тянет просторечный смысл, каким в этом регистре шутить нельзя.
- **Дефисные слепки с «что».** Английское *that-it-is* (Dass-sein, бытие-факта: **что** нечто
  есть, в отличие от того, **что** оно есть) нельзя передавать слепком «что-оно-есть»:
  в именной позиции «что» читается сперва как вопросительно-относительное «что», и слепок
  оборачивается в *Was-sein* — чтойность, ровно противоположное. Бери форму цитаты:
  *«она есть»* / *«оно есть»*, где род следует роду предмета (вещь — «она», абсолютное —
  «оно»). Форма цитаты однозначна: «оно есть» не прочесть как чтойность. Слепки через дефис
  хороши для корпуса вообще («в-себе», «бытие-для-другого», «сущность-в-её-показывании»),
  но не тогда, когда первое слово слепка есть омоним служебного.

## House style / commits

Same as the English repo: single-italic-span abstract, italic-plain math (not LaTeX),
`§NN` cross-references, and a `README.md` index **kept parallel with the English README**.

**Проверяй зеркальность механически, а не на глаз.** Чекер не видит расхождений с английским.
Перед каждым коммитом прогоняй построчный разбор: число `**`-пролётов и множество ссылок `§NN`
в каждой строке должны совпадать с английским файлом (нумерация строк 1:1). Он ловит то, чего
не ловит чтение, — так был пойман лишний жирный «**Кант**» в §25, какого нет в подлиннике.
Скрипт и порядок прогона — в `REVIEW.md`. Там же проверка целости файла: **только CRLF, без
одиночных LF и без BOM** (в `README.md` есть застарелый одиночный CR — правь его только
побайтово).

- **GPG-sign every commit** (`-S`). Signing program: `C:/Program Files/GnuPG/bin/gpg.exe`.
- Author: `Roman Konstantinovskiy <stop-cran@list.ru>`.
- Trailer: `Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>`.
- Stage only `.md` / `README.md`; do not stage build artifacts.
- Use the literal `§` character in commit messages.
- Verify after committing: `git log --pretty="%h %G? %s" -1` should show `G`.
