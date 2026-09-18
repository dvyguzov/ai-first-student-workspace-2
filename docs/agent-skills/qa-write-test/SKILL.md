---
name: qa-write-test
description: >-
  Написать автотест по канону takeaway: слой, PO, tags, Allure.
  Use when asked to add ui/e2e/api test, cover a scenario, or copy LoginTests.
---

# Разработай автотест

RAG (ровно 4, не всю папку): `po-fluent`, `po-step`, `test-negative`, `cfg-stands`.
Другой ярус — замени пару, всё равно ≤4: ui → `po-locators` + `test-layers`; api → `test-api-layer` + `test-layers`. Нет `write` в профиле → вместо одной пары `coverage-access`.
Профиль: `docs/coverage-profile.md`. Ярус без `write` → STOP.

## When

- «напиши e2e на …», «покрой header на mock», «добавь negative login», «покрой API login»

## Do not

- CSS/xpath в классе `*Tests`
- Новый `ChromeDriver` / setup в тесте
- E2e на JSON-контракт, если место в `tests/api` (и api `write`)
- Ярус / модуль, которого нет в профиле как `write`
- `localhost` / prod URL / пароль хаба в коде теста
- Деструктивный сценарий на prod без OK / без ADR фичи с фабрикой (`cfg-stands`)
- Читать всю папку `docs/agent-skills/rag/`
- Commit без OK

## Якоря

| Слой | Образец |
|------|---------|
| e2e | `tests/e2e/LoginTests`, `pages/LoginPage` (`data-testid`) |
| ui | `tests/ui/HeaderTests` / `LoginFormTests` — chrome на `-Denv=mock`; header через `BasePage.header` |
| api | `tests/api/AuthApiTests`, `api/AuthApiClient` |
| fluent e2e | `loginPage.openPage().fillAndSubmitForm("user1", "password1")` — сид литералами, чанк `testdata-user` |
| fluent ui | `loginPage.openPage().header.shouldHaveLangLabel("EN")` |

## Steps

1. `docs/coverage-profile.md`: выбранный `@Layer` = `write`? Нет → STOP, назови компенсацию из `coverage-access`. Модуль и стек — из профиля, не хардкод takeaway, если профиль другой.
2. Выбери **один** `@Layer` (чанк `test-layers`). Chrome на стабе — `ui`. Сквозной путь через живой `/api` — `e2e`. JSON-контракт — `api`.
3. **Стенды (чанк `cfg-stands`):** этот тест поедет на pipeline (`ci`), stage (`stage`) и/или prod (`prod`)? Данные (сиды) есть на всех? Сиды на prod не сносить. Фабрика+teardown на prod — только если ADR фичи. URL только из config. Контракт новой фичи — её RAG, не этот skill.
4. Есть PO/клиент? Расширь его. Нет — создай локаторы в `pages/` (общий chrome — `pages/components/`), не в тесте.
5. Класс: `@Layer`, `@Epic`, `@Feature`, `@DisplayName`. Метод: `@Tag` яруса + `positive`/`negative`.
6. Прогон только этого теста на профиле слоя (`mock` для ui, `ci` для e2e/api). Команда — из **модуля профиля** (rule 01). Якорь takeaway (java/Gradle), не универсал:

```bash
cd tests/java/tests-java-junit5-rest_assured-selenide
# e2e
./gradlew test -Denv=ci -DincludeTags=e2e -Dtest=LoginTests#<method>
# ui
./gradlew test -Denv=mock -DincludeTags=ui -Dtest=HeaderTests#<method>
# api
./gradlew test -Denv=ci -DincludeTags=api -Dtest=AuthApiTests#<method>
```

Другой стек — команда своей ячейки, не этот блок.

7. В ответе: слой, стек/модуль профиля, **на каких стендах поедет**, команда, exit code. Не коммитить.

## DoD

- [ ] Слой выбран явно; в профиле `write`; стек/модуль названы
- [ ] Названы стенды: mock / pipeline / stage / prod (что да / нет)
- [ ] Нет URL и секретов в тесте
- [ ] Локаторы не в тесте
- [ ] `@Step` на PO или api-шаги в отчёте
- [ ] Изолированный прогон модуля из профиля (takeaway: Gradle `-Denv=ci`; иначе команда ячейки)
- [ ] Нет commit

## Example prompt

```text
Rules включены. Прочитай docs/agent-skills/qa-write-test/SKILL.md
и только po-fluent, po-step, test-negative, cfg-stands.
Нужен e2e на неверный пароль.
Если такой тест уже есть — напиши класс#метод, слой и на каких стендах поедет.
Код не пиши. Не коммить.
```
