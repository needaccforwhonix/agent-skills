# Weaviate Agent Skills - Setup Instructions

This document provides setup instructions for AI agents using the Weaviate skill and plugin.

## Prerequisites

### 1. Weaviate Cloud Instance

If the user does not have an instance yet, direct them to the cloud console to register and create a free sandbox. Create a Weaviate instance via [Weaviate Cloud](https://console.weaviate.cloud/signin?utm_source=github&utm_campaign=agent_skills).

### 2. Environment Variables

**Required:**

```bash
WEAVIATE_URL="https://your-cluster.weaviate.cloud"
WEAVIATE_API_KEY="your-api-key"
```

**External Provider Keys (auto-detected):**

Set only the keys your collections use:

- `OPENAI_API_KEY`
- `COHERE_API_KEY`
- `HUGGINGFACE_API_KEY`
- `JINAAI_API_KEY`
- `VOYAGE_API_KEY`
- `MISTRAL_API_KEY`
- `NVIDIA_API_KEY`
- `VERTEX_API_KEY`
- `STUDIO_API_KEY`
- `AZURE_API_KEY`
- `ANTHROPIC_API_KEY`
- `ANYSCALE_API_KEY`
- `DATABRICKS_TOKEN`
- `FRIENDLI_TOKEN`
- `XAI_API_KEY`
- `AWS_ACCESS_KEY`
- `AWS_SECRET_KEY`

**Check if variables are set:**

```bash
[ -z "$WEAVIATE_URL" ] && echo "WEAVIATE_URL is NOT set" || echo "WEAVIATE_URL is set"
[ -z "$WEAVIATE_API_KEY" ] && echo "WEAVIATE_API_KEY is NOT set" || echo "WEAVIATE_API_KEY is set"
```

### 3. Python Runtime

All scripts require Python 3.11+.

```bash
python3 --version
```

### 4. uv Package Manager (Recommended)

Scripts use [uv](https://docs.astral.sh/uv/getting-started/installation/) for dependency management.

**Check if uv is installed:**

```bash
uv --version
```

**Install uv if needed:**

```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Or with pip
pip install uv

# Or with Homebrew
brew install uv
```

### Project Structure

| Skill                  | Path                         | Description                                                                       |
| ---------------------- | ---------------------------- | --------------------------------------------------------------------------------- |
| **weaviate**           | `skills/weaviate/`           | Scripts and references for searching, querying, and managing Weaviate collections |
| **weaviate-cookbooks** | `skills/weaviate-cookbooks/` | Implementation guides for building full-stack AI applications with Weaviate       |

## Running Scripts

All scripts are in `skills/weaviate/scripts/`. Run from that directory.

## Available Scripts

For full parameter details, examples, and usage guidance, see the linked references.

### Search & Query

- [Query Agent - Ask Mode](./skills/weaviate/references/ask.md): Generate AI-powered answers with source citations across multiple collections.
- [Query Agent - Search Mode](./skills/weaviate/references/query_search.md): Retrieve raw objects using natural language queries across multiple collections.
- [Hybrid Search](./skills/weaviate/references/hybrid_search.md): Combine vector similarity and keyword matching — the default choice for most searches.
- [Semantic Search](./skills/weaviate/references/semantic_search.md): Pure vector similarity search for finding conceptually similar content.
- [Keyword Search](./skills/weaviate/references/keyword_search.md): BM25 keyword matching for exact terms, IDs, or specific text patterns.

### Collection Management

- [List Collections](./skills/weaviate/references/list_collections.md): Show all available collections with their properties.
- [Get Collection Details](./skills/weaviate/references/get_collection.md): Get detailed configuration of a specific collection including vectorizer, properties, and multi-tenancy settings.
- [Explore Collection](./skills/weaviate/references/explore_collection.md): Get statistical insights, aggregation metrics, and sample data from a collection.
- [Create Collection](./skills/weaviate/references/create_collection.md): Create a new collection with custom schema, optional vectorizer, and multi-tenancy support.

### Data Operations

- [Fetch and Filter](./skills/weaviate/references/fetch_filter.md): Fetch objects by UUID or with complex nested filters (AND, OR logic).
- [Import Data](./skills/weaviate/references/import_data.md): Import data from CSV, JSON, or JSONL files with automatic type conversion and column mapping.

## Dependencies

All scripts use inline dependency declarations (auto-installed via `uv run`):

| Package           | Version  | Used By                 |
| ----------------- | -------- | ----------------------- |
| `weaviate-client` | >=4.19.2 | All scripts             |
| `weaviate-agents` | >=1.2.0  | ask.py, query_search.py |
| `typer`           | >=0.21.0 | All scripts             |

## Weaviate Cookbooks

Weaviate cookbooks are implementation guides for building full-stack AI applications with Weaviate. All cookbooks are in the `skills/weaviate-cookbooks/` skill. For full details and best practices, see the linked references.

- [Query Agent Chatbot](./skills/weaviate-cookbooks/references/query_agent_chatbot.md): Build a full-stack chatbot using Weaviate Query Agent with streaming and chat history support.
- [Data Explorer](./skills/weaviate-cookbooks/references/data_explorer.md): Build a full-stack data explorer app with sorting, keyword search, and tabular data view.
- [Basic RAG](./skills/weaviate-cookbooks/references/basic_rag.md): Implement basic retrieval and generation with Weaviate — covers vector, keyword, hybrid, and image search.
- [Advanced RAG](./skills/weaviate-cookbooks/references/advanced_rag.md): Extend basic RAG with query rewriting, decomposition, LLM-created filters, and re-ranking.
- [Multimodal RAG (PDF)](./skills/weaviate-cookbooks/references/pdf_multimodal_rag.md): Build a multimodal RAG system for PDF documents using Weaviate Embeddings (ModernVBERT/colmodernvbert) and Ollama with Qwen3-VL for generation.
- [Basic Agent](./skills/weaviate-cookbooks/references/basic_agent.md): Build tool-calling AI agents with structured outputs using DSPy.
- [Agentic RAG](./skills/weaviate-cookbooks/references/agentic_rag.md): Build RAG-powered AI agents combining retrieval with agent logic — covers naive RAG tools, hierarchical RAG, vector DB memory, and Weaviate Query Agent.

### Optional Frontend Guide

- [Frontend Interface](./skills/weaviate-cookbooks/references/frontend_interface.md): Build a Next.js frontend (App Router, Tailwind v4, shadcn/ui) to interact with Weaviate backends.

## Contributing

For full guidelines, see [CONTRIBUTING.md](./CONTRIBUTING.md).

### Adding a Reference

1. Create a new `.md` file in `skills/<skill-name>/references/`.
2. Include usage, parameters, examples, and prerequisites.
3. Link the new reference from the skill's `SKILL.md`.

### Creating a New Skill

1. Create directory: `mkdir -p skills/my-skill/references`
2. Add a `SKILL.md` with YAML frontmatter (`name`, `description`) and reference links.
3. Add reference markdown files in `references/`.

Skills follow the [Agent Skills Open Standard](https://agentskills.io/).



## 🛡️ Strict Embedding Separation, Zero-Fallback Law & 24/7 Dual-GPU Invariant
- **Reference**: 

### 1. Das Absolute Fallback-Verbot (Zero-Fallback Law)
Unter keinen Umständen, zu keinem Zeitpunkt und aus keinem Grund darf ein Fallback zwischen verschiedenen Embedding-Modellen stattfinden.
* **Geltende Aktion:** Fällt ein Embedding-Modell aus oder ist überlastet, MUSS die Operation sofort hart fehlschlagen () oder die Payload transaktional in einer Queue (NATS/SQLite) verharren, bis das exakte Modell bereit ist.
* **Verboten:** Kein stiller oder dynamischer Modellwechsel (weder Jina -> Gemma noch umgekehrt).

### 2. Warum ein Embedding-Fallback mathematisch & informationstheoretisch unmöglich ist
* **Topologische Inkompatibilität heterogener Vektorräume (Non-Isomorphism):**
  Jedes Modell 	heta: \mathcal{X} 	o \mathbb{R}^D$ projiziert Text in eine spezifische, gelernte Riemannsche Mannigfaltigkeit. Jina v5 (=256$) und EmbeddingGemma (=768$) spannen zwei völlig inkompatible geometrische Räume auf. Die Basisvektoren der semantischen Achsen sind ohne explizite Procrustes-Transformation nicht ausgerichtet.
* **Kollaps der Kosinus-Ähnlichkeit ($	ext{sim} pprox 0$):**
  Wird eine Suchanfrage mit Modell $ berechnet ( = f_B(q)$), während der Dokumentenkorpus mit Modell $ indiziert wurde ( = f_A(d)$), verhält sich das Skalarprodukt mathematisch wie das zweier rein zufälliger Vektoren auf einer hochdimensionalen Einheitssphäre:
  86306\mathbb{E}[	ext{sim}(u, v)] = 0 \quad 	ext{mit Varianz} \quad \sigma^2 = rac{1}{D}86306
  Der Nearest-Neighbor-Algorithmus (HNSW/k-NN) liefert stochastisches Rauschen. Das RAG-System erhält völlig falsche oder irrelevante Kontexte.
* **Irreversible Index-Vergiftung (Index Poisoning):**
  Wird auch nur ein einziger Vektor von Modell $ als 'Fallback' in den Index von Modell $ geschrieben, verunreinigt er die Distanzgraphen und Clusterzentren dauerhaft.
* **Das Gesetz des Fail-Fast:**
  Ein Ausfall muss hart abbrechen ().

### 3. Duale 24/7 Erfassungspflicht (GPU-Only)
* **GPU-Only Mandat:** Es läuft absolut nichts auf der CPU — GPU ONLY (NVIDIA GB10 CUDA) für ausnahmslos jedes Embedding-Modell.
* **24/7 Parallelität:** Sowohl  (256D, ~4,1 GB VRAM) als auch  (768D, ~1,2 GB VRAM) laufen dauerhaft 24/7 im VRAM (Summe ~5,3 GB VRAM).
* **Duale Erfassung:** Jeder zu indizierende Text/Chunk wird immer von beiden Modellen parallel eingebettet und getrennt persistiert.

### 4. Idioten- & Failsafe-Sicherung auf Datenbankebene
* **SQLite Schema CHECK-Constraints:**
   und  erzwingen atomare Abbrüche auf Engine-Ebene bei Modell-Mismatches.
* **Qdrant Collection Constraints:**
  Strikte Trennung in separate Collections ( vs ) mit fixierter Vektordimension.


## ⚡ High-Quality Systems Programming Languages Priority (No-Python Policy)
- **Reference**: `/home/m1st/.agents/rules/RULE_High_Quality_Systems_Programming_Languages.md`
- **Rule**:
  1. **Bevorzugte Sprachen:** High Quality **Golang (Go), Rust, C++, Zig, PowerShell, C** sind IMMER und AUSNAHMSLOS die bevorzugten Programmiersprachen.
  2. **Kein Python:** Python ist für neue Daemons, Watcher, Automatisierungen, APIs, CLI-Tools und Dienste strikt untersagt (GIL-Bottlenecks, Dependency-Drift, Speicherineffizienz).
  3. **Natives Systems-Engineering:** Alle Hintergrunddienste, Caching-Ebenen und Task-Runner müssen als native, speichersichere und nebenläufige Binaries kompiliert werden.
