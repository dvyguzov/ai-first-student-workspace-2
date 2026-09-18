# Пак QA (takeaway поток 2)

Репозиторий: [ai-first-student-workspace-2](https://github.com/qa-guru/ai-first-student-workspace-2).  
Агент читает **2–4 RAG-чанка** на задачу, не всю папку `rag/`.

## Слои

| Слой | Где | Вопрос |
|------|-----|--------|
| Rule | `.clinerules/` | Что нельзя всегда? |
| Skill | `docs/agent-skills/<name>/SKILL.md` | Как сделать задачу? |
| RAG | `docs/agent-skills/rag/<id>.md` | Откуда факт? |
| ADR | `docs/adr/` | Почему A, не B? |

Каталог чанков: [rag/README.md](rag/README.md).

## Эфир

| Занятие | Одна мысль | Что сдаём |
|---------|------------|-----------|
| 2 | два файла переживают чат | `qa-smoke-debug` + rule |
| 3 | 2–4 чанка, не папка | `qa-write-test` **без кода** |
| 4 | почему A, не B | свой `docs/adr/007-*.md` |
| след. | пирамида | `qa-coverage-audit` → `qa-pyramid-plan` |

Остальные skills в репо — не зачёт сегодняшней пары.

## RAG на e2e (занятие 3)

Skill `qa-write-test` называет четыре id: `po-fluent`, `po-step`, `test-negative`, `cfg-stands`.  
Другой ярус — замени пару (всё равно ≤4).

## ADR (занятие 4)

| Файл | Зачем |
|------|--------|
| `docs/adr/005-screenshot-not-layer.md` | образец: screenshot — slice, не `@Layer` |
| `docs/adr/009-login-401-is-api.md` | тот же сюжет, что ДЗ RAG: JSON 401 ≠ новый e2e |
| `docs/agent-skills/_templates/adr-stub.md` | шаблон |
| `docs/adr/007-….md` | **свой** файл (006 уже занят) |

`010` — следующее занятие. `006-one-note` на эфире не открываем.

## Команды ярусов

```bash
cd tests/java/tests-java-junit5-rest_assured-selenide
# ui — браузер SPA на stub API
./gradlew test -Denv=mock -DincludeTags=ui -DexcludeTags=screenshot
# e2e — сквозной путь через живой /api
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot
```

Gradle-task `testE2e` **нет**. `@Tag("smoke")` — prod slice, не ярус. Chrome на стабе — ярус `ui`.

Прод: [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) (`-Denv=prod`).
