---
id: test-taxonomy
domain: testing
adr: 002
tags: [allure, epic, feature, tag, tms]
related: [tms-meta]
---
# Allure labels

**id:** `test-taxonomy`

Канон на классе `LoginTests`: `@Epic("Authentication")`, `@Feature("Login")`, `@Layer("e2e")`.  
`LoginFormTests` / `HeaderTests` (chrome на стабе): `@Layer("ui")`.  
На методе — `@Tag` яруса (`ui` / `e2e`) + `positive` / `negative`. Узкий прод-кейс дополнительно `@Tag("smoke")`.

TMS (`@AllureId`, `@Issue`) — чанк `tms-meta`. Образец в коде: `LoginFormTests` (`@AllureId("46592")`, `@Issue("MUL-2")`).

## Do

- Epic / Feature на **классе**.
- `@DisplayName` человекочитаемый — его видно в Allure и в `-Dtest=`.
- Один epic на класс (Home ≠ Authentication).

## Don't

- Мешать epic Home и Authentication в одном классе без причины.
- Выдумывать `@AllureId`, если кейса в TestOps ещё нет — сначала заглушка / ручной id от преподавателя.
