---
name: qa-stop-ci
description: >-
  Остановить идущий GitHub Actions run или Jenkins build.
  Use when asked to cancel a workflow, stop a build, or abort CI.
---

# Останови CI

RAG: `ci-github-actions` **или** `ci-jenkins`.

Только **свой** прогон. Чужие job / витрину преподавателя не гасить.

## When

- «отмени run», «stop build», «CI завис»

## Do not

- Cancel чужого fork / канон-job школы
- `ensure.py --stop` / kill портов app (это не CI)
- Удалять job целиком
- В том же task чинить причину (`qa-fix-ci`)

## GitHub Actions

```bash
gh run list --limit 5
gh run cancel <run-id>
```

Нет `gh` / нет прав → `blocked`, не крутить UI наугад.

## Jenkins

Stop на своём билде (красный крестик / Cancel). Не Disable job.

## DoD

- [ ] Что остановили (run-id / build number)
- [ ] Свой, не чужой
- [ ] Подтверждение cancel **или** blocked
- [ ] Нет commit

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-stop-ci/SKILL.md
и rag/ci-github-actions.md.
Отмени мой текущий workflow run. Чужие не трогай. Не коммить.
```
