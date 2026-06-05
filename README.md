# claude-genomics-plugins

Claude Code plugins for genomic analysis. Two plugins included:

## Plugins

### 1. genomic-analysis-toolkit

HIBLUP genomic prediction / rMVP GWAS analysis assistant with format-confusion prevention.

**Skill:** `/genomic-analysis-toolkit:genomic-analysis`

**Features:**
- **HIBLUP mode** — Genomic prediction, GEBV, heritability estimation, cross-validation → outputs Bash commands
- **rMVP mode** — GWAS association analysis, Manhattan/QQ plots → outputs R scripts
- Automatic phenotype format conversion when switching between tools
- Format validation gate (HIBLUP: IID+Trait columns; rMVP: Taxa+Trait columns)

### 2. genomics-team

Multi-agent team workflow for genomic prediction pipeline development.

**Skill:** `/genomics-team:genomics-team`

**Workflow:** Review → Plan → Dev → Test/Deploy

**Features:**
- Automated code review with genomics-aware agents
- Parallel development (up to 3 concurrent Dev agents)
- Built-in failure recovery (3-retry with escalating context)
- Git push + deployment integration

## Installation

### Option 1: Install both plugins

Add this repo as a marketplace in your `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "genomics-plugins": {
      "source": {
        "source": "directory",
        "path": "https://github.com/lzy1217-colud/claude-genomics-plugins.git"
      }
    }
  },
  "enabledPlugins": {
    "genomic-analysis-toolkit@genomics-plugins": true,
    "genomics-team@genomics-plugins": true
  }
}
```

Then restart Claude Code. The plugins will be available as:
- `/genomic-analysis-toolkit:genomic-analysis`
- `/genomics-team:genomics-team`

### Option 2: Install via Claude Code CLI

```bash
# Add the marketplace
claude plugin add-marketplace genomics-plugins https://github.com/lzy1217-colud/claude-genomics-plugins.git

# Install individual plugins
claude plugin install genomic-analysis-toolkit@genomics-plugins
claude plugin install genomics-team@genomics-plugins
```

## Required Agent Definitions (genomics-team only)

The `genomics-team` plugin uses custom subagents. For full functionality, you also need these agent definitions in `~/.claude/agents/`:

- `genomics-reviewer.md` — Code review agent
- `genomics-planner.md` — Planning agent
- `genomics-dev.md` — Development agent
- `genomics-test-deploy.md` — Testing & deployment agent

See the [agents template](./agents/) for examples you can customize for your project.

## Requirements

- **HIBLUP mode:** HIBLUP installed, PLINK binary files (.bed/.bim/.fam) or VCF
- **rMVP mode:** R with `rMVP` package installed, bgzip-compressed VCF with tabix index
- **genomics-team:** A git-tracked project directory

## License

MIT
