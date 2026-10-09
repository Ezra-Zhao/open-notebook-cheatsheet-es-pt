# 📓 Open Notebook — Quick Guide (English)

> Commands verified against [lfnovo/open-notebook](https://github.com/lfnovo/open-notebook) README (2026-10-09).
> What it is: the open-source NotebookLM alternative — private, multi-model, 100% local. Your data never leaves your machine.

---

## 0. Deploy in 4 steps (Docker)

```bash
mkdir open-notebook && cd open-notebook
curl -o docker-compose.yml https://raw.githubusercontent.com/lfnovo/open-notebook/main/docker-compose.yml
```

Edit `docker-compose.yml`: replace `OPEN_NOTEBOOK_ENCRYPTION_KEY=change-me-to-a-secret-string` with your own secret (generate one with `openssl rand -hex 32`).

```bash
docker compose up -d
# wait ~30 s, then open http://localhost:8502
```

- UI: `http://localhost:8502` · API: `http://localhost:5055`
- Shared network or server? Bind ports to `"127.0.0.1:8502:8502"` and `"127.0.0.1:5055:5055"`, or add `- OPEN_NOTEBOOK_PASSWORD=<redacted> to `environment:`.

---

## 1. Connect an AI provider

Sidebar: **Models** (under Manage) → find your provider → **Add Configuration** → name + API key (local Ollama: **Base URL** instead) → **Test** → **Models** → pick a **Model Type**, tick models → **Add**.

Minimum: **1 language model + 1 embedding model**. Then **Auto-assign Defaults** under Default Model Assignments.

| Provider | LLM | Embedding | STT | TTS | Notes |
|---|---|---|---|---|---|
| OpenAI | ✅ | ✅ | ✅ | ✅ | Most complete |
| Google (GenAI) | ✅ | ✅ | ✅ | ✅ | Full alternative |
| Anthropic | ✅ | ❌ | ❌ | ❌ | No embeddings — pair with another provider |
| Ollama (local) | ✅ | ✅ | ❌ | ❌ | **Free, 100% local**, zero API cost |
| Groq / Mistral / DeepSeek / xAI | ✅ | partial | partial | partial | See official matrix |
| OpenRouter / LM Studio / OpenAI-compatible | ✅ | ✅ | ✅ | ✅ | Any compatible endpoint |

No API key? Ollama in Docker: official **Local Quick Start** (zero cost).

---

## 2. Multi-speaker podcast

- **1–4 speakers** with custom profiles (NotebookLM only does 2).
- Full script control + **Episode Profiles**.
- Flow: create a notebook → add sources (PDF, video, audio, web) → generate the podcast.

---

## 3. MCP & API

- **MCP**: official "MCP Integration" guide in `docs/` — connects Claude Desktop, VS Code and other MCP clients.
- **REST API**: full API at `http://localhost:5055` — complete automation.

---

## 4. Update & backup

```bash
docker compose pull && docker compose up -d   # update
```

- Back up the `surrealdb` data volume before updating in production.
- Stuck? Official 5-minute troubleshooting guide, Discord, or GitHub Issues.

---

*Questions? https://www.open-notebook.ai · Join the official Discord.*
