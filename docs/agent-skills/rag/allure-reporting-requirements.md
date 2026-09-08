---
id: allure-reporting-requirements
domain: testing
adr: 002
tags: [allure, layer, quality]
related: [allure-attach, po-step]
---
# Steps и attachments по слою

**id:** `allure-reporting-requirements`

| `@Layer` | Steps | Attachments |
|----------|-------|-------------|
| infra / unit | опционально | не требуются |
| api | обязательно (клиент / `Allure.step`) | Rest Assured listener в `ci` |
| ui | обязательно (PO `@Step`, в т.ч. `HeaderComponent`) | screenshot — `@Tag("screenshot")` на mock |
| e2e | обязательно (PO `@Step`) | screenshot — по флагу env |
| manual | обязательно (`Allure.step`) | не браузер |

## Don't

- Смешивать `Allure.step` и listener Selenide в одном тесте (двойные шаги).
- Требовать screenshot у api-слоя.
