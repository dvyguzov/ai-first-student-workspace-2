---
id: cfg-base-url
domain: config
adr: 002
tags: [baseUrl, apiBaseUrl]
---
# baseUrl и apiBaseUrl

**id:** `cfg-base-url`

`ci.properties`: UI (Selenide) `baseUrl=http://localhost:9821` — gateway, не голый frontend `:9811` (там нет `/api`). Без хвостового `/`: `Configuration.baseUrl = config.baseUrl()` + `open("/login")`. REST: `apiBaseUrl=http://localhost:8800/`.

PO открывает пути: `open("/login")`, `open("/")`.

## Do

- Fail fast, если `baseUrl` пустой.
- Fail fast, если `apiBaseUrl` пустой.
- `baseUrl` в профиле без хвостового `/`.
- Один прогон Gradle = один стенд.

## Don't

- Открывать UI на `:9811` и ждать `/api`.
- `open("http://…")` с полным URL в PO.
