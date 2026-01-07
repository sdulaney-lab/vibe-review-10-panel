# Vibe Review 10-Panel: AI Application Evaluation Framework
*Created: 2025-12-19*
*Updated: 2026-01-06 - Now with 11 Judges including AI Governance*

A comprehensive **11-judge AI panel** evaluation system for applications, featuring specialized judges with mathematical behavioral calibration and P0-P3 severity-weighted corrective prompts.

> **Note**: The repo is named "10-Panel" for historical reasons, but the framework now includes **11 judges** with the addition of the AI Governance Specialist in January 2026.

## Quick Start

### 1. Clone This Repository
```bash
git clone https://github.com/YOUR_ORG/vibe-review-10-panel.git
```

### 2. Copy Slash Command to Your Project
```bash
# Copy the slash command to your project's .claude/commands directory
cp vibe-review-10-panel/.claude/commands/vibe-review.md YOUR_PROJECT/.claude/commands/
```

### 3. Run Vibe Review
```bash
# In Claude Code, simply type:
/vibe-review http://localhost:5000 dev
```

---

## What is Vibe Review?

Vibe Review is a **multi-agent evaluation framework** that simulates 11 specialized AI judges, each with distinct expertise and behavioral calibration. The system:

1. **Collects Evidence** using Playwright browser automation (for URLs) or code analysis (for directories)
2. **Evaluates** through 11 specialized judge perspectives
3. **Classifies Findings** by P0-P3 severity
4. **Generates Corrective Prompts** - copy-paste ready fixes for Claude Code

---

## The 11 Judges

| # | Judge | Domain | Behavioral Vector |
|---|-------|--------|-------------------|
| 1 | **Security Specialist** | Auth, API Protection, XSS/SQLI | strictness=0.95, risk_tolerance=0.05, paranoia=0.95 |
| 2 | **Performance Analyst** | Speed, Latency, Resources | efficiency_focus=0.95, optimization_mindset=0.9 |
| 3 | **UX/Usability Expert** | User Experience, A11y, IA | empathy=0.95, user_advocacy=0.95, accessibility=0.95 |
| 4 | **Visual Design Critic** | Aesthetics, Brand, Hierarchy | detail_focus=0.95, creativity=0.85, accessibility=0.9 |
| 5 | **Data Guardian** | Integrity, Persistence, Consistency | accuracy=0.95, consistency=0.95, integrity=0.98 |
| 6 | **Business Strategist** | Logic, Completeness, Value | business_alignment=0.85, strictness=0.85, user_advocacy=0.85 |
| 7 | **Accessibility Guardian** | WCAG, Screen Readers, Cognitive | strictness=0.98, empathy=0.95, inclusivity=0.98 |
| 8 | **Infrastructure Architect** | Scalability, Monitoring, DevOps | reliability=0.95, scalability=0.9, observability=0.9 |
| 9 | **Developer Experience** | Code Quality, Docs, Maintainability | clarity=0.95, consistency=0.9, maintainability=0.95 |
| 10 | **Sustainability Specialist** | Carbon-aware workloads, Energy efficiency | carbon_reflexivity=0.95, computational_parsimony=0.9, infrastructure_stewardship=0.95 |
| 11 | **AI Governance Specialist** | LLM Safety, Prompt Security, AI Ethics | compliance=0.95, ethics=0.95, safety_focus=0.98 |

### Judge 11: AI Governance Specialist (New in v2.0)

Added January 2026 to address AI-specific concerns aligned with enterprise AI production guidelines:

- **OWASP LLM Top 10**: Prompt injection (LLM01), output sanitization (LLM02), training data poisoning (LLM03), model DoS (LLM04), excessive agency (LLM08)
- **Prompt Management**: Centralized registry, semantic versioning, change management
- **AI Safety**: Hallucination detection, confidence scoring, human-in-the-loop for high-stakes decisions
- **Cognitive Architecture**: Chain-of-thought logging, grounded truth (RAG), guardrails

---

## Severity Classification (P0-P3)

