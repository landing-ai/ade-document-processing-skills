# ADE Document Processing Skills

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Agent skills for [LandingAI's Agentic Document Extraction (ADE)](https://landing.ai/) — production-ready document AI that converts complex, real-world documents into accurate, structured data with full auditability and traceability.

These skills teach agentic coding assistants (Claude, Cursor, Roo Code, or any agent supporting the [Agent Skills](https://agentskills.io/home) convention) how to write Python scripts that parse, extract, classify, and build processing pipelines for documents — without templates or ML training.

## Why ADE?

- **Vision-first** — Proprietary models that understand layout, not just text. Handles complex tables, dense forms, multi-column pages, and scanned documents
- **Accurate** — [99.16% on DocVQA](https://landing.ai/blog/superhuman-on-docvqa-without-images-in-qa-agentic-document-extraction), proven on 1B+ documents processed
- **Traceable** — Every extracted value includes bounding boxes, page coordinates, and confidence scores traceable back to the source document
- **Agentic by design** — Adapts to each document autonomously, planning and verifying until quality thresholds are met
- **20+ file formats** — PDF, images, spreadsheets, presentations, and more — no templates required

## Skills

### document-extraction

Core ADE SDK operations for parsing and extracting document content.

- **Parse** documents into structured Markdown with layout awareness and hierarchical JSON
- **Extract** specific fields using JSON schemas or Pydantic models (invoices, forms, tables)
- **Split** and classify multi-document batches by type (invoices vs receipts, statements vs forms)
- **Process large files** asynchronously (up to 1 GB / 6,000 pages)
- **Visual grounding** — precise bounding boxes, page numbers, and confidence scores for every element

### document-workflows

End-to-end pipeline patterns that compose ADE operations into production workflows.

- **Batch process** documents in parallel (sync with ThreadPoolExecutor or async)
- **Classify-then-extract** pipelines for mixed document types
- **RAG preparation** — semantic chunking, embeddings, ChromaDB/FAISS ingestion
- **Export** structured results to DataFrames, CSV, or Snowflake
- **Visualize** extractions — bounding box overlays, chunk cropping, page annotations
- **Word-level grounding** — find and highlight specific terms within document sections
- Build **Streamlit UIs** for interactive document processing

## Prerequisites

- A **VISION_AGENT_API_KEY** from [LandingAI](https://va.landing.ai/settings/api-key) (free trial, no credit card required)
- A Python environment (e.g. [uv](https://docs.astral.sh/uv/) or venv) — the skills install `landingai-ade` and other dependencies as needed

## Installation

### For Claude Code agents

```
# Step 1: Add the marketplace 
/plugin marketplace add landing-ai/ade-document-processing-skills

# Step 2: Install the plugin
/plugin install ade-document-processing@ade-document-processing-skills
```

### Manual installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/landing-ai/ade-document-processing-skills.git
   ```

2. **Copy the skills** into your project or home directory:

   ```bash
   # Project-level (skills apply to this project only)
   cp -R ade-document-processing-skills/plugins/ade-document-processing/skills/document-extraction  YOUR_PROJECT/.claude/skills/
   cp -R ade-document-processing-skills/plugins/ade-document-processing/skills/document-workflows   YOUR_PROJECT/.claude/skills/

   # Global (skills available in all projects)
   cp -R ade-document-processing-skills/plugins/ade-document-processing/skills/document-extraction  ~/.claude/skills/
   cp -R ade-document-processing-skills/plugins/ade-document-processing/skills/document-workflows   ~/.claude/skills/
   ```

### Set up your API key

Create a `.env` file in your project root:

```bash
echo 'VISION_AGENT_API_KEY=your-key-here' > .env
```

Get your key at [va.landing.ai/settings/api-key](https://va.landing.ai/settings/api-key).

## Usage

The skills guide your agent to write Python scripts that process documents using ADE. Ask your agentic assistant:

> "Write a Python script that reads all invoices under `./documents/` and extracts the line items, descriptions, and prices as a CSV file"
>
> "Write a script that extracts all figures from this scientific paper as individual PNG files"
>
> "Write a script that reads account statements and extracts all transactions across pages into a single CSV file"
>
> "Write a script that extracts the introduction section from this PDF and highlights every occurrence of a specific term with a translucent red overlay"
>
> "Write a Python script that reads all PDFs in a folder, extracts the abstract and introduction sections, and saves them as plain text files"

The skills handle dependency installation, API client setup, and error handling automatically.

## Repository Structure

```
├── .claude-plugin/
│   └── marketplace.json          # Maps plugins for discovery
├── plugins/
│   └── ade-document-processing/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin manifest listing skills
│       └── skills/
│           ├── document-extraction/
│           │   ├── SKILL.md      # Core ADE SDK skill
│           │   └── references/   # Detailed reference docs
│           └── document-workflows/
│               ├── SKILL.md      # Pipeline patterns skill
│               └── references/   # Detailed reference docs
├── LICENSE
└── README.md
```

## Links

- [LandingAI](https://landing.ai/) — Agentic Document Extraction platform
- [ADE Documentation](https://docs.landing.ai/ade/)
- [ADE Python Library](https://github.com/landing-ai/ade-python)
- [Agent Skills Convention](https://agentskills.io/home)

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
