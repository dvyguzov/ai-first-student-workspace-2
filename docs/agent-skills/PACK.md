# Пак QA skills / rules / RAG (AI-first)

Учебный комплект под takeaway потока 2  
[ai-first-student-workspace-2](https://github.com/qa-guru/ai-first-student-workspace-2). Поток 1 ([ai-first-student-workspace](https://github.com/qa-guru/ai-first-student-workspace)) не синкать.

Копирование в demo-workspace: [sync-to-workspace.sh](sync-to-workspace.sh).  
Окно преподавателя: [lesson-02/teacher-second-workspace.md](../qa-guru/ai-first-qa/lesson-02/teacher-second-workspace.md) (занятия 3–4 — тот же cwd).

## Слои

| Слой | Где | Роль |
|------|-----|------|
| Rules | `.clinerules/*.md` (Cline), `.cursor/rules/*.mdc` (Cursor Agent), `AGENTS.md` | лимиты |
| Skills | `docs/agent-skills/<name>/SKILL.md` (SSOT); Cursor опц. `.cursor/skills/` | workflow + DoD |
| RAG | `docs/agent-skills/rag/<id>.md` | факты (2–4 файла на задачу) |
| ADR | `docs/adr/` + цитата в skill | почему (занятие 4) |

Листы A4: [lab.qa.guru](https://lab.qa.guru/) — общая карта, по слою, стеки наращивания, login A/B, абляция, лаборатория ([36](https://lab.qa.guru/36-login-lab.html) — тумблеры Skill/Rule/RAG; сценарий пока e2e; ярусы доступа — `docs/coverage-profile.md`), ДЗ ([40](https://lab.qa.guru/#40-homework)), словарь ([50](https://lab.qa.guru/50-glossary.html)).

## Skills

| Skill | Промпт | Занятие | Файлы |
|-------|--------|---------|-------|
| `qa-smoke-debug` | e2e slice + Allure + flaky | **2 · эфир и зачёт** (единственный skill на паре) | [example](examples/multistack/qa-smoke-debug/SKILL.md) · [template](templates/qa-smoke-debug/SKILL.md) |
| `qa-write-test` | разработай автотест | 3–4 | [example](examples/multistack/qa-write-test/SKILL.md) · [template](templates/qa-write-test/SKILL.md) |
| `qa-review-framework` | ревью фреймворка | позже / опц. | [example](examples/multistack/qa-review-framework/SKILL.md) |
| `qa-homework-check` | self-check сдачи занятия | 2–4 | [example](examples/multistack/qa-homework-check/SKILL.md) |

**Homonym:** pack `qa-homework-check` (студент self-check) ≠ monorepo `.cursor/skills/` cold `qa-homework-check` (ментор GC/диплом). Перед задачей: `mv docs/cursor-skills-cold/qa-homework-check .cursor/skills/` → новый Agent chat.
| `qa-review-ci` | изучи GHA / Jenkins | 3 | [example](examples/multistack/qa-review-ci/SKILL.md) |
| `qa-create-ci` | включи Actions / заведи job | 3 · опц. | [example](examples/multistack/qa-create-ci/SKILL.md) |
| `qa-fix-ci` | почини красный прогон | 3 | [example](examples/multistack/qa-fix-ci/SKILL.md) |
| `qa-run-ci` | перезапусти workflow/build | 3 | [example](examples/multistack/qa-run-ci/SKILL.md) |
| `qa-stop-ci` | отмени run/build | 3 | [example](examples/multistack/qa-stop-ci/SKILL.md) |
| `qa-run-stand` | Gradle на pipeline / stage / prod | 3–4 | [example](examples/multistack/qa-run-stand/SKILL.md) |
| `qa-pull-takeaway` | точечный adopt из upstream | 3 | [example](examples/multistack/qa-pull-takeaway/SKILL.md) |
| `qa-setup-host` | DNS / nginx / TLS | 3 · опц. | [example](examples/multistack/qa-setup-host/SKILL.md) |
| `qa-coverage-audit` | оцени покрытие | 4 | [example](examples/multistack/qa-coverage-audit/SKILL.md) |
| `qa-pyramid-plan` | план + один ярус | 4 | [example](examples/multistack/qa-pyramid-plan/SKILL.md) |
| `qa-make-full-pyramid` | ярус за ярусом, уже влитая фича | 4 | [example](examples/multistack/qa-make-full-pyramid/SKILL.md) |
| `qa-bootstrap-framework` | фреймворк с чеклиста | позже | [example](examples/multistack/qa-bootstrap-framework/SKILL.md) |

CI: глагол в skill (`review`/`create`/`fix`/`run`/`stop`), раннер в RAG (`ci-github-actions` / `ci-jenkins`). `qa-run-ci` ≠ `qa-run-stand`.  
`qa-make-full-pyramid` ≠ `qa-pyramid-plan` (план + одна дыра) и ≠ `qa-write-test` (один автотест): один вызов = один ярус уже влитой фичи, потом STOP. Контракт фичи — RAG (HTTP CRUD: `crud-http`), не таблица в generic skill.  
Поверхность (какие ярусы `write`, какой стек на ярусе) — `docs/coverage-profile.md` + RAG `coverage-access`, не cartesian в matrix.  
Не skill: TMS (`test-taxonomy` / `tms-meta`), JaCoCo/Sonar (`quality-gates`). Хост ≠ stand.

## Rules (example)

| Файл | Лимит |
|------|--------|
| [01-qa-java-gradle.md](examples/multistack/clinerules/01-qa-java-gradle.md) · [`.mdc`](examples/multistack/cursor-rules/01-qa-java-gradle.mdc) | ui / e2e команды, не full suite |
| [02-git-safety.md](examples/multistack/clinerules/02-git-safety.md) | нет commit без OK |
| [03-env-and-stand.md](examples/multistack/clinerules/03-env-and-stand.md) | pipeline / mock(ui) / stage / prod, всегда `-Denv` |
| [04-one-task-one-layer.md](examples/multistack/clinerules/04-one-task-one-layer.md) | один task = один ярус |
| [05-homework-check.md](examples/multistack/clinerules/05-homework-check.md) | self-check ДЗ: таблица + статус, без commit |
| [08-coverage-access.md](examples/multistack/clinerules/08-coverage-access.md) | не кодить ярус `access: none`; стек из профиля |

Takeaway 06–07 — product (backend / frontend), не этот пакет numbered-gap. Профиль: [coverage-profile.md](examples/multistack/coverage-profile.md) → в репо `docs/coverage-profile.md`. ADR [010](adr/010-coverage-access-not-full-pyramid.md).

## Команды ярусов (канон takeaway)

```bash
cd tests/java/tests-java-junit5-rest_assured-selenide
# ui — браузер SPA на stub API (job ui-tests)
./gradlew test -Denv=mock -DincludeTags=ui -DexcludeTags=screenshot
# e2e — сквозной путь через живой /api
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot
```

Gradle-task `testE2e` **нет**. `@Tag("smoke")` есть на узких методах — **prod slice**, не ярус. На занятии срез e2e = тег `e2e` минус screenshot. Chrome на стабе — ярус `ui`, не e2e.

CI: `.github/workflows/ci.yml`. Прод: [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) (`-Denv=prod`), не матрица `/stack/…`.  
ADR курса (takeaway `docs/adr/`): [adr/005-screenshot-not-layer.md](adr/005-screenshot-not-layer.md), [adr/006-one-note-not-list.md](adr/006-one-note-not-list.md), [adr/010-coverage-access-not-full-pyramid.md](adr/010-coverage-access-not-full-pyramid.md) (HTTP — RAG [`crud-http`](rag/crud-http.md), SSOT monorepo `docs/rag/testing/crud-http.md`). Не путать с monorepo `docs/adr/005-testing-pyramid-review.md` / `006-allurerc-mjs-ethalon.md`. Проверяльщик школы (преподаватель): monorepo ADR 014 + skill `qa-homework-check`.
