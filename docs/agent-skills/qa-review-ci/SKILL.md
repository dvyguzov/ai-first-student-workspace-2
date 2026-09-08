---
name: qa-review-ci
description: >-
  Изучить GitHub Actions или Jenkins job: jobs, tags, что skip.
  Use when asked to read ci.yml, explain a pipeline, or map CI to the pyramid.
---

# Изучи CI

RAG: `ci-github-actions` **или** `ci-jenkins` (какой раннер назвал человек) + `ci-gradle-args`, `test-pyramid`.

Не путать с `qa-run-stand` (это Gradle на app). Здесь только **прочитать** пайплайн.

## When

- «разбери ci.yml», «что делает Jenkins job», «какие слои в CI»

## Do not

- Менять YAML / job config
- Запускать или отменять прогон (`qa-run-ci` / `qa-stop-ci`)
- Копировать matrix-оркестратор
- Секреты в ответ

## GitHub Actions

Файл `.github/workflows/ci.yml`. Таблица: job × слой/slice × команда (`ci-gradle-args`).  
Deploy skip без `DEPLOY_HOST` (`deploy-backend` / `deploy-frontend`) — не «CI сломан».

## Jenkins

Job `{login}-app-tests-…` на [jenkins.qa.guru](https://jenkins.qa.guru).  
Таблица: что в build (те же `-Denv` / tags, что в GHA). Нет доступа → `blocked`.

## DoD

- [ ] Назван раннер (GHA или Jenkins)
- [ ] Таблица job/build → слой
- [ ] YAML/job не менялись
- [ ] Нет commit

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-review-ci/SKILL.md
и rag/ci-github-actions.md, test-pyramid.
Таблица job ci.yml → слой → команда. Не меняй файлы. Не коммить.
```
