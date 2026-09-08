---
name: qa-make-full-pyramid
description: >-
  Закрыть уже влитую фичу по ярусам unit → integration → component → api → ui → e2e → manual.
  Один вызов = один ярус; после яруса STOP. Не заменяет qa-write-test / qa-coverage-audit.
---

# Полная пирамида — один ярус за вызов

Фича **уже влита**. Этот skill не пишет продукт и не заменяет:
`qa-coverage-audit` (карта), `qa-pyramid-plan` (план + одна дыра продукта),
`qa-write-test` (как писать api/ui/e2e).

«100% пирамиды» = каждый сценарий фичи на **своём** `@Layer` **из write-ярусов профиля** (RAG `test-pyramid`, `coverage-access`).
Не 100% строк JaCoCo (`quality-gates`). Не e2e на все глаголы. Slice ≠ слой.

Контракт HTTP фичи — её RAG (CRUD: `crud-http`). Не копировать таблицу глаголов сюда.

## When

- «закрой пирамиду», «ярус unit/api/ui/e2e…», «следующий ярус», «make-full-pyramid»
- После влитой фичи, не вместо реализации

## Do not

- Реализовывать фичу (нет кода → STOP)
- Два яруса в одном вызове; «добить всё»
- Подменять `qa-write-test` / `qa-coverage-audit`
- E2e на все HTTP-глаголы; `@Layer("screenshot")`; smoke как ярус; chrome на стабе как e2e
- Выдумывать контракт (не читая RAG фичи)
- `localhost` / prod URL в Java
- Чинить чужие тесты «заодно»
- Кодить ярус с `access: none`
- Commit без OK

## RAG (на вызов — 2–4 id, не все сразу)

Каталог: `coverage-access` · `test-pyramid` · `test-layers` · `test-api-layer` · `cfg-stands` · `adr-when` · `quality-gates` + **RAG фичи**.
Профиль: `docs/coverage-profile.md`. Ярус `none` — пропустить, не кодить.

| Ярус | Читать |
|------|--------|
| unit | `test-pyramid`, RAG фичи, `quality-gates` |
| integration | `test-pyramid`, RAG фичи, `cfg-stands` |
| component | `test-pyramid`, `test-layers` |
| api | RAG фичи, `test-api-layer`, `cfg-stands` |
| ui | `test-pyramid`, `test-layers`, `cfg-stands` |
| e2e | `test-pyramid`, RAG фичи, `cfg-stands` (+ `qa-write-test` и его RAG) |
| manual | `test-pyramid`, `cfg-stands`, `adr-when` |

Пример takeaway (заметка): RAG = `crud-http`; ADR = `docs/adr/006-one-note-not-list.md`. Slice: `docs/adr/005-screenshot-not-layer.md`.

## Якоря (образец слоя, не дописывать чужой фиче)

| `@Layer` | Класс / файл | Прогон яруса |
|----------|--------------|--------------|
| unit | `backend/java/backend-java-spring/…/service/ItemServiceTest.java` | `cd backend/java/backend-java-spring && ./gradlew test jacocoTestReport jacocoTestCoverageVerification -DexcludeTags=integration` |
| integration | `backend/java/backend-java-spring/…/integration/AuthLifecycleIntegrationTest.java` | `cd backend/java/backend-java-spring && ./gradlew test -DincludeTags=integration` |
| component | `frontend/typescript/frontend-typescript-react/src/test/pages/HomePage.test.tsx` | `cd frontend/typescript/frontend-typescript-react && npm test -- --coverage` |
| api | `tests/java/tests-java-junit5-rest_assured-selenide/…/tests/api/AuthApiTests.java` | `cd tests/java/tests-java-junit5-rest_assured-selenide && ./gradlew test -Denv=ci -DincludeTags=api` |
| ui | `…/tests/ui/HeaderTests.java` / `HomeLayoutTests.java` | `cd tests/java/tests-java-junit5-rest_assured-selenide && ./gradlew test -Denv=mock -DincludeTags=ui -DexcludeTags=screenshot` |
| e2e | `…/tests/e2e/LoginTests.java` | `cd tests/java/tests-java-junit5-rest_assured-selenide && ./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot` |
| manual | `…/tests/manual/ExploratoryManualTests.java` | `cd tests/java/tests-java-junit5-rest_assured-selenide && ./gradlew test -Denv=ci -DincludeTags=manual` |

Изолированно: тот же `-Denv` / tags + `-Dtest=Class#method` (api/ui/e2e) или точечный класс backend/Vitest.

Порядок ярусов, если человек не назвал: **unit → integration → component → api → ui → e2e → manual**, пропуская `access: none`.

## Steps

1. Фича влита? Нет → STOP. Не кодить продукт.
2. Ярус = тот, что назвал человек, иначе первый пустой **write** в порядке выше. Rule: один task = один `@Layer` = один стек профиля.
3. Прочитай **этот** SKILL, `docs/coverage-profile.md` и **2–4** RAG из таблицы яруса (включая RAG фичи + `coverage-access` если ярус спорный).
4. Api/ui/e2e — пиши по `qa-write-test`. Unit/integration/component/manual — по якорю слоя.
5. Стенды: `cfg-stands`. Разрушение на prod — сиды нельзя; фабрика — только если ADR фичи (в RAG фичи).
6. Прогон **только этого** яруса (команда из таблицы, лучше точечный `-Dtest`).
7. Строка в живом отчёте, если есть (`docs/lessons/note-crud-pyramid.md`).
8. **STOP.** Ждать «следующий ярус».

## DoD

- [ ] Фича уже влита (этот skill её не писал)
- [ ] Ровно один `@Layer` с `write` в профиле; slice не назван ярусом
- [ ] 2–4 RAG, не вся папка; контракт из RAG фичи
- [ ] Стенды названы (`cfg-stands`)
- [ ] Прогон яруса; exit code в ответе
- [ ] Отчёт обновлён, если файл есть
- [ ] Нет commit без OK
- [ ] Следующий ярус не начат

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-make-full-pyramid/SKILL.md,
docs/coverage-profile.md и 2–4 RAG текущего яруса (для HTTP CRUD — crud-http;
спорный ярус — coverage-access). Фича уже влита.
Ярус: unit. По якорю ItemServiceTest. Не коммить. После яруса STOP.
```