| Severity | Meaning | Examples |
|----------|---------|----------|
| **P0 - Critical** | Blocks deployment | Security breaches, data loss, auth bypasses, high-carbon deployments, zombie infrastructure |
| **P1 - High** | Must fix before production | Major UX issues, performance blockers, a11y failures, unoptimized assets >1MB |
| **P2 - Medium** | Fix in next sprint | Minor bugs, design inconsistencies, inefficient algorithms, excessive tracking |
| **P3 - Low** | Nice to have | Polish items, optimizations, missing disclosures |

---

## Context-Aware Evaluation Profiles

Choose the right profile for your application's stage:

| Profile | Security | Performance | UX | Visual | A11y | Infra | DX | Sustainability | AI Gov | Use Case |
|---------|----------|-------------|-----|--------|------|-------|-----|----------------|--------|----------|
| `dev` | 0.4 | 0.4 | 0.6 | 0.4 | 0.3 | 0.2 | 0.4 | 0.2 | 0.3 | Local development |
| `hackathon` | 0.5 | 0.5 | 0.8 | 0.5 | 0.3 | 0.2 | 0.3 | 0.2 | 0.4 | Speed over polish |
| `mvp` | 0.7 | 0.7 | 0.9 | 0.7 | 0.6 | 0.5 | 0.5 | 0.5 | 0.6 | Minimum viable product |
| `staging` | 0.9 | 0.8 | 0.9 | 0.8 | 0.8 | 0.7 | 0.7 | 0.7 | 0.8 | Pre-production |
| `production` | 0.95 | 0.9 | 0.95 | 0.85 | 0.95 | 0.9 | 0.8 | 0.85 | 0.9 | Live deployment |
| `enterprise` | 0.98 | 0.95 | 0.95 | 0.9 | 0.98 | 0.95 | 0.9 | 0.95 | 0.98 | Enterprise compliance |

---

## Installation

See [SETUP.md](docs/SETUP.md) for detailed Claude Code integration instructions.

### Quick Installation

1. **Create the commands directory** in your project:
   ```bash
   mkdir -p .claude/commands
   ```

2. **Copy the slash command**:
   ```bash
   cp .claude/commands/vibe-review.md YOUR_PROJECT/.claude/commands/
   ```

3. **Verify installation** - in Claude Code:
   ```
   /vibe-review http://localhost:3000 dev
   ```

---

## Usage Examples

```bash
# Evaluate local dev server (lenient)
/vibe-review http://localhost:5190 dev

# Evaluate codebase directory for MVP readiness
/vibe-review /Users/yourname/Documents/my-project mvp

# Evaluate staging deployment
/vibe-review https://staging.myapp.com staging

# Evaluate production deployment (strictest)
/vibe-review https://myapp.com production
```

---

## Output Format

Vibe Review generates a markdown file with:
- Executive Summary with letter grade (A-F)
- P0/P1 Critical Issues summary
- 11 Corrective Prompts (one per judge)

**Output file naming**: `YYYYMMDD-[project-name]-vibe-review.md`

See [docs/EXAMPLE_OUTPUT.md](docs/EXAMPLE_OUTPUT.md) for a sample report.

---

## Project Structure

```
vibe-review-10-panel/
├── README.md                    # This file
├── .claude/
│   └── commands/
│       └── vibe-review.md       # The slash command (copy to your project)
├── docs/
│   ├── SETUP.md                 # Detailed setup instructions
│   ├── METHODOLOGY.md           # Full methodology documentation
│   ├── JUDGES.md                # Deep dive on each judge
│   ├── EXAMPLE_OUTPUT.md        # Sample vibe review report
│   └── SUSTAINABILITY.md        # Green Software Engineering principles
└── examples/
    └── sample-vibe-review.md    # Real example output
```

---

## Requirements

- **Claude Code** (claude.ai/code) - Anthropic's CLI for Claude
- **Playwright MCP** (optional but recommended) - For browser automation when evaluating URLs

---

## Contributing

1. Fork this repository
2. Create a feature branch
3. Submit a Pull Request

---

## License

MIT License - Use freely in your projects.

---

## Credits

Developed by AI Garage team. Sustainability judge inspired by Green Software Foundation principles.
