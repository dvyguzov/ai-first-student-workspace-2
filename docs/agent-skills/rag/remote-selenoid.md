---
id: remote-selenoid
domain: testing
adr: 002
tags: [selenoid, remote]
---
# Браузер на хабе

**id:** `remote-selenoid`

Профиль `prod`: `remoteUrl=https://selenoid.qa.guru/wd/hub`. **Креды в git не кладут** — передают `-DremoteUrl=https://user:pass@selenoid.qa.guru/wd/hub` (CI secret / локальный env).

Локальный `ci`: `remoteUrl` пустой → Chrome на машине.

## Do

- Прод-прогон только с `-Denv=prod` (и рабочим remoteUrl).
- Capabilities — `selenoid:options` в `TestBase`, не chrome-flags как на local.

## Don't

- `./gradlew test` «на прод» без профиля.
- Коммитить пароль хаба.
