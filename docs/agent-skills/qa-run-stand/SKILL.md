---
name: qa-run-stand
description: >-
  Запуск автотестов на mock / pipeline / stage / prod (Selenoid).
  Use when asked to run tests on mock, prod, stage, CI stand, or remote hub.
---

# Запуск на стенде (mock / pipeline / stage / prod)

RAG: `cfg-stands`, `cfg-env-profile`, `cfg-base-url`, `remote-selenoid`, `ci-gradle-args`.

Код теста один. Меняется только `-Denv=` (и `remoteUrl` на удалённом хабе).

## When

- «запусти на mock / проде / стейдже / в пайплайне», «Selenoid», «CI как locally»

## Do not

- `./gradlew test` без `-Denv`
- Хардкод URL в тесте
- Коммитить пароль Selenoid
- Prod без рабочего `remoteUrl`
- Деструктивные тесты на prod без OK
- Выдумывать host в Java, если DNS ещё не поднят

## A. Ui на stub (`mock`)

Chrome на стабе — ярус `ui`, не e2e. Compose: `docker compose --profile mock up -d stand-gateway`.

```bash
cd tests/java/tests-java-junit5-rest_assured-selenide
./gradlew test -Denv=mock -DincludeTags=ui -DexcludeTags=screenshot
```

## B. Pipeline ≈ локальный CI (`ci`)

```bash
docker compose up -d --build
curl -sf http://localhost:8800/api/health
# UI: http://localhost:9821/

cd tests/java/tests-java-junit5-rest_assured-selenide
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot
```

Jenkins `{login}-app-tests` / GHA — тот же `-Denv` и tags, что в job.

## C. Stage (`stage`)

```bash
./gradlew test -Denv=stage -DincludeTags=e2e -DexcludeTags=screenshot \
  -DremoteUrl="$SELENOID_WEBDRIVER_URL"
```

URL: [https://stage.ai-first.autotests.ai/](https://stage.ai-first.autotests.ai/). Нет DNS/стенда → не подменять URL в Java.

## D. Prod (`prod`)

```bash
./gradlew test -Denv=prod -DincludeTags=e2e -DexcludeTags=screenshot \
  -DremoteUrl="$SELENOID_WEBDRIVER_URL"
```

Нет URL хаба → стоп. Узкий срез, не full pyramid.

## DoD

- [ ] Названы слово (mock/pipeline/stage/prod) и `-Denv`
- [ ] Health (ci) или явный «нет remoteUrl» (prod) / «нет properties» (stage)
- [ ] Срез tags, не full suite
- [ ] Exit code
- [ ] Нет секретов в ответе и в git

## Example prompt

```text
Прочитай docs/agent-skills/qa-run-stand/SKILL.md и cfg-stands.
Запусти e2e на pipeline (compose). Не prod. Не коммить.
```
