---
id: test-pyramid
domain: testing
adr: 005
tags: [pyramid, layer, slice]
related: [test-layers, coverage-access]
---
# Пирамида (takeaway)

**id:** `test-pyramid`

`@Layer` — ярус пирамиды. **CI slice** (`screenshot` / `mock` / `smoke`) — не ярус: тот же `@Layer` + другой `@Tag`.

«100% пирамида» = **одна** оценка на весь продукт: каждый сценарий на своём ярусе, пропорция здравая. Не сумма «по 100% на каждый слой». Не 100% строк JaCoCo. Не «e2e на всё».

## Ярусы в этом проекте

| `@Layer` | Где код | Зачем |
|----------|---------|--------|
| unit | `backend/java/backend-java-spring/src/test` (без `@Tag("integration")`) | логика без HTTP/браузера; JaCoCo |
| integration | тот же `backend-…/src/test`, `@Tag("integration")` | Spring + Testcontainers |
| component | `frontend/typescript/frontend-typescript-react/` Vitest + RTL | UI-компонент в jsdom, не Selenide |
| api | `tests/…/tests/api/` | HTTP, Rest Assured, `ApiTestBase` |
| ui | `tests/…/tests/ui/` (`HeaderTests`, `LoginFormTests`) | браузер на stub API (`-Denv=mock`) |
| e2e | `tests/…/tests/e2e/` | браузер через живой бэкенд |
| manual | `tests/…/tests/manual/` | `@Manual` + `Allure.step`, не WebDriver |
| infra | `tests/…/tests/infra/` | config / HAR / CSS — инфра тестов |

Gradle-task `testE2e` в takeaway **нет**. Срез яруса = `-DincludeTags=<имя>`.

## Slice ≠ слой

| Slice | Как отбираем | Где в CI | Не делать |
|-------|----------------|----------|-----------|
| classroom ui | `@Tag("ui")`, exclude `screenshot` | job `ui-tests` | звать mock «e2e» |
| classroom e2e | `@Tag("e2e")`, exclude `screenshot` | job `e2e-tests` | выдумывать task `testE2e` |
| smoke | `@Tag("smoke")` на узких методах (`HomeTests`, login valid) | prod: `e2e & smoke` / `api & smoke` | называть smoke ярусом |
| screenshot | `@Tag("screenshot")` + env mock/prod | `ui-tests`, `e2e-tests` screenshot step | `@Layer("screenshot")` |
| mock | `@Tag("mock")` внутри `ui` | тот же `ui-tests` | путать с api-слоем или с ярусом |

Локально на занятии: `-DincludeTags=e2e` (шире, чем prod-smoke).  
Prod: узкий `@Tag("smoke")` + Selenoid. Оба — **не** новые `@Layer`.

## Don't

- Закрывать api-контракт только e2e.
- Писать e2e там, где хватает `AuthApiTests`.
- Путать JaCoCo (строки backend unit) с покрытием сценариев пирамиды.
- Предлагать ярус с `access: none` (чанк `coverage-access`, файл `docs/coverage-profile.md`).
