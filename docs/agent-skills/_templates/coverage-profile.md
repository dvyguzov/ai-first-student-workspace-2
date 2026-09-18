# Поверхность автоматизации

Заполни и положи в корень учебного репо: `docs/coverage-profile.md`.  
Как читать: RAG `coverage-access`. Канон ярусов: `test-pyramid`.

`stack` / `module` — **эта** ячейка, не каталог матрицы. Harness — корень репо, не `<module>/.harnes`. Агенты — блок `harness.agents` (ADR 011).

```yaml
product:
  backend:
    stack: {BACKEND}          # takeaway: java-spring
    access: write             # write | read | none
  frontend:
    stack: {FRONTEND}         # takeaway: typescript-react
    access: write

automation:
  unit:        { access: none, stack: "", module: "" }
  integration: { access: none, stack: "", module: "" }
  component:   { access: none, stack: "", module: "" }
  api:         { access: write, stack: "{API_STACK}", module: "{API_MODULE}" }
  ui:          { access: write, stack: "{UI_STACK}", module: "{UI_MODULE}" }
  e2e:         { access: write, stack: "{E2E_STACK}", module: "{E2E_MODULE}" }
  manual:      { access: write, stack: "", module: "" }

harness:
  agents:
    cline:  { access: write, module: .clinerules }      # write | none
    cursor: { access: write, module: .cursor/rules }
```

Один task = один `@Layer` = один `stack` из этого файла.  
`none` на ярусе — не предлагать тест. Агент `none` — адаптер в emit не копировать. Пак держит оба.
