# ai-first-student-workspace-2

Учебный workspace курса **AI-first QA, поток 2**: takeaway Java/Spring + React + Selenide, плюс rules / skills / RAG.

Не форкайте [ai-first-student-workspace](https://github.com/qa-guru/ai-first-student-workspace) (поток 1). Этот репозиторий с ним **не синкается**.

Сначала **Fork** этого репозитория, потом clone своего форка.

```bash
# Fork на GitHub, затем:
git clone https://github.com/<your-login>/ai-first-student-workspace-2.git
cd ai-first-student-workspace-2
docker compose up -d --build
```

| Role | Folder |
|------|--------|
| Backend | `backend/java/backend-java-spring/` |
| Frontend | `frontend/typescript/frontend-typescript-react/` (`vendor/` — запечённый design-system runtime) |
| Tests | `tests/java/tests-java-junit5-rest_assured-selenide/` |

```bash
curl -sf http://localhost:8800/api/health
# UI same-origin (SPA + /api): http://localhost:9821/
# UI container only:          http://localhost:9811/
```

| Method | Path | Что |
|--------|------|-----|
| GET | `/api/health` | liveness |
| GET | `/api/openapi.yaml` | контракт (байты `_contract/openapi.yaml`) |
| GET | `/api/docs` | Swagger UI на ту yaml |

```bash
curl -sf http://localhost:8800/api/openapi.yaml >/dev/null
# Swagger UI: http://localhost:8800/api/docs
# same-origin: http://localhost:9821/api/docs
```

Tests (gateway already up):

```bash
cd tests/java/tests-java-junit5-rest_assured-selenide
./gradlew test -Denv=ci -DincludeTags=e2e -DexcludeTags=screenshot,mock
```

CI: `.github/workflows/ci.yml` (same orchestrator as the clone; stack knobs in `env:`).  
Prod stand: [https://ai-first.autotests.ai/](https://ai-first.autotests.ai/) (`-Denv=prod`).  
Stage: [https://stage.ai-first.autotests.ai/](https://stage.ai-first.autotests.ai/) (`-Denv=stage`).

Maintainers: refresh from autotests-ai-multistack-app in the zero-design-system monorepo:

```bash
./generators/render/render.sh --preset singlestack
```
