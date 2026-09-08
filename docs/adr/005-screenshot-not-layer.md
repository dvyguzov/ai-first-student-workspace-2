# ADR 005 (учебный): screenshot — slice, не слой

**Статус:** принято  
**Дата:** 2026-08-19

## Контекст

Хочется «ярус визуальных тестов» рядом с api/e2e. В CI уже есть compare PNG (mock / stage). Если завести `@Layer("screenshot")`, сломается маппинг TestOps и пирамида: пиксельный diff — это тот же браузерный сценарий, другой **отбор**.

## Решение

1. Классы `*ScreenshotTests` остаются на ярусе сценария: chrome PNG → `@Layer("ui")`, welcome-panel после логина → `@Layer("e2e")`.
2. Отбор: `@Tag("screenshot")` + `-Denv=mock` или `prod` + job `ui-tests` / `e2e-tests` screenshot step.
3. `@Tag("smoke")` — тоже slice (узкий прод), не ярус. Gradle-task `testE2e` в takeaway нет.
4. Mock UI (`-Denv=mock`) — **ярус `ui`**, не api-слой и не e2e. Header / burger / layout chrome — `tests/ui` + `HeaderComponent`. `@Tag("mock")` — slice внутри ui.

## Последствия

- Новый визуальный кейс ≠ новый `@Layer`.
- «100% пирамида» не требует screenshot на каждый flow.
- Полный ADR школы (monorepo) студентам не копировать — этот файл достаточен.

## RAG

`test-pyramid` · `test-layers` · `ci-github-actions`
