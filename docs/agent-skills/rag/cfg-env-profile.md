---
id: cfg-env-profile
domain: config
adr: 002
tags: [env, properties]
---
# Выбор стенда

**id:** `cfg-env-profile`

`-Denv=ci` → `src/test/resources/config/ci.properties`.

Файлы в takeaway: `default.properties` (флаги) + `ci` / `mock` / `stage` / `prod` (куда стучимся).

Ось **pipeline / stage / prod** — чанк `cfg-stands`. Тест не содержит URL стенда.

## Do

- Всегда передавать `-Denv=`.
- URL только в properties / `-DbaseUrl`, не в тесте.

## Don't

- Файл `local.properties` / `multistack_ci.properties` (стенд — короткое имя: `ci` / `stage` / `prod` / `mock`).
- Хардкод `http://localhost:9821` в `LoginTests`.
