# RAG для курса AI-first QA (диета)

Retrieval-единицы **для учебного репо студента**. Не копия всего `docs/rag/` monorepo (~96 чанков) — Ollama 7b это не удержит.

**SSOT паттернов в monorepo:** `docs/rag/` (преподаватель).  
**Студенту:** эти файлы кладём в `docs/agent-skills/rag/` учебного проекта. Skill пишет: «прочитай `docs/agent-skills/rag/po-fluent.md`».

Якоря кода — **takeaway** `ai-first-student-workspace` (клон [qa-guru/ai-first-student-workspace](https://github.com/qa-guru/ai-first-student-workspace)). Ethalon в monorepo — тот же код в другой раскладке папок.

## Слой чанка

| Слой | Смысл |
|------|--------|
| OS | любой стек: пирамида, доступ, HTTP, стенды, ADR |
| cell | дефолтная ячейка takeaway (Java / Gradle / Selenide / Rest Assured) |
| course | проверка ДЗ, не продукт |

Другой стек позже — оверлей `cell`-чанков, не копия OS и не каталог в модуле. Адаптеры агентов — не строка этой таблицы, а `harness.agents` (ADR 011). Агент читает **2–4 файла**, не всю папку. Машина слоёв: [overlay-manifest.yaml](../overlay-manifest.yaml).

## Как читать

Один чанк = один `id`.

| id | Слой | Когда |
|----|------|--------|
| [`test-pyramid`](test-pyramid.md) | OS | какой ярус, не путать slice |
| [`coverage-access`](coverage-access.md) | OS | какие ярусы `write`; стек на ярусе |
| [`crud-http`](crud-http.md) | OS | HTTP CRUD: PUT 201/200, PATCH merge-patch; POST только на коллекции (SSOT: monorepo `docs/rag/testing/crud-http.md`) |
| [`cfg-stands`](cfg-stands.md) | OS | pipeline / stage / prod при написании теста |
| [`cfg-host`](cfg-host.md) | OS | DNS / nginx / TLS (не stand) |
| [`adr-when`](adr-when.md) | OS | rule/skill/RAG vs ADR |
| [`test-taxonomy`](test-taxonomy.md) | OS | Epic / Feature / Tag |
| [`tms-meta`](tms-meta.md) | OS | `@AllureId` / `@Issue` |
| [`quality-gates`](quality-gates.md) | OS | JaCoCo / Sonar ≠ пирамида |
| [`testdata-user`](testdata-user.md) | OS | сид `user1` литералами vs `UserBuilder` на register |
| [`allure-attach`](allure-attach.md) | OS | screenshot / results |
| [`allure-reporting-requirements`](allure-reporting-requirements.md) | OS | steps по `@Layer` |
| [`test-layers`](test-layers.md) | cell | `@Layer` → Gradle `-DincludeTags` |
| [`e2e-layers`](e2e-layers.md) | cell | config / TestBase / pages / tests |
| [`po-fluent`](po-fluent.md) | cell | цепочка PO, `return this` |
| [`po-locators`](po-locators.md) | cell | селекторы только в PO |
| [`po-step`](po-step.md) | cell | `@Step` на методах страницы |
| [`test-negative`](test-negative.md) | cell | negative login |
| [`test-api-layer`](test-api-layer.md) | cell | Rest Assured, не Selenide |
| [`base-lifecycle`](base-lifecycle.md) | cell | `TestBase` setup/teardown |
| [`cfg-env-profile`](cfg-env-profile.md) | cell | `-Denv=` |
| [`cfg-base-url`](cfg-base-url.md) | cell | `baseUrl` / `apiBaseUrl` |
| [`ci-gradle-args`](ci-gradle-args.md) | cell | эталонные Gradle-команды |
| [`ci-github-actions`](ci-github-actions.md) | cell | jobs takeaway `ci.yml` (глаголы — skills `qa-*-ci`) |
| [`remote-selenoid`](remote-selenoid.md) | cell | браузер на хабе |
| [`ci-jenkins`](ci-jenkins.md) | course | jenkins.qa.guru: job, агент, signup |
| [`hw-check-verdict`](hw-check-verdict.md) | course | статус сдачи: принято / нет / ожидает |
| [`hw-check-ai-first`](hw-check-ai-first.md) | course | рубрика занятий 2–4 |
| [`hw-check-voice`](hw-check-voice.md) | course | тон комментария к сдаче |

Занятие 2: явный путь к файлу. Занятие 3: зачем 2–4 чанка, не вся папка. Занятие 4: писать ADR (не пирамида). Пирамида — следующее занятие.
