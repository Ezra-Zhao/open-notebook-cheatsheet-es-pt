# 📓 Open Notebook — guía rápida (Español)

> Comandos verificados con el README de [lfnovo/open-notebook](https://github.com/lfnovo/open-notebook) (2026-10-09).
> Qué es: alternativa open-source a NotebookLM — privada, multi-modelo, 100% local. Tus datos no salen de tu máquina.

---

## 0. Despliegue en 4 pasos (Docker)

```bash
mkdir open-notebook && cd open-notebook
curl -o docker-compose.yml https://raw.githubusercontent.com/lfnovo/open-notebook/main/docker-compose.yml
```

Edita `docker-compose.yml`: cambia `OPEN_NOTEBOOK_ENCRYPTION_KEY=change-me-to-a-secret-string` por una clave tuya (genérala con `openssl rand -hex 32`).

```bash
docker compose up -d
# espera ~30 s y abre http://localhost:8502
```

- UI: `http://localhost:8502` · API: `http://localhost:5055`
- ¿Red compartida o servidor? Cambia los puertos a `"127.0.0.1:8502:8502"` y `"127.0.0.1:5055:5055"`, o añade `- OPEN_NOTEBOOK_PASSWORD=<redacted> en `environment:`.

---

## 1. Conectar un proveedor de IA

En la barra lateral: **Models** (en Manage) → busca tu proveedor → **Add Configuration** → nombre + API key (Ollama local: **Base URL** en vez de key) → **Test** → **Models** → elige un **Model Type**, marca los modelos → **Add**.

Mínimo necesario: **1 modelo de lenguaje + 1 modelo de embedding**. Luego **Auto-assign Defaults** en Default Model Assignments.

| Proveedor | LLM | Embedding | STT | TTS | Notas |
|---|---|---|---|---|---|
| OpenAI | ✅ | ✅ | ✅ | ✅ | El más completo |
| Google (GenAI) | ✅ | ✅ | ✅ | ✅ | Alternativa completa |
| Anthropic | ✅ | ❌ | ❌ | ❌ | Sin embeddings: combínalo con otro proveedor |
| Ollama (local) | ✅ | ✅ | ❌ | ❌ | **Gratis, 100% local**, sin coste de API |
| Groq / Mistral / DeepSeek / xAI | ✅ | parcial | parcial | parcial | Ver matriz oficial |
| OpenRouter / LM Studio / OpenAI-compatible | ✅ | ✅ | ✅ | ✅ | Cualquier endpoint compatible |

¿Sin API key? Ollama en Docker: guía oficial **Local Quick Start** (cero costo).

---

## 2. Pódcast multi-locutor

- **1–4 locutores** con perfiles personalizados (NotebookLM solo da 2).
- Control total del guion + **Episode Profiles** (formato del episodio).
- Flujo: crea un notebook → añade fuentes (PDF, video, audio, web) → genera el pódcast.

---

## 3. MCP y API

- **MCP**: guía oficial "MCP Integration" en `docs/` — conecta Claude Desktop, VS Code y otros clientes MCP.
- **API REST**: completa, en `http://localhost:5055` — automatización total.

---

## 4. Actualizar y respaldar

```bash
docker compose pull && docker compose up -d   # actualizar
```

- Respalda el volumen de datos de `surrealdb` antes de actualizar en producción.
- ¿Algo falla? Guía oficial de troubleshooting (5 minutos), Discord o GitHub Issues.

---

*¿Dudas? https://www.open-notebook.ai · Únete al Discord oficial.*
