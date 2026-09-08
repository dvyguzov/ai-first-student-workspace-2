---
id: ci-jenkins
domain: config
tags: [ci, jenkins]
related: [ci-github-actions, ci-gradle-args, cfg-stands]
---
# Jenkins (qa.guru)

**id:** `ci-jenkins`

Хост: [https://jenkins.qa.guru](https://jenkins.qa.guru). Signup: [https://jenkins.qa.guru/signup](https://jenkins.qa.guru/signup) (когда открыт).

Тот же код тестов, что GitHub Actions. Другой runner. Срез: `-Denv=` и tags из `ci-gradle-args` (в живом takeaway часто `multistack_ci`).

Глаголы — skills `qa-review-ci` · `qa-create-ci` · `qa-fix-ci` · `qa-run-ci` · `qa-stop-ci`. Этот чанк — факты.

## Факты

| | |
|--|--|
| Имя job | `{login}-app-tests-freestyle-java-allure3-full-attachments` |
| SCM | ваш fork takeaway (не канон-job школы) |
| Агент | `java-jdk21` |
| Креды | Jenkins credentials, не git |
| Markup | Plain Text в `currentBuild.description` — без HTML |

Позже (отдельные доступы): Selenoid, Jira, Confluence, TestOps.

## Don't

- Hudson.Administer
- Пароль в description / чат
- Считать Jenkins заменой GHA: GHA = takeaway pipeline; Jenkins = школьный контур TMS
