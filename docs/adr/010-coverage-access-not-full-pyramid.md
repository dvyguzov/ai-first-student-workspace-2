# ADR 010 (учебный): пирамида обрезана доступом, не языком продукта

**Статус:** принято  
**Дата:** 2026-08-31

## Контекст

Пак закрывает стек продукта (backend × frontend × tests). На работе часто иначе: UI на одном языке, API на другом; в backend не пускают; frontend-unit можно. Если агент всегда рисует полную пирамиду takeaway, он предлагает тесты, которые человек не смержит.

Развилка: считать «100%» каноном ячеек matrix **или** функцией **поверхности**, которая есть у этого человека.

## Решение

1. Intake — `docs/coverage-profile.md`: ярус → `access` (`write` / `read` / `none`) → стек/модуль.
2. `qa-coverage-audit` / `qa-pyramid-plan` / `qa-write-test` / `qa-make-full-pyramid` читают профиль **до** выбора `@Layer`.
3. `none` — серая колонка, не дыра этого чата. Компенсация — RAG `coverage-access`.
4. Смешанные стеки по ярусам — норма. Не новая cartesian-cell в `matrix.yaml`.

## Последствия

- Учебный takeaway: все ярусы `write` (java-spring). Workplace-вариации — тот же файл, другие значения.
- Лист [36](https://lab.qa.guru/36-login-lab.html) пока закреплён на e2e (тумблеры — слои агента). Ярусы доступа туда — отдельный проход.
- Номер **010** — пак. Takeaway 007–009 заняты продуктом (backend / frontend / login-401).

## RAG

`coverage-access` · `test-pyramid` · `adr-when`
