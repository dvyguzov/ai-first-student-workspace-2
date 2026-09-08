---
name: qa-homework-check
description: >-
  Self-check сдачи занятия AI-first (рубрика чеклиста, черновик комментария ментора).
  Use when student asks to check homework, зачёт, сдачу занятия 2–4.
---

# Self-check ДЗ (как ментор)

RAG: `hw-check-verdict`, `hw-check-ai-first` (и `hw-check-voice`, если файл есть в паке).

Не путать с `qa-review-framework` (ревью фреймворка, не зачёт занятия).

## When

- «проверь домашку», «зачёт занятия N», «можно сдавать?»

## Do not

- `git commit` / `git push`
- Выдумывать критерии вне чеклиста занятия
- Чинить код в том же task (сначала таблица pass/fail)
- Писать «прочитай весь `docs/agent-skills/rag/`»

## Шаги

1. Номер занятия (2 / 3 / 4). Чеклист: `docs/qa-guru/…` у преподавателя **или** локальный чеклист, если положили в репо. Иначе — чанк `hw-check-ai-first`.
2. Прочитать skill + 2–3 RAG, не всю папку.
3. Сверить артефакты: `.clinerules/`, `docs/agent-skills/`, ADR, `ci.yml` — что требует **это** занятие.
4. Таблица критерий | вес | pass/fail | что исправить.
5. Статус: принято / не принято / ожидает проверки (нет артефакта).
6. Черновик комментария: привет → список → статус. Accept можно коротко.

## Авто-незачёт

Простыня skill/rule >250 строк · rule противоречит skill · агент закоммитил сам · `reset --hard` · токен в файле · выдуманный `testE2e` · `@Layer("screenshot")` как ярус (зан. 4).

## Example prompt

```text
Прочитай docs/agent-skills/qa-homework-check/SKILL.md
и rag/hw-check-verdict.md, rag/hw-check-ai-first.md.
Проверь сдачу занятия N. Не коммить. Таблица + статус.
```

## DoD

- [ ] Занятие названо
- [ ] Таблица по рубрике, не эссе
- [ ] Один статус
- [ ] Нет commit
