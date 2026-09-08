---
name: qa-setup-host
description: >-
  Зарегистрировать DNS и поднять HTTPS-хост продукта (nginx + compose).
  Use when asked for subdomain, hosting, TLS, or prod URL. Not a test stand (ci/stage/prod).
---

# Поддомен и хостинг

RAG: `cfg-host`, `cfg-stands`, `ci-github-actions`.

`stand` в курсе = pipeline / stage / prod (`qa-run-stand`). Здесь — **хост** (DNS + nginx).

Для курса достаточно витрины преподавателя ([ai-first.autotests.ai](https://ai-first.autotests.ai/) · [stage.ai-first.autotests.ai](https://stage.ai-first.autotests.ai/)). Свой хост — **опционально**. Зону `autotests.ai` студенты не трогают.

## When

- «зарегистрируй поддомен», «поставь nginx», «свой prod URL»

## Do not

- Выдумывать host в `*.java`, если DNS ещё нет
- Открывать Postgres в интернет
- Коммитить SSH-ключ / сертификат
- Называть localhost prod
- Трогать чужие зоны DNS школы без OK преподавателя

## Steps

1. Имя: `{login}.ваш-домен` (свой registrar). Не зона `autotests.ai` без OK преподавателя.
2. У регистратора (Beget / GoDaddy / Namecheap / панель VPS): запись **A** `{host}` → IPv4 VPS. Подождать TTL.
3. На VPS: Docker Engine, clone **своего форка**, `docker compose up -d --build`. Если `:8800`/`:9821` уже заняты — `.env` с `BACKEND_JAVA_PORT` / `CI_GATEWAY_PORT` и `docker compose --project-name … --env-file .env`. Health на выбранном backend-порту `/api/health`.
4. nginx: `server_name` = хост; `proxy_pass` на **gateway** (канон `:9821`, не frontend `:9811`). TLS: `certbot --nginx`.
5. Проверка: `curl -sf https://{host}/api/health`. UI и `/api` с того же origin.
6. GitHub vars `DEPLOY_HOST` / `DEPLOY_USER` / `DEPLOY_APP_DIR` (+ remap `DEPLOY_COMPOSE_*`) и `secrets.DEPLOY_SSH_KEY` — skill `qa-create-ci`. Тесты: `-Denv=prod` только с рабочим `remoteUrl`.

Нет VPS/DNS → таблица «blocked: чего не хватает», код не менять.

## DoD

- [ ] Host назван явно
- [ ] Health HTTPS 2xx **или** явный blocked
- [ ] Gateway `:9821`, не frontend `:9811`
- [ ] Нет секретов в git и в ответе
- [ ] Нет commit без OK

## Example prompt

```text
Rules ON. Прочитай docs/agent-skills/qa-setup-host/SKILL.md
и rag/cfg-host.md.
План своего HTTPS-хоста: DNS A, nginx на gateway :9821, health.
Нет VPS — таблица blocked. URL в Java не выдумывай. Не коммить.
```
