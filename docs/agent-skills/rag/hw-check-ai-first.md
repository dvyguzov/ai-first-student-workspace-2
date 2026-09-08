---
id: hw-check-ai-first
domain: testing
tags: [homework, ai-first, rubric]
related: [hw-check-verdict, adr-when]
---
# Рубрика AI-first занятия 2–4

**id:** `hw-check-ai-first`

Полные чеклисты у преподавателя: `docs/qa-guru/ai-first-qa/lesson-0N/checklist-submission-homework.md`. Здесь — сжатая рубрика для self-check.

## Занятие 2 (rules + skills)

| Критерий | Вес |
|----------|-----|
| Rule: контракт среза (команда + exclude screenshot/visual как в репо) | 25% |
| Rule: safety (commit + allure-results) | 15% |
| Skill: структура (3 сценария + DoD, свои имена) | 25% |
| Skill: воспроизводимость (новый task → те же flags) | 25% |
| Артефакты (2 скрина + текст) | 10% |

Авто-незачёт: простыня >250 строк; rule противоречит skill; агент закоммитил сам.

## Занятие 3 (RAG + CI)

| Критерий | Вес |
|----------|-----|
| Sync: adopt/skip, rules не затёрты | 25% |
| CI: job → слой, команды как в YAML, не `testE2e` | 30% |
| RAG: 2–4 чанка, не вся папка | 30% |
| Артефакты | 15% |

Авто-незачёт: `reset --hard`; токен в чате; «прочитай весь rag» как единственный промпт.

## Занятие 4 (ADR + пирамида)

| Критерий | Вес |
|----------|-----|
| ADR: контекст + решение + последствия | 30% |
| Audit: слои заполнены, 3 дыры с ярусом | 30% |
| Один шаг оркестратора, не mega-task | 25% |
| Термины: slice ≠ слой; JaCoCo ≠ пирамида | 15% |

Авто-незачёт: выдуманные `@AllureId`; токен Sonar в файле; `@Layer("screenshot")` / `@Layer("smoke")`; chrome на стабе как `@Layer("e2e")`.

## Don't

- Проверять диплом Java/Python этим чанком
- Путать с `qa-review-framework`
