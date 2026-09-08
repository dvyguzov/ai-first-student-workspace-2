---
name: qa-pyramid-plan
description: >-
  План 100% пирамиды и реализация одного недостающего яруса.
  Use when asked for pyramid plan or to fill a missing layer.
---

# 100% пирамида — план и один шаг

RAG: `coverage-access`, `test-pyramid`, `test-layers`, `test-api-layer`, `cfg-stands`, `adr-when`.  
ADR: `docs/adr/005-screenshot-not-layer.md`, `docs/adr/010-coverage-access-not-full-pyramid.md`. Сначала `qa-coverage-audit`, потом этот план, потом `qa-write-test`.  
Профиль: `docs/coverage-profile.md` — дыра только на `write`.

«100%» = продукт закрыт по пирамиде **целиком**, не каждый ярус по 100% и не 100% строк кода. Этот skill закрывает **одну дыру** в общей карте, не «добить слой до 100%».

## When

- «план пирамиды», «довёл до 100%», «куда класть этот кейс»

## Do not

- Добавлять e2e вместо api
- Называть chrome на стабе e2e
- Вводить `@Layer("screenshot")`
- Реализовывать все дыры в одном task (один ярус / один стек / один тест)
- Предлагать ярус с `access: none`

## Steps

1. Возьми таблицу из `qa-coverage-audit` (или собери коротко) и `docs/coverage-profile.md`.
2. План: для каждой **write**-дыры — ярус + стек/модуль профиля + класс-якорь + **стенды** (pipeline / stage / prod). `none` — компенсация из `coverage-access`, не пункт плана.
3. Согласуй с человеком **одну** реализацию.
4. Пиши по `qa-write-test` (PO/api-клиент, tags).
5. Прогон только этого слоя.

Примеры правильного слота:

| Дыра | Куда |
|------|------|
| JSON login 401 | `AuthApiTests`, не новый UI-клик |
| Chrome формы / header на стабе | `tests/ui/…`, не `@Layer("e2e")` |
| Текст ошибки на форме после живого login | `LoginTests` + PO, уже есть wrong password |
| Чеклист exploratory | `tests/manual`, `@Manual` |

## DoD

- [ ] План таблицей (дыра → ярус → стек профиля)
- [ ] Нет пунктов на `access: none`
- [ ] Не больше одного нового теста без OK
- [ ] Прогон с правильным `-DincludeTags`
- [ ] Screenshot не назван ярусом

## Example prompt

```text
Прочитай docs/agent-skills/qa-pyramid-plan/SKILL.md,
coverage-access и docs/coverage-profile.md.
План пирамиды по write-ярусам. Реализуй только если я скажу какой ярус.
Не коммить.
```
