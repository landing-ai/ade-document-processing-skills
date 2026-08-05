# ADE Document Processing Skills

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An agent skill for [LandingAI's Agentic Document Extraction (ADE)](https://landing.ai/): production-ready document AI that converts complex, real-world documents into accurate, structured data with full auditability and traceability.

The skill teaches agentic coding assistants (Claude, Cursor, Roo Code, or any agent supporting the [Agent Skills](https://agentskills.io/home) convention) how to parse, extract, classify, and split documents, and how to compose those operations into processing pipelines, using the ADE REST APIs or the official Python and TypeScript libraries. No templates or ML training required.

## Prerequisites

- A **VISION_AGENT_API_KEY** from [LandingAI](https://va.landing.ai/settings/api-key) (free trial, no credit card required)
- A Python environment (e.g. [uv](https://docs.astral.sh/uv/) or venv) if your agent writes Python; the skill installs `landingai-ade` and other dependencies as needed

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

2. **Copy the skill** into your project or home directory:

   ```bash
   # Project-level (skill applies to this project only)
   cp -R ade-document-processing-skills/plugins/ade-document-processing/skills/document-extraction  YOUR_PROJECT/.claude/skills/

   # Global (skill available in all projects)
   cp -R ade-document-processing-skills/plugins/ade-document-processing/skills/document-extraction  ~/.claude/skills/
   ```

### Set up your API key

Create a `.env` file in your project root:

```bash
echo 'VISION_AGENT_API_KEY=your-key-here' > .env
```

Get your key at [va.landing.ai/settings/api-key](https://va.landing.ai/settings/api-key).

## Why ADE?

- **Vision-first**: Proprietary models that understand layout, not just text. Handles complex tables, dense forms, multi-column pages, and scanned documents
- **Accurate**: [99.16% on DocVQA](https://landing.ai/blog/superhuman-on-docvqa-without-images-in-qa-agentic-document-extraction), proven on 1B+ documents processed
- **Traceable**: Extracted values include bounding boxes and page coordinates traceable back to the source document
- **Agentic by design**: Adapts to each document autonomously, planning and verifying until quality thresholds are met
- **20+ file formats**: PDF, images, spreadsheets, presentations, and more, with no templates required

## The Skill

### document-extraction

Covers the full ADE surface, from single API operations to the pipeline patterns that compose them. It defaults to the current v2 (DPT-3) APIs and routes to the v1 APIs for the capabilities that live there.

Core operations:

- **Parse** documents into structured Markdown with layout awareness and hierarchical JSON
- **Extract** specific fields using JSON schemas or Pydantic models (invoices, forms, tables)
- **Split** multi-document batches into separate documents by type (invoices vs receipts, statements vs forms)
- **Classify** each page by type to route pages before parsing
- **Generate a table of contents** from a document's hierarchical section structure
- **Process large files and long extractions** asynchronously with Parse Jobs and Extract Jobs
- **Visual grounding**: precise bounding boxes and page numbers for every element

Pipeline patterns:

- **Batch process** documents in parallel
- **Classify-then-extract** pipelines for mixed document types
- **RAG preparation**: semantic chunking, embeddings, vector database ingestion
- **Table stitching** for tables that span multiple pages
- **Export** structured results to DataFrames, CSV, or databases
- **Visualize** extractions: bounding box overlays, chunk cropping, word-level highlighting

## Usage

The skill guides your agent to write code that processes documents using ADE. Ask your agentic assistant:

> "Write a Python script that reads all invoices under `./documents/` and extracts the line items, descriptions, and prices as a CSV file"
>
> "Write a script that extracts all figures from this scientific paper as individual PNG files"
>
> "Write a script that reads account statements and extracts all transactions across pages into a single CSV file"
>
> "Write a script that extracts the introduction section from this PDF and highlights every occurrence of a specific term with a translucent red overlay"
>
> "Write a Python script that reads all PDFs in a folder, extracts the abstract and introduction sections, and saves them as plain text files"

The skill includes guidance and patterns for dependency installation, API client setup, and error handling, so your agent handles these for you.

## Repository Structure

```
├── .claude-plugin/
│   └── marketplace.json          # Maps plugins for discovery
├── plugins/
│   └── ade-document-processing/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin manifest listing skills
│       └── skills/
│           └── document-extraction/
│               └── SKILL.md      # The ADE skill
├── LICENSE
└── README.md
```

## Links

- [LandingAI](https://landing.ai/): Agentic Document Extraction platform
- [ADE Documentation (v2)](https://docs.landing.ai/dpt3/overview)
- [ADE Documentation (v1)](https://docs.landing.ai/ade/ade-overview)
- [ADE Python Library](https://github.com/landing-ai/ade-python)
- [ADE TypeScript Library](https://github.com/landing-ai/ade-typescript)
- [Agent Skills Convention](https://agentskills.io/home)

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
