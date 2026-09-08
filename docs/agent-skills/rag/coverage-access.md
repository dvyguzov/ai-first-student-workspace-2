---
id: coverage-access
domain: testing
adr: 010
tags: [pyramid, access, coverage]
related: [test-pyramid, test-layers]
---
# Поверхность автоматизации

**id:** `coverage-access`

Стек продукта и **ярусы, куда можно писать тесты**, — разные оси. Читай `docs/coverage-profile.md` до плана покрытия.

Канон ярусов — `test-pyramid`. Этот чанк — `access` и стек **яруса**.

## `access`

| | |
|--|--|
| `write` | можно добавить тест |
| `read` | смотреть, не менять |
| `none` | нет доступа; не дыра этого task |

Стек яруса может быть другим, чем продукт и соседний ярус.

## Компенсация

| Нет write | Куда |
|-----------|------|
| unit | api → component → ui |
| integration | api |
| component | ui (mock) |
| api | узкий e2e + residual |
| ui | e2e или manual |
| e2e | api + ui + residual |

Не прыгать в e2e, если ниже есть `write`. Backend `access: none` → не предлагать unit/integration.

Один task = один `@Layer` = один стек из профиля.

## Don't

- Полная пирамида без профиля (takeaway-файл есть — его и бери).
- `none` как «надо закрыть в этом чате».
- API-стек в UI-модуле «потому что ближе».
