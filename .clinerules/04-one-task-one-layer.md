---
paths:
  - "**/*Tests.java"
  - "**/pages/**"
---

# Один task — один ярус

- Новый чат Cline / Cursor после смены rule или skill.
- Одна задача = один `@Layer` или один тест. Не «почини всё».
- Chrome на стабе = `@Layer("ui")`, не e2e.
- Селекторы не трогать без triage (skill flaky / review).
- API-контракт не закрывать новым e2e, если уже есть `tests/api`.
