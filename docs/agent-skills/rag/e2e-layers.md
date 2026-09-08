---
id: e2e-layers
domain: testing
adr: 002
tags: [structure, testbase, pages]
---
# Слои тестового модуля

**id:** `e2e-layers`

Корень: `tests/java/tests-java-junit5-rest_assured-selenide/src/test/java/`.

| Пакет | Назначение |
|-------|------------|
| `config/` | env profiles, typed keys |
| `api/` | `ApiTestBase`, HTTP-клиенты |
| `pages/` | Page Objects, локаторы, `@Step` |
| `pages/components/` | вложенные PO (`HeaderComponent`); шарятся через `BasePage.header` |
| `helpers/` | `User` / `UserBuilder` / `DataFaker` — throwaway, не сид (чанк `testdata-user`) |
| `tests/ui/` | браузер на stub API (`@Layer("ui")`, `-Denv=mock`) |
| `tests/e2e/` | браузер через живой `/api` (`@Layer("e2e")`) |
| `tests/api/` | HTTP-сценарии, `ApiTestBase` |
| `tests/manual/` | exploratory stubs |
| `tests/infra/` | helpers (config / HAR / CSS; не слой пирамиды) |
| `allure/` | attachments |
| `annotations/` | `@Layer`, `@Manual` |

## Do

Новый сценарий: сначала PO (или API-клиент) → потом класс теста. URL только из config.

## Don't

- `Configuration.browser` в каждом `@Test`.
- CSS/xpath в классе `*Tests`.
