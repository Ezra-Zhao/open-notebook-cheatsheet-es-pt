# 📓 Open Notebook — guia rápido (Português)

> Comandos verificados com o README de [lfnovo/open-notebook](https://github.com/lfnovo/open-notebook) (2026-10-09).
> O que é: alternativa open-source ao NotebookLM — privada, multi-modelo, 100% local. Seus dados não saem da sua máquina.

---

## 0. Deploy em 4 passos (Docker)

```bash
mkdir open-notebook && cd open-notebook
curl -o docker-compose.yml https://raw.githubusercontent.com/lfnovo/open-notebook/main/docker-compose.yml
```

Edite o `docker-compose.yml`: troque `OPEN_NOTEBOOK_ENCRYPTION_KEY=change-me-to-a-secret-string` por uma chave sua (gere com `openssl rand -hex 32`).

```bash
docker compose up -d
# espere ~30 s e abra http://localhost:8502
```

- UI: `http://localhost:8502` · API: `http://localhost:5055`
- Rede compartilhada ou servidor? Troque as portas para `"127.0.0.1:8502:8502"` e `"127.0.0.1:5055:5055"`, ou adicione `- OPEN_NOTEBOOK_PASSWORD=<redacted> em `environment:`.

---

## 1. Conectar um provedor de IA

Na barra lateral: **Models** (em Manage) → ache seu provedor → **Add Configuration** → nome + API key (Ollama local: **Base URL** em vez de key) → **Test** → **Models** → escolha um **Model Type**, marque os modelos → **Add**.

Mínimo necessário: **1 modelo de linguagem + 1 modelo de embedding**. Depois **Auto-assign Defaults** em Default Model Assignments.

| Provedor | LLM | Embedding | STT | TTS | Notas |
|---|---|---|---|---|---|
| OpenAI | ✅ | ✅ | ✅ | ✅ | O mais completo |
| Google (GenAI) | ✅ | ✅ | ✅ | ✅ | Alternativa completa |
| Anthropic | ✅ | ❌ | ❌ | ❌ | Sem embeddings: combine com outro provedor |
| Ollama (local) | ✅ | ✅ | ❌ | ❌ | **Grátis, 100% local**, sem custo de API |
| Groq / Mistral / DeepSeek / xAI | ✅ | parcial | parcial | parcial | Ver matriz oficial |
| OpenRouter / LM Studio / OpenAI-compatible | ✅ | ✅ | ✅ | ✅ | Qualquer endpoint compatível |

Sem API key? Ollama no Docker: guia oficial **Local Quick Start** (custo zero).

---

## 2. Podcast multi-locutor

- **1–4 locutores** com perfis personalizados (o NotebookLM só dá 2).
- Controle total do roteiro + **Episode Profiles** (formato do episódio).
- Fluxo: crie um notebook → adicione fontes (PDF, vídeo, áudio, web) → gere o podcast.

---

## 3. MCP e API

- **MCP**: guia oficial "MCP Integration" em `docs/` — conecta Claude Desktop, VS Code e outros clientes MCP.
- **API REST**: completa, em `http://localhost:5055` — automação total.

---

## 4. Atualizar e backup

```bash
docker compose pull && docker compose up -d   # atualizar
```

- Faça backup do volume de dados do `surrealdb` antes de atualizar em produção.
- Algo falhou? Guia oficial de troubleshooting (5 minutos), Discord ou GitHub Issues.

---

*Dúvidas? https://www.open-notebook.ai · Entre no Discord oficial.*
