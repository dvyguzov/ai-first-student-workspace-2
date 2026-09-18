# ADR 011 (учебный): harness в корне — OS + оверлей + агенты-модули

**Статус:** принято  
**Дата:** 2026-09-13

## Контекст

Пак один, потребителей два (курс / configurator). Развилка: класть harness в модуль стека (`<module>/.harnes`, каталог `stacks/`) **или** сплющивать OS + оверлей в **корень** окна. Второй harness в ячейке ломает пути занятий 3–4 (`docs/agent-skills/rag/<id>.md`, `.clinerules/01-qa-java-gradle.md`) и плодит меню матрицы в живом профиле.

Номер **011** — только пак. Не путать с monorepo `docs/adr/011-cursor-host-pre-router-feasibility.md`.

## Решение

1. Harness окна — **корень**: `.clinerules/`, `.cursor/rules/`, `docs/agent-skills/` (skills + RAG). Не `<module>/.harnes`.
2. Стек яруса — строка `docs/coverage-profile.md` + rule команд с `paths` (takeaway: `01-qa-java-gradle`). Не каталог всех ячеек матрицы в профиле.
3. Агенты — модули в том же профиле: `harness.agents` (`cline` / `cursor`, `access: write` | `none`, `module:` `.clinerules` / `.cursor/rules`). Пак держит все адаптеры; emit копирует выбранные (`write`).
4. Overlay в корень: **assemble** = OS + `cell` + выбранные agents (без слоя `course`: hw-check, ДЗ, занятия 2–4). **clone-as-student** / текущий `sync-to-workspace.sh` = OS + `cell` + `course` + оба агента. Сплющивание, не дерево `stacks/`.

## Последствия

- Пути takeaway не менять: `docs/agent-skills/rag/po-fluent.md`, `.clinerules/01-qa-java-gradle.md`.
- Не переносить `rag/*.md` в `stacks/` и не заводить пустой django-оверлей в этом паке.
- Студенческий GitHub не синкать, пока пак и программа не готовы.

## RAG

`coverage-access` · `adr-when`
