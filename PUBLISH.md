# Publishing Clarity OpenClaw Skills

## Repository Status

**Local repository:** `/home/absent/clarity-openclaw-skills`
**Commit:** 8655186 (initial commit with 5 skills)
**Branch:** main
**Files:** 17 (5 SKILL.md, 8 Python scripts, shared modules, LICENSE, README, .gitignore)

## Option 1: Create GitHub Repository (Recommended)

### Via GitHub Web UI

1. Go to: https://github.com/new
2. Settings:
   - Owner: `clarityprotocol`
   - Repository name: `clarity-openclaw-skills`
   - Description: `OpenClaw skills for querying Clarity Protocol protein folding data`
   - Public repository
   - Do NOT initialize with README (we already have one)
3. Click "Create repository"
4. Push from terminal:

```bash
cd /home/absent/clarity-openclaw-skills
git remote add origin git@github.com:clarityprotocol/clarity-openclaw-skills.git
git push -u origin main
```

### Via GitHub CLI (if available)

```bash
cd /home/absent/clarity-openclaw-skills
gh repo create clarityprotocol/clarity-openclaw-skills --public --source=. --push \
  --description "OpenClaw skills for querying Clarity Protocol protein folding data"
```

## Option 2: Publish to ClawHub Marketplace (When Available)

The `openclaw` CLI is not yet publicly available. Once it's released:

### Validate Skills

```bash
openclaw skill validate clarity-research
openclaw skill validate clarity-variant
openclaw skill validate clarity-literature
openclaw skill validate clarity-clinical
openclaw skill validate clarity-fold-status
```

### Publish Skills

```bash
openclaw skill publish clarity-research
openclaw skill publish clarity-variant
openclaw skill publish clarity-literature
openclaw skill publish clarity-clinical
openclaw skill publish clarity-fold-status
```

Or upload via ClawHub web UI (if available).

## Verification Checklist

- [x] 5 SKILL.md files with valid YAML frontmatter
- [x] 8 Python scripts with shared api_client.py
- [x] No hardcoded credentials (verified with grep)
- [x] MIT License included
- [x] README with installation instructions
- [x] .gitignore for Python artifacts
- [x] Git repository initialized and committed

## Testing Skills Locally

Before publishing, verify skills work:

```bash
# Set API key (optional, for higher rate limits)
export CLARITY_API_KEY="your-key-here"

# Test each skill
cd /home/absent/clarity-openclaw-skills

python3 clarity-research/scripts/query_variants.py --format summary
python3 clarity-variant/scripts/get_variant.py --fold-id 1
python3 clarity-literature/scripts/search_papers.py
python3 clarity-clinical/scripts/query_clinical.py --variant "tau P301L"
python3 clarity-fold-status/scripts/check_status.py
```

Expected: User-friendly output or clear error messages (not stack traces).

## Distribution Channels

1. **GitHub** (primary): Public repository for git clone / direct download
2. **ClawHub** (future): Marketplace listing with VirusTotal scanning
3. **Clarity Protocol Website**: Link to GitHub repository from docs

## Post-Publication

After GitHub push, add to Clarity Protocol documentation:
- Link from https://clarityprotocol.io/docs
- Add to PROJECT.md in main repository
- Tweet announcement with #OpenClaw hashtag
