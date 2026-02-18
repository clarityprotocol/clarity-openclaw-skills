# Clarity Protocol Skills for Claude Code

Protein folding research skills for [Claude Code](https://code.claude.com) — query variants, literature, clinical data, and AI agent findings from [Clarity Protocol](https://clarityprotocol.io).

## Installation

### Claude Code (Recommended)

```bash
# Add the marketplace
/plugin marketplace add clarityprotocol/clarity-openclaw-skills

# Install the plugin (includes all 5 skills)
/plugin install clarity-protocol@clarity-skills
```

That's it. All skills are now available in your Claude Code sessions.

### Manual / Other AI Agents

Clone this repo and point your agent to the skill folders:

```bash
git clone https://github.com/clarityprotocol/clarity-openclaw-skills.git
```

Skills are in `plugins/clarity-protocol/skills/` — each has a `SKILL.md` with instructions and `scripts/` with Python tools.

## Available Skills

| Skill | Slash Command | Use When |
|-------|--------------|----------|
| **clarity-research** | `/clarity-protocol:clarity-research` | "What variants does Clarity track?" |
| **clarity-variant** | `/clarity-protocol:clarity-variant` | "Show me details for fold 5" |
| **clarity-literature** | `/clarity-protocol:clarity-literature` | "What papers are linked to tau P301L?" |
| **clarity-clinical** | `/clarity-protocol:clarity-clinical` | "What's the ClinVar classification for this variant?" |
| **clarity-fold-status** | `/clarity-protocol:clarity-fold-status` | "How many variants are tracked?" |

Claude also activates skills automatically based on your questions — no slash command needed.

## Example Queries

Ask Claude naturally and the right skill activates:

- "What protein variants are tracked by Clarity Protocol?"
- "Show me the AI analysis for the APP V717I mutation"
- "Find papers about tau P301L"
- "What's the clinical significance of SOD1 A4V?"
- "How many folds has Clarity completed?"

## API Rate Limits

Skills query the public Clarity Protocol API at `https://clarityprotocol.io/api/v1`:

- **Without API key**: 10 requests/minute
- **With API key**: 100 requests/minute

To use an API key, set the environment variable:

```bash
export CLARITY_API_KEY="your-api-key"
```

## API Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /api/v1/info` | API overview and status |
| `GET /api/v1/research/variants` | List all variants |
| `GET /api/v1/research/variants/{fold_id}` | Variant details with AI summary |
| `GET /api/v1/research/variants/{fold_id}/findings` | Agent findings for a variant |
| `GET /api/v1/literature/papers` | List research papers |
| `GET /api/v1/literature/papers/{pmid}` | Paper details by PubMed ID |
| `GET /api/v1/clinical/variants` | Clinical variant data |
| `GET /api/v1/clinical/variants/{protein}/{mutation}` | Single variant clinical data |

## For Developers

Each skill includes Python scripts that can be run directly:

```bash
cd plugins/clarity-protocol/skills

# Query all variants
python clarity-research/scripts/query_variants.py

# Get variant details
python clarity-variant/scripts/get_variant.py --fold-id 5

# Search papers
python clarity-literature/scripts/search_papers.py

# Query clinical data
python clarity-clinical/scripts/query_clinical.py --variant "tau P301L"
```

All scripts support `--format json` for machine-readable output.

**Requirements**: Python 3.7+, `requests` library (`pip install requests`)

## Repository Structure

```
clarity-openclaw-skills/
├── .claude-plugin/
│   └── marketplace.json           # Plugin marketplace catalog
├── plugins/
│   └── clarity-protocol/
│       ├── .claude-plugin/
│       │   └── plugin.json        # Plugin manifest
│       └── skills/
│           ├── clarity-research/   # Search variants by disease/protein
│           ├── clarity-variant/    # Variant details + AI findings
│           ├── clarity-literature/ # PubMed paper search
│           ├── clarity-clinical/   # ClinVar + gnomAD data
│           └── clarity-fold-status/# API overview + status
├── README.md
└── LICENSE
```

## About Clarity Protocol

Clarity Protocol is an autonomous protein folding research pipeline focused on neurodegenerative diseases (Alzheimer's, Parkinson's, ALS, FTD). It combines:

- Local GPU-accelerated protein folding (ColabFold/AlphaFold2)
- Four AI research agents monitoring scientific databases
- Public API for community access to findings
- Downloadable research reports per variant

Visit [clarityprotocol.io](https://clarityprotocol.io) to explore the data.

## License

MIT License - See [LICENSE](LICENSE)
