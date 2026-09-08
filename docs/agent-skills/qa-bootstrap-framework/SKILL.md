---
name: qa-bootstrap-framework
description: >-
  Поднять тестовый фреймворк: clone takeaway + чеклист слоёв, не vibe-scaffold.
  Use when asked to create a test framework from scratch.
---

# Фреймворк «с нуля»

Это **не** «сгенерируй JUnit из головы». Канон курса: клон takeaway или чеклист слоёв + RAG.

RAG: `e2e-layers`, `test-pyramid`, `cfg-env-profile`, `cfg-base-url`, `cfg-stands`.

## When

- «создай тестовый фреймворк», «с нуля Selenide/JUnit», «скелет автотестов»

## Do not

- Пустой `build.gradle` с выдуманными плагинами
- Копировать monorepo `zero-design-system` целиком
- Cursor cold skill `generate-full-stack` (это инфра преподавателя)

## Steps

1. База: clone  
   `https://github.com/qa-guru/ai-first-student-workspace`  
   или учебный zip с занятия.
2. Чеклист слоёв (должно появиться / остаться):

| Слой | Есть? |
|------|-------|
| `config/*.properties` + `-Denv` | |
| профили pipeline / stage / prod (хотя бы ci + prod; stage — заготовка) | |
| `TestBase` / `ApiTestBase` | |
| `pages/` с `@Step` + `pages/components/` (общий chrome) | |
| `tests/ui` + `tests/e2e` + `tests/api` | |
| `@Layer` + `@Tag` | |
| Allure results dir | |

3. Подставить стенды: `baseUrl` / `apiBaseUrl` в **properties** на pipeline, stage (если есть), prod — не в тестах.
4. Первый прогон: e2e slice из `qa-smoke-debug` (app UP).
5. Если у студента **другой** стек — перенести **структуру** (слои/tags/PO), не Java-файлы as-is. Якоря в SKILL заменить.

## DoD

- [ ] Репо не с нуля из чата, а из takeaway/чеклиста
- [ ] Первый e2e или api прогон с `-Denv`
- [ ] Таблица слоёв заполнена
- [ ] Нет commit без OK

## Example prompt

```text
Прочитай docs/agent-skills/qa-bootstrap-framework/SKILL.md.
Нужен фреймворк под этот репозиторий. Не генерируй Gradle с нуля —
опирайся на takeaway/чеклист. Не коммить.
```
