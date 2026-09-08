---
name: qa-run-ci
description: >-
  Запустить или перезапустить GitHub Actions workflow / Jenkins build.
  Use when asked to rerun CI, dispatch workflow, or Build Now. Not Gradle on a stand.
---

# Запусти / перезапусти CI

RAG: `ci-github-actions` **или** `ci-jenkins`.

Это **не** `qa-run-stand` (Gradle против app). Здесь — кнопка пайплайна.

## When

- «перезапусти Actions», «workflow_dispatch», «Build Now», «rerun failed»

## Do not

- `git commit` / пустой push «чтобы дёрнуть CI», если человек не просил commit
- Prod-deploy (`deploy: true`) без OK
- Чужой job / чужой fork
- Секреты в argv (`gh` печатает их в лог)
- Чинить код в этом task (`qa-fix-ci`)

## GitHub Actions

```bash
gh workflow list
gh run list --limit 5
gh workflow run CI
# или: gh run rerun <run-id> --failed
```

`workflow_dispatch` inputs (`deploy`, `deploy_stage`) — только если человек явно сказал.

## Jenkins

Build Now на **своём** `{login}-app-tests-…`. Параметры как в прошлом зелёном билде. Нет кнопки → `blocked`.

## DoD

- [ ] Раннер + что именно запустили (весь workflow / failed jobs / один job)
- [ ] URL нового run/build **или** blocked
- [ ] Не prod-deploy без OK
- [ ] Нет commit без просьбы

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-run-ci/SKILL.md
и rag/ci-github-actions.md.
Перезапусти только упавшие jobs последнего run. Не deploy. Не коммить.
```
