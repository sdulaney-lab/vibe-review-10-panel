# Vibe Review A+ Panel Evaluation

Run a comprehensive **10-judge panel** evaluation on the target application using P0-P3 severity weighting.

## Usage

```
/vibe-review [TARGET] [CONTEXT]
```

**Arguments:**
- `TARGET`: Application URL (e.g., `http://localhost:5190`) or codebase path (e.g., `/path/to/my-project`)
- `CONTEXT`: Evaluation profile - one of: `dev`, `hackathon`, `mvp`, `staging`, `production`, `enterprise`

---

## Output File Naming Convention

**MANDATORY**: Save all corrective prompts to a single markdown file using this naming pattern:

```
YYYYMMDD-[PROJECT_NAME]-vibe-review.md
```

**Examples:**
- `20251219-my-awesome-app-vibe-review.md`
- `20251219-insightstream-vibe-review.md`
- `20251219-pam-meeting-agent-vibe-review.md`

**Rules:**
1. Use today's date in YYYYMMDD format (no hyphens in date)
2. Extract project name from the TARGET path or URL (use directory name or subdomain)
3. Use lowercase with hyphens for project name
4. Always end with `-vibe-review.md`
5. Save the file in the project's root directory

**File Header Template:**
```markdown
# [PROJECT_NAME] - Vibe Review A+ Panel Results
*Created: YYYY-MM-DD*
*Target: [TARGET]*
*Context: [CONTEXT]*
*Evaluation Profile Strictness: [PROFILE_VALUES]*

---

## Executive Summary
[Overall assessment with letter grade A-F]

## P0 Critical Issues (Blocks Deployment)
[List or "None identified"]

## P1 High Priority Issues
[List or "None identified"]

---

[10 Judge Corrective Prompts follow...]
```

---

## Evaluation Framework

Execute the **Vibe Review A+ Panel** methodology with 10 specialized AI judges:

### Phase 1: Evidence Collection
Using Playwright browser automation (for URLs) and code analysis (for directories), collect:
1. **Visual Evidence**: Screenshots of all major views, responsive breakpoints
2. **Performance Evidence**: Load times, API response times, bundle sizes
3. **Accessibility Evidence**: Lighthouse audit, ARIA compliance, keyboard navigation
4. **Security Evidence**: Authentication flows, input validation, API protection
5. **Functionality Evidence**: Core user flows, error handling, edge cases
6. **Sustainability Evidence**: Carbon region deployment, asset optimization, dark mode support, idle resource consumption

### Phase 2: 10-Judge Evaluation

Each judge evaluates using their behavioral vector calibration:

| Judge | Domain | Behavioral Vector |
|-------|--------|-------------------|
| **Security Specialist** | Auth, API Protection, XSS/SQLI | strictness=0.95, risk_tolerance=0.05, paranoia=0.95 |
| **Performance Analyst** | Speed, Latency, Resources | efficiency_focus=0.95, optimization_mindset=0.9 |
| **UX/Usability Expert** | User Experience, A11y, IA | empathy=0.95, user_advocacy=0.95, accessibility=0.95 |
| **Visual Design Critic** | Aesthetics, Brand, Hierarchy | detail_focus=0.95, creativity=0.85, accessibility=0.9 |
| **Data Guardian** | Integrity, Persistence, Consistency | accuracy=0.95, consistency=0.95, integrity=0.98 |
| **Business Strategist** | Logic, Completeness, Value | business_alignment=0.85, strictness=0.85, user_advocacy=0.85 |
| **Accessibility Guardian** | WCAG, Screen Readers, Cognitive | strictness=0.98, empathy=0.95, inclusivity=0.98 |
| **Infrastructure Architect** | Scalability, Monitoring, DevOps | reliability=0.95, scalability=0.9, observability=0.9 |
| **Developer Experience** | Code Quality, Docs, Maintainability | clarity=0.95, consistency=0.9, maintainability=0.95 |
| **Sustainability Specialist** | Carbon-aware workloads, Energy efficiency, Data minimization | carbon_reflexivity=0.95, computational_parsimony=0.9, infrastructure_stewardship=0.95 |

### Phase 3: P0-P3 Severity Weighting

Classify every finding by severity:
- **P0 - Critical** (blocks deployment): Security breaches, data loss, auth bypasses, high-carbon region deployments with low-carbon alternatives, zombie infrastructure consuming resources
- **P1 - High** (must fix before production): Major UX issues, performance blockers, a11y failures, unoptimized media assets >1MB, lack of dark mode causing unnecessary energy consumption
- **P2 - Medium** (fix in next sprint): Minor bugs, design inconsistencies, code quality, inefficient algorithms with O(n²) complexity, excessive tracking scripts
- **P3 - Low** (nice to have): Polish items, optimizations, future enhancements, missing environmental impact disclosures, SCI scoring documentation

### Phase 4: Cross-Judge Conflict Detection

Flag when judges have:
- Scoring divergence >3 points on same component
- Contradictory findings (e.g., Performance says "remove animation" vs UX says "add animation")
- Domain overlap requiring resolution

### Phase 5: Output Generation

Generate **10 Corrective Prompts** in the output file - one per judge - formatted as:
```markdown
## Judge [N]: [Judge Name]
**Domain**: [Specific expertise]
**Behavioral Vector**: [Key calibration values]

### Critical Issues Identified
1. [Issue with file:line reference if applicable]
2. ...

### Corrective Prompt
[Complete, copy-paste-ready prompt for Claude Code implementation]

### Acceptance Criteria
- [Specific, testable success conditions]
```

---

## Context-Aware Evaluation Profiles

| Profile | Security | Performance | UX | Visual | A11y | Infra | DX | Sustainability | Description |
|---------|----------|-------------|-----|--------|------|-------|-----|----------------|-------------|
| `dev` | 0.4 | 0.4 | 0.6 | 0.4 | 0.3 | 0.2 | 0.4 | 0.2 | Local development, focus on functionality |
| `hackathon` | 0.5 | 0.5 | 0.8 | 0.5 | 0.3 | 0.2 | 0.3 | 0.2 | Speed over polish |
| `mvp` | 0.7 | 0.7 | 0.9 | 0.7 | 0.6 | 0.5 | 0.5 | 0.5 | Minimum viable product |
| `staging` | 0.9 | 0.8 | 0.9 | 0.8 | 0.8 | 0.7 | 0.7 | 0.7 | Pre-production testing |
| `production` | 0.95 | 0.9 | 0.95 | 0.85 | 0.95 | 0.9 | 0.8 | 0.85 | Live deployment |
| `enterprise` | 0.98 | 0.95 | 0.95 | 0.9 | 0.98 | 0.95 | 0.9 | 0.95 | Enterprise compliance |

**Note**: `development` is an alias for `dev`

---

## Example Invocations

```bash
# Evaluate local dev server (lenient)
/vibe-review http://localhost:5190 dev

# Evaluate codebase directory for MVP readiness
/vibe-review /path/to/my-project mvp

# Evaluate production deployment (strictest)
/vibe-review https://myapp.com production
```

---

**Begin evaluation now.**

1. Determine project name from TARGET
2. Create output file: `YYYYMMDD-[project-name]-vibe-review.md`
3. Use Playwright for browser evidence collection (URLs) or code analysis (directories)
4. Generate 10 corrective prompts prioritized by P0-P3 severity
5. Save all results to the output file in the project's root directory
