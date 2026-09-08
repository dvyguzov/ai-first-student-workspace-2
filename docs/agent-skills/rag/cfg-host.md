---
id: cfg-host
domain: config
tags: [dns, nginx, tls, host]
related: [cfg-stands, ci-github-actions]
---
# Поддомен учебного хоста

**id:** `cfg-host`

Не путать со `stand` (pipeline / stage / prod). Здесь — DNS + nginx + TLS.

Канон курса (витрина преподавателя):

| Слово | Host | `-Denv=` |
|-------|------|----------|
| pipeline | compose (GHA runner / ноутбук) | `ci` |
| stage | [https://stage.ai-first.autotests.ai/](https://stage.ai-first.autotests.ai/) | `stage` |
| prod | [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) | `prod` |

Свой продукт: `{login}.example.com` (ваш registrar) → A-запись на VPS → nginx → `127.0.0.1:9821` (gateway). SPA ходит в `/api` на том же origin.

## Шаги (свой хостинг)

1. Купить/взять домен у регистратора (Beget / GoDaddy / Namecheap — как есть). Не зона `autotests.ai`.
2. DNS: `A {host} → IPv4 VPS`. Подождать TTL.
3. На VPS: Docker, clone **своего форка**, `docker compose up -d --build`. Порты `:8800`/`:9821` заняты → remap в `.env` + `--project-name`.
4. nginx `server_name` + `proxy_pass` на gateway (`:9821` или remap) + TLS (Let's Encrypt).
5. В GitHub форка: `vars.DEPLOY_HOST` / `DEPLOY_USER` / `DEPLOY_APP_DIR` + `secrets.DEPLOY_SSH_KEY`. На общем хосте с матрицей — ещё `DEPLOY_COMPOSE_PROJECT` и `DEPLOY_COMPOSE_ENV_FILE`.
6. Health: `https://{host}/api/health` 2xx. Потом `-Denv=prod` (когда будет `remoteUrl`).

Пока DNS нет — **не** подставлять другой URL в Java. Тесты читают properties.

## Don't

- Публиковать Postgres наружу.
- Класть SSH-ключ в репозиторий.
- Называть localhost «prod».
- Копировать матричный путь `/stack/backend-…/frontend-…`.
