---
name: qa-coverage-audit
description: >-
  Оценить покрытие takeaway: @Layer inventory vs flows vs OpenAPI.
  Use when asked for coverage, gaps, or test map.
---

# Оцени покрытие

RAG: `coverage-access`, `test-pyramid`, `test-layers`, `test-taxonomy`, `test-api-layer`.  
Профиль: `docs/coverage-profile.md` (нет файла — спроси, не рисуй полную пирамиду workplace).

## When

- «какое покрытие», «чего не хватает», «карта тестов»

## Do not

- Путать line coverage JaCoCo с пирамидой
- Предлагать «добавить e2e на всё»
- Считать `access: none` дырой этого task
- Менять код в этом task (план — да, реализация — `qa-pyramid-plan` / `qa-write-test`)

## Steps

1. Прочитай `docs/coverage-profile.md`. Ярус `none` / `read` — серая колонка, не дыра этого task.
2. Inventory только по `write`: `tests/ui|e2e|api|manual|infra` + backend `src/test` + frontend `*.test.tsx` — если профиль даёт write.
3. Таблица: класс × `@Layer` × `@Tag` × сценарий (DisplayName).
4. Flows: login / register / logout / home health+items / auth API.
5. Сверить `AuthApiTests` vs `LoginTests` — где дубль, где дыра **на write-ярусе**.
6. Screenshot / mock / smoke — **slice**, не недостающий ярус. `mock` живёт внутри `ui`.
7. Дальше (занятие 4): отдельный task `qa-pyramid-plan`. Здесь только audit, без кода.

## Формат ответа

| Сценарий | unit | cmp | api | ui | e2e | man | Дыра? |
|----------|:----:|:---:|:---:|:--:|:---:|:---:|-------|
| login valid | | | | | | | |
| login 401 / wrong password | | | | | | | |
| register | | | | | | | |
| home items | | | | | | | |
| login form chrome (mock) | | | | | | | |
| header lang/theme (mock) | | | | | | | |

Легенда ячейки: есть тест / пусто (дыра, если `write`) / **✕** (`access: none` — не дыра).  
Плюс 3 приоритетных пробела **только по write** (ярус + стек из профиля + почему не e2e).

## DoD

- [ ] Inventory не «у нас всё покрыто» без таблицы
- [ ] Slice ≠ слой; `none` ≠ дыра
- [ ] Нет правок кода
- [ ] 3 приоритета с ярусом **и стеком из профиля**

## Example prompt

```text
Прочитай docs/agent-skills/qa-coverage-audit/SKILL.md,
rag/coverage-access.md и docs/coverage-profile.md.
Оцени покрытие. Таблица + 3 дыры только по write. Код не меняй.
```
