---
paths:
  - "**/*Tests.java"
  - "**/*Test.java"
  - "**/*.test.ts"
  - "**/*.test.tsx"
  - "**/pages/**"
  - "docs/coverage-profile.md"
---

# Покрытие только по профилю доступа

- Перед новым тестом / планом пирамиды читай `docs/coverage-profile.md`.
- Ярус с `access: none` не предлагать и не кодить.
- Один task = один `@Layer` = один стек из профиля (не API в UI-модуле «заодно»).
- `none` ≠ дыра audit: серая колонка, компенсация — RAG `coverage-access`.
