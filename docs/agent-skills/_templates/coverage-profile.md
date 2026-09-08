# Поверхность автоматизации

Заполни и положи в корень учебного репо: `docs/coverage-profile.md`.  
Как читать: RAG `coverage-access`. Канон ярусов: `test-pyramid`.

```yaml
product:
  backend:
    stack: {BACKEND}          # go / java-spring / …
    access: write             # write | read | none
  frontend:
    stack: {FRONTEND}         # js-angular / typescript-react / …
    access: write

automation:
  unit:        { access: none, stack: "", module: "" }
  integration: { access: none, stack: "", module: "" }
  component:   { access: none, stack: "", module: "" }
  api:         { access: write, stack: "{API_STACK}", module: "{API_MODULE}" }
  ui:          { access: write, stack: "{UI_STACK}", module: "{UI_MODULE}" }
  e2e:         { access: write, stack: "{E2E_STACK}", module: "{E2E_MODULE}" }
  manual:      { access: write, stack: "", module: "" }
```

Один task = один `@Layer` = один `stack` из этого файла.  
`none` — не предлагать тест на этом ярусе.
