# Поверхность автоматизации (takeaway)

Ярус × доступ × стек. Как читать — RAG `docs/agent-skills/rag/coverage-access.md`.  
Шаблон под другой контур: `docs/agent-skills/_templates/coverage-profile.md` (после sync). Другой стек — id/путь своей ячейки, не список из шаблона.

Это **не** стек продукта целиком и не `layers:` модуля в `matrix.yaml`.

```yaml
product:
  backend:
    stack: java-spring
    access: write
  frontend:
    stack: typescript-react
    access: write

automation:
  unit:
    access: write
    stack: java-spring
    module: backend/java/backend-java-spring
  integration:
    access: write
    stack: java-spring
    module: backend/java/backend-java-spring
  component:
    access: write
    stack: typescript-react
    module: frontend/typescript/frontend-typescript-react
  api:
    access: write
    stack: java-junit5-rest_assured-selenide
    module: tests/java/tests-java-junit5-rest_assured-selenide
  ui:
    access: write
    stack: java-junit5-rest_assured-selenide
    module: tests/java/tests-java-junit5-rest_assured-selenide
  e2e:
    access: write
    stack: java-junit5-rest_assured-selenide
    module: tests/java/tests-java-junit5-rest_assured-selenide
  manual:
    access: write
    stack: java-junit5-rest_assured-selenide
    module: tests/java/tests-java-junit5-rest_assured-selenide

harness:
  agents:
    cline:  { access: write, module: .clinerules }
    cursor: { access: write, module: .cursor/rules }
```

`access` яруса: `write` | `read` | `none`. Агенты: `write` | `none` (ADR 011).  
Workplace (API C#, UI Python, backend закрыт) — не этот файл; пример в RAG `coverage-access`.
