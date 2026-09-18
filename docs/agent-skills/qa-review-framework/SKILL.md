---
name: qa-review-framework
description: >-
  Ревью тестового фреймворка takeaway: слои, TestBase, PO, tags, Allure.
  Use when asked to analyse or review the test framework. No rewrite unless OK.
---

# Ревью тестового фреймворка

RAG (≤4): `e2e-layers`, `po-locators`, `test-pyramid`, `cfg-stands`.

## When

- «посмотри фреймворк», «дай ревью автотестов», «канонично ли»

## Do not

- Переписывать стек в том же task
- Предлагать TestNG / Cucumber «потому что привык»
- Commit / массовый refactor без OK

## Что пройти (чеклист)

1. Пакеты: `config/`, `pages/` + `pages/components/`, `api/`, `tests/ui|e2e|api|manual|infra/` — чанк `e2e-layers`. Chrome на стабе — `tests/ui`, не e2e.
2. Lifecycle: `TestBase` vs `ApiTestBase` — нет setup в `@Test`.
3. Локаторы только в PO (`data-testid`). Header — `HeaderComponent`, не копия в каждом `*Page`.
4. `@Layer` + `@Tag` согласованы; screenshot / mock / smoke не выдаются за ярус.
5. Allure: steps на ui/e2e/api; results в `build/allure-results`.
6. Стенды: `mock` (ui) / `ci` (pipeline) / `prod`; stage-файла может не быть — это находка, не баг кода. URL не в тестах. Деструктивные тесты без ограничения стенда — must.

## Формат ответа

Таблица: **must / should / nice** × находка × файл:строка × зачем. Без воды. 5–12 пунктов.

Эталонные файлы: `tests/TestBase.java`, `pages/BasePage.java`, `pages/components/HeaderComponent.java`, `pages/LoginPage.java`, `api/ApiTestBase.java`, `tests/ui/HeaderTests.java`, `tests/e2e/LoginTests.java`.

## DoD

- [ ] Таблица находок, не эссе
- [ ] Ссылки на файлы takeaway
- [ ] Нет правок кода без OK
- [ ] Явно: что уже канон (не выдумывать «нет PO», если `LoginPage` есть)

## Example prompt

```text
Прочитай docs/agent-skills/qa-review-framework/SKILL.md
и чанки e2e-layers, base-lifecycle.
Ревью модуля tests/java/tests-java-junit5-rest_assured-selenide. Не меняй код.
```
