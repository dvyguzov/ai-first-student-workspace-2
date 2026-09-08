---
id: base-lifecycle
domain: testing
adr: 002
tags: [testbase, junit]
---
# TestBase lifecycle

**id:** `base-lifecycle`

Канон: `tests/TestBase.java`. `@BeforeAll` — `Configuration.baseUrl` из config. `@AfterEach` — attachments. Драйвер не создаётся в каждом `@Test`.

API-тесты наследуют `ApiTestBase`, не `TestBase`.

## Do

- Один setup на класс.
- Close browser — по флагу config, не «всегда закрыть в первой строке теста».

## Don't

- `Selenide.open` + `new ChromeDriver()` в тесте.
