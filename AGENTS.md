# QA Agent — takeaway Java/Selenide/Allure

- Ответы на **русском**; команды и пути — как в этом репозитории.
- Cline читает `.clinerules/`. Cursor Agent читает `.cursor/rules/*.mdc`. Это разные агенты.
- Модуль тестов: `tests/java/tests-java-junit5-rest_assured-selenide/`.
- Поверхность: `docs/coverage-profile.md` (какие ярусы `write`).
- Продукт: backend и frontend этого репо. Не писать Selenide в том же task.

## Ui (браузер на стабе)

```bash
cd tests/java/tests-java-junit5-rest_assured-selenide
./gradlew test -Denv=mock -DincludeTags=ui -DexcludeTags=screenshot
```

Compose: `docker compose --profile mock up -d stand-gateway`. Не называть mount на WireMock end-to-end.

## E2e (default «smoke»)

```bash
cd tests/java/tests-java-junit5-rest_assured-selenide
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot
```

Нет Gradle-task `testE2e` (rule 01). Срез занятия = `@Tag("e2e")` минус screenshot. `@Tag("smoke")` — prod slice, не эта команда (ADR 005). App: compose + gateway `:9821`, health `:8800`.

## Ограничения

- Не `git commit` / `git push` / `git reset --hard` без явной просьбы.
- Не удаляй `build/allure-results` без OK.
- Один task = один `@Layer` (rule 04).
- Fix тестов — только после triage и OK человека.
- Прод-стенд только `-Denv=prod` + рабочий remoteUrl.
- Новый автотест обязан быть годен для **pipeline / stage / prod** (URL из properties, не localhost в коде). RAG: `docs/agent-skills/rag/cfg-stands.md`.
- Ярусы только из `docs/coverage-profile.md` (`access: write`). RAG: `coverage-access`. Rule 08.
- Новый функционал без своего яруса — в ответе **Дыра** (не молчать). Не заводить JaCoCo-exclude под новую фичу.

## Workflow

См. `docs/agent-skills/` (`qa-smoke-debug`, `qa-write-test`, `qa-make-full-pyramid`, `qa-homework-check`, …) и RAG `docs/agent-skills/rag/` (HTTP CRUD: `crud-http`; поверхность: `coverage-access`). Модули продукта — `docs/coverage-profile.md`, не отдельный product-RAG.
