# Clarity Protocol OpenClaw Skills

OpenClaw skills for querying protein folding data from [Clarity Protocol](https://clarityprotocol.io).

## Available Skills

| Skill | Description | Use When |
|-------|-------------|----------|
| **clarity-research** | Search protein variants by disease or protein name | "What variants does Clarity track?" |
| **clarity-variant** | Get detailed variant info with AI summary | "Show me details for fold 5" |
| **clarity-literature** | Search papers and get paper details | "What papers are linked to tau P301L?" |
| **clarity-clinical** | Query ClinVar/gnomAD clinical data | "What's the ClinVar classification for this variant?" |
| **clarity-fold-status** | API overview and status check | "How many variants are tracked?" |

## Installation

### Option 1: Manual Installation

1. Clone this repository:
```bash
git clone https://github.com/clarityprotocol/clarity-openclaw-skills.git
cd clarity-openclaw-skills
```

2. Copy skill folders to your AI agent's skills directory:
```bash
# For Claude Desktop (example path)
cp -r clarity-* ~/Library/Application\ Support/Claude/skills/

# Or your agent's custom skills path
cp -r clarity-* /path/to/agent/skills/
```

3. (Optional) Set API key for higher rate limits:
```bash
export CLARITY_API_KEY="your-api-key"
```

Without API key: 10 requests/minute (IP-based)
With API key: 100 requests/minute

### Option 2: Direct Skill Installation

Each skill can be installed independently by copying its folder.

## Usage

### For AI Agents

Skills are automatically activated when you ask relevant questions:

- "What protein variants are tracked by Clarity Protocol?"
- "Show me the AI analysis for fold 12"
- "Find papers about tau P301L"
- "What's the clinical significance of this variant?"

### For Developers

Each skill includes Python scripts that can be run directly:

```bash
# Query all variants
python3 clarity-research/scripts/query_variants.py

# Get variant details
python3 clarity-variant/scripts/get_variant.py --fold-id 5

# Search papers
python3 clarity-literature/scripts/search_papers.py

# Query clinical data
python3 clarity-clinical/scripts/query_clinical.py --variant "tau P301L"
```

All scripts support `--format json` for machine-readable output.

## API Endpoints

Skills query the public Clarity Protocol API at `https://clarityprotocol.io/api/v1`:

- `GET /research/variants` - List all variants
- `GET /research/variants/{fold_id}` - Variant details
- `GET /research/variants/{fold_id}/findings` - Agent findings
- `GET /literature/papers` - List papers
- `GET /literature/papers/{pmid}` - Paper details
- `GET /clinical/variants` - Clinical variant data
- `GET /clinical/variants/{protein}/{mutation}` - Single variant clinical data
- `GET /info` - API info and status

Rate limits:
- Anonymous (IP-based): 10 requests/minute, 100 requests/hour
- Authenticated (API key): 100 requests/minute, 1000 requests/hour

## Requirements

- Python 3.7+
- `requests` library (`pip install requests`)

## License

MIT License - See [LICENSE](LICENSE)

## About Clarity Protocol

Clarity Protocol is an autonomous protein folding research pipeline focused on neurodegenerative diseases (Alzheimer's, Parkinson's, ALS, FTD). It combines:

- Local GPU-accelerated protein folding (ColabFold)
- AI research agents for literature and clinical data analysis
- Public API for community access to findings

Visit [clarityprotocol.io](https://clarityprotocol.io) to explore the data.
