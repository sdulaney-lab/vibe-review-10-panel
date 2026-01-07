# Vibe Review A+ Panel Evaluation

Run a comprehensive **11-judge panel** evaluation on the target application using P0-P3 severity weighting. Updated to include AI/LLM-specific evaluation criteria aligned with production deployment guidelines.

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

[11 Judge Corrective Prompts follow...]
```

---

## Evaluation Framework

Execute the **Vibe Review A+ Panel** methodology with 11 specialized AI judges:

### Phase 1: Evidence Collection
Using Playwright browser automation (for URLs) and code analysis (for directories), collect:
1. **Visual Evidence**: Screenshots of all major views, responsive breakpoints
2. **Performance Evidence**: Load times, API response times, bundle sizes, LLM latency metrics
3. **Accessibility Evidence**: Lighthouse audit, ARIA compliance, keyboard navigation
4. **Security Evidence**: Authentication flows, input validation, API protection, prompt injection vectors
5. **Functionality Evidence**: Core user flows, error handling, edge cases
6. **Sustainability Evidence**: Carbon region deployment, asset optimization, dark mode support, idle resource consumption
7. **AI/LLM Evidence**: Prompt management, RAG implementation, output sanitization, hallucination handling

### Phase 2: 11-Judge Evaluation

Each judge evaluates using their behavioral vector calibration:

| Judge | Domain | Behavioral Vector |
|-------|--------|-------------------|
| **1. Security Specialist** | Auth, API Protection, XSS/SQLI, AI Attack Vectors | strictness=0.95, risk_tolerance=0.05, paranoia=0.95 |
| **2. Performance Analyst** | Speed, Latency, Resources, LLM Metrics | efficiency_focus=0.95, optimization_mindset=0.9 |
| **3. UX/Usability Expert** | User Experience, A11y, IA, AI Interaction Patterns | empathy=0.95, user_advocacy=0.95, accessibility=0.95 |
| **4. Visual Design Critic** | Aesthetics, Brand, Hierarchy, AI Interface Patterns | detail_focus=0.95, creativity=0.85, accessibility=0.9 |
| **5. Data Guardian** | Integrity, Persistence, Consistency, AI Data Trails | accuracy=0.95, consistency=0.95, integrity=0.98 |
| **6. Business Strategist** | Logic, Completeness, Value, AI ROI | business_alignment=0.85, strictness=0.85, roi_focus=0.9 |
| **7. Accessibility Guardian** | WCAG, Screen Readers, Cognitive, AI Content A11y | strictness=0.98, empathy=0.95, inclusivity=0.98 |
| **8. Infrastructure Architect** | Scalability, Monitoring, DevOps, LLM Provider Health | reliability=0.95, scalability=0.9, observability=0.9 |
| **9. Developer Experience** | Code Quality, Docs, Maintainability, Prompt Management | clarity=0.95, consistency=0.9, maintainability=0.95 |
| **10. Sustainability Specialist** | Carbon-aware, Energy efficiency, AI Inference Efficiency | carbon_reflexivity=0.95, computational_parsimony=0.9 |
| **11. AI Governance Specialist** | LLM Safety, Prompt Engineering, Hallucination Management | trustworthiness=0.95, safety_rigor=0.95, transparency=0.90 |

---

## Detailed Judge Evaluation Criteria

### Judge 1: Security Specialist ("The Paranoid Guardian")
**Domain**: Authentication, API Protection, Vulnerability Detection, AI Attack Vectors
**Behavioral Vector**: `strictness=0.95, risk_tolerance=0.05, paranoia=0.95, compliance_focus=0.9`

**Traditional Security Criteria:**
- **P0 Critical**: SQL injection, XSS, auth bypasses, exposed API keys, missing HTTPS, broken access control
- **P1 High**: CSRF protection, password policies, session management, rate limiting, dependency CVEs
- **P2 Medium**: Security headers, verbose errors, excessive logging of sensitive data, input sanitization
- **P3 Low**: Documentation gaps, missing security.txt, suboptimal CSP policies

**AI-Specific Security Criteria (OWASP LLM Top 10):**
- **P0 Critical**:
  - Prompt injection vulnerabilities in user-facing AI inputs (LLM01)
  - AI outputs returning sensitive data without sanitization (LLM02)
  - LLM provider API keys exposed in client-side code
  - No authentication on AI inference endpoints
  - Training data poisoning vectors (LLM03)
- **P1 High**:
  - Missing prompt injection filters/scanning
  - AI responses not sanitized for PII before display
  - No rate limiting on AI inference endpoints
  - JWT tokens accepting "none" algorithm or missing exp validation
  - Insecure output handling allowing code execution (LLM02)
  - Model denial of service vulnerabilities (LLM04)
- **P2 Medium**:
  - DLP scanning not applied to AI outputs
  - AI conversation logs stored without encryption
  - Missing audit trail for AI-human interactions
  - Excessive agency granted to AI without human approval (LLM08)
- **P3 Low**:
  - Missing AI security documentation
  - No adversarial input testing documented

---

### Judge 2: Performance Analyst ("The Speed Demon")
**Domain**: Load Times, Latency, Resource Optimization, LLM Performance Metrics
**Behavioral Vector**: `efficiency_focus=0.95, optimization_mindset=0.9, user_patience_model=0.85`

**Traditional Performance Criteria:**
- **P0 Critical**: Page load >10s, API timeouts, memory leaks, bundle >5MB uncompressed
- **P1 High**: First Contentful Paint >3s, LCP >4s, CLS >0.25, images >500KB
- **P2 Medium**: Missing lazy loading, unnecessary re-renders, uncompressed assets, missing cache headers
- **P3 Low**: Sub-optimal code splitting, missing preload hints, font loading optimization

**AI-Specific Performance Criteria:**
- **P0 Critical**:
  - LLM response timeout >30s without user feedback
  - Token streaming not implemented (blocking full response wait)
  - Memory leaks from conversation context accumulation
  - No timeout handling for LLM provider calls
- **P1 High**:
  - LLM first-token latency >3s without loading state
  - No token usage monitoring/budgeting
  - Missing graceful degradation when LLM provider slow/unavailable
  - Full context sent on every request (no context windowing)
- **P2 Medium**:
  - Response streaming chunks too large (>100 tokens per chunk)
  - No caching for repeated similar queries (semantic caching)
  - Missing LLM provider latency dashboarding
  - Synchronous LLM calls blocking main thread
- **P3 Low**:
  - No request batching for multiple AI calls
  - Missing performance comparison across model providers

---

### Judge 3: UX/Usability Expert ("The User Advocate")
**Domain**: User Experience, Information Architecture, Interaction Design, AI Interaction Patterns
**Behavioral Vector**: `empathy=0.95, user_advocacy=0.95, accessibility=0.95, forgiveness=0.8`

**Traditional UX Criteria:**
- **P0 Critical**: Core user flow broken, critical functionality unreachable, data loss on common actions, unusable on mobile
- **P1 High**: Confusing navigation, missing action feedback, unclear errors, poor mobile experience
- **P2 Medium**: Inconsistent patterns, missing loading states, suboptimal forms, minor mobile issues
- **P3 Low**: Micro-interaction polish, empty state improvements, onboarding enhancements

**AI-Specific UX Criteria:**
- **P0 Critical**:
  - AI processing with no user feedback (frozen UI)
  - AI errors crash the application
  - No way to cancel/stop AI generation
- **P1 High**:
  - No loading/thinking indicator during AI processing
  - Missing "AI is typing" feedback for conversational interfaces
  - No way for users to report AI errors/hallucinations
  - AI responses don't distinguish facts from generated content
  - No clear indication of AI capabilities and limitations
- **P2 Medium**:
  - No conversation history/context visibility
  - Missing AI confidence indicators where appropriate
  - No "regenerate" option for unsatisfactory responses
  - Unclear AI capability boundaries in UI
  - AI reasoning (CoT) not visible when useful for user trust
- **P3 Low**:
  - No user preference settings for AI behavior
  - Missing AI interaction tutorials/onboarding

---

### Judge 4: Visual Design Critic ("The Pixel Perfectionist")
**Domain**: Aesthetics, Brand Consistency, Visual Hierarchy, AI Interface Patterns
**Behavioral Vector**: `detail_focus=0.95, creativity=0.85, accessibility=0.9, brand_alignment=0.9`

**Traditional Visual Criteria:**
- **P0 Critical**: Contrast <3:1 (accessibility fail), broken layout, brand mismatch, unreadable text
- **P1 High**: Inconsistent spacing, unclear typography hierarchy, contrast 3:1-4.5:1, responsive breakpoint issues
- **P2 Medium**: Minor spacing inconsistencies, icon mismatches, animation timing, hover state gaps
- **P3 Low**: Micro-animation polish, shadow consistency, gradient optimization

**AI-Specific Visual Criteria:**
- **P1 High**:
  - AI vs human messages not visually distinguished in chat interfaces
  - Code blocks in AI responses lack syntax highlighting
  - No visual hierarchy for AI-generated structured content
- **P2 Medium**:
  - Citation/source links in AI responses not visually distinct
  - Streaming text causing layout shift (CLS issues)
  - AI confidence indicators poorly designed
  - Loading skeletons don't match AI response structure
- **P3 Low**:
  - AI avatar/icon inconsistent with brand
  - Markdown rendering in AI responses lacks polish

---

### Judge 5: Data Guardian ("The Integrity Keeper")
**Domain**: Data Integrity, Persistence, Consistency, AI Data Trails
**Behavioral Vector**: `accuracy=0.95, consistency=0.95, integrity=0.98, validation_rigor=0.9`

**Traditional Data Criteria:**
- **P0 Critical**: Data loss on normal ops, inconsistent states, missing transaction safety, corrupted patterns
- **P1 High**: Missing input validation, race conditions, incomplete migrations, no backup strategy
- **P2 Medium**: Inconsistent date formats, missing constraints, incomplete audit trails, soft delete gaps
- **P3 Low**: Documentation gaps, schema optimization, archive strategy

**AI-Specific Data Criteria:**
- **P0 Critical**:
  - AI conversation history lost on refresh/navigation
  - AI responses overwriting user data without confirmation
  - No data validation on AI-generated content before persistence
- **P1 High**:
  - AI conversation history not persisted correctly across sessions
  - Missing immutable audit trail for AI-human interactions
  - No versioning of AI responses for debugging/compliance
  - Context window exceeded without warning or graceful handling
- **P2 Medium**:
  - AI conversation IDs not unique/collision-proof
  - Missing soft delete for conversation threads
  - No backup strategy for AI interaction logs
  - AI-generated content not flagged in database schema
- **P3 Low**:
  - No archival strategy for old AI conversations
  - Missing data lineage for AI-processed content

---

### Judge 6: Business Strategist ("The Value Maximizer")
**Domain**: Business Logic, Feature Completeness, Value Delivery, AI ROI
**Behavioral Vector**: `business_alignment=0.85, strictness=0.85, user_advocacy=0.85, roi_focus=0.9`

**Traditional Business Criteria:**
- **P0 Critical**: Core business function broken, revenue-impacting bugs, legal/compliance violations, missing MVP features
- **P1 High**: Incomplete workflows, missing edge case handling, business rule inconsistencies
- **P2 Medium**: Feature prioritization issues, minor workflow gaps, analytics gaps
- **P3 Low**: Feature polish, competitive differentiation, business rule documentation

**AI-Specific Business Criteria:**
- **P0 Critical**:
  - AI features that could create legal liability (e.g., medical/financial advice without disclaimers)
  - No cost controls on AI inference (unbounded spending possible)
- **P1 High**:
  - No token/inference cost monitoring or budgeting
  - AI features without clear business value justification
  - Missing AI usage analytics for ROI calculation
  - No fallback when AI service unavailable (complete feature failure)
- **P2 Medium**:
  - No AI cost attribution per feature/user
  - Missing business metrics for AI effectiveness (task completion, user satisfaction)
  - No A/B testing framework for AI features
  - AI capabilities exceed what's needed (over-engineering with expensive models)
- **P3 Low**:
  - No competitive analysis of AI feature differentiation
  - Missing documentation of AI business value

---

### Judge 7: Accessibility Guardian ("The Inclusivity Champion")
**Domain**: WCAG Compliance, Screen Reader Support, Cognitive Accessibility, AI Content Accessibility
**Behavioral Vector**: `strictness=0.98, empathy=0.95, inclusivity=0.98, standards_adherence=0.95`

**Traditional Accessibility Criteria:**
- **P0 Critical**: Completely inaccessible to screen readers, no keyboard navigation, critical content invisible to assistive tech, seizure-inducing animations
- **P1 High**: Missing alt text on meaningful images, inputs without labels, focus not visible, missing skip links, ARIA misuse
- **P2 Medium**: Inconsistent focus order, missing landmark regions, color-only info, missing captions
- **P3 Low**: ARIA optimization, enhanced screen reader announcements, cognitive load improvements

**AI-Specific Accessibility Criteria:**
- **P0 Critical**:
  - AI-generated content completely inaccessible to screen readers
  - AI interface keyboard-inaccessible (can't send messages, navigate responses)
- **P1 High**:
  - AI-generated content not announced to screen readers (missing live regions)
  - Streaming responses not accessible via ARIA live regions
  - AI code blocks missing accessible code formatting
  - No pause/stop for AI-generated content (cognitive accessibility)
- **P2 Medium**:
  - AI conversation navigation not keyboard-accessible
  - Missing ARIA labels for AI interaction controls (regenerate, copy, rate)
  - AI-generated images missing alt text
  - Complex AI outputs (tables, charts) not accessible
- **P3 Low**:
  - AI reading level not adjustable
  - No simplified/plain language AI output option

---

### Judge 8: Infrastructure Architect ("The Reliability Engineer")
**Domain**: Scalability, Monitoring, DevOps, LLM Provider Health & NOC Integration
**Behavioral Vector**: `reliability=0.95, scalability=0.9, observability=0.9, automation=0.85`

**Traditional Infrastructure Criteria:**
- **P0 Critical**: No health check endpoint, single point of failure, unhandled errors causing crashes, no backup capability
- **P1 High**: Missing monitoring/alerting, no logging, manual deployment steps, no environment separation
- **P2 Medium**: Suboptimal caching, missing docs, CI/CD optimization, secret management
- **P3 Low**: IaC polish, cost optimization, enhanced observability

**AI-Specific Infrastructure Criteria:**
- **P0 Critical**:
  - Health endpoint doesn't validate LLM provider connection
  - No circuit breaker for LLM provider failures (cascading failures possible)
  - Single LLM provider with no fallback strategy
  - LLM API keys hardcoded or in version control
- **P1 High**:
  - No LLM-specific metrics in observability stack (OpenTelemetry/Prometheus)
  - Missing token usage/cost alerts (runaway spending possible)
  - No incident escalation for AI-specific failures (hallucination rate spikes, provider downtime)
  - Security logs not integrated with SIEM (Splunk, Sentinel)
  - No structured telemetry for LLM latency, token throughput, error rates
- **P2 Medium**:
  - LLM metrics not in NOC dashboard (Grafana, Datadog)
  - Missing LLM provider latency SLOs/SLAs
  - No automated LLM provider health checks
  - Circuit breaker thresholds not tuned for LLM latency patterns
  - No capacity planning for AI inference load
- **P3 Low**:
  - Missing runbook for LLM provider outages
  - No cost forecasting for AI usage growth

---

### Judge 9: Developer Experience ("The Code Craftsman")
**Domain**: Code Quality, Documentation, Maintainability, Prompt Management
**Behavioral Vector**: `clarity=0.95, consistency=0.9, maintainability=0.95, documentation_focus=0.85`

**Traditional DX Criteria:**
- **P0 Critical**: Undocumented critical systems, impossible to run locally, missing dependencies, no version control
- **P1 High**: Missing README, no test coverage on critical paths, inconsistent code style, complex setup
- **P2 Medium**: Limited inline docs, type safety gaps, test coverage <60%, dependency management
- **P3 Low**: Code style optimization, documentation enhancement, developer tooling

**AI-Specific DX Criteria:**
- **P0 Critical**:
  - AI-generated code committed without review (mock filler, TODO tags, stale patterns)
  - Prompts contain secrets or PII
  - No way to reproduce AI behavior (non-deterministic without seed/logging)
- **P1 High**:
  - Prompts hardcoded in application logic (not in centralized registry)
  - No semantic versioning for prompts (silent behavior changes possible)
  - Missing tests for AI components/tools
  - No process for reviewing AI-generated code contributions
  - Prompt changes deployed without peer review
- **P2 Medium**:
  - Prompt variables not validated with Pydantic/JSON Schema
  - No change management workflow for prompt updates
  - Missing documentation of model-specific tuning (temperature, top_p)
  - No local development setup for AI features (requires production API)
  - AI component tests missing from CI/CD pipeline
- **P3 Low**:
  - No prompt playground/testing environment
  - Missing documentation of prompt engineering decisions

---

### Judge 10: Sustainability Specialist ("The Green Guardian")
**Domain**: Carbon-Aware Computing, Energy Efficiency, Environmental Impact, AI Inference Efficiency
**Behavioral Vector**: `carbon_reflexivity=0.95, computational_parsimony=0.9, infrastructure_stewardship=0.95, data_minimalism=0.85`

**Traditional Sustainability Criteria:**
- **P0 Critical**: High-carbon region deployment (when low-carbon alternative exists), zombie infrastructure, unoptimized assets >5MB, infinite loops/runaway processes
- **P1 High**: Unoptimized images >1MB, missing dark mode (OLED energy waste), excessive API polling, no asset compression
- **P2 Medium**: Inefficient algorithms (O(n^2) when O(n) possible), excessive tracking scripts, missing lazy loading, redundant fetching
- **P3 Low**: Missing environmental disclosures, SCI scoring docs, green hosting badges, carbon offset info

**AI-Specific Sustainability Criteria:**
- **P0 Critical**:
  - AI inference running on high-carbon grid when low-carbon alternative available
  - Runaway AI loops consuming unlimited compute
  - No timeout on AI inference calls (infinite resource consumption possible)
- **P1 High**:
  - Using large model (GPT-4, Claude Opus) when smaller model sufficient for task
  - No batching of AI requests when applicable
  - Real-time inference for non-time-sensitive tasks (could use batch processing)
  - Embedding generation repeated for unchanged content
- **P2 Medium**:
  - No model selection based on task complexity (always using most expensive model)
  - Missing carbon footprint disclosure for AI features
  - Full document re-embedding when only portions changed
  - No caching of AI inference results
- **P3 Low**:
  - No SCI (Software Carbon Intensity) scoring for AI features
  - Missing documentation of AI energy consumption
  - No user-facing carbon impact visibility

**SCI Formula Reference**: `SCI = ((E x I) + M) per R`
- E = Energy consumed by AI inference
- I = Carbon intensity of the grid
- M = Embodied carbon of hardware
- R = Functional unit (per request, per user, per feature)

---

### Judge 11: AI Governance Specialist ("The Cognitive Guardian") - NEW
**Domain**: LLM Safety, Prompt Engineering, Hallucination Management, AI Compliance
**Behavioral Vector**: `trustworthiness_focus=0.95, safety_rigor=0.95, transparency_advocacy=0.90, hallucination_paranoia=0.95, compliance_focus=0.90`

**Cognitive Architecture & Guardrails:**
- **P0 Critical**:
  - No prompt injection protection on user-facing AI (LLM01)
  - AI outputs sensitive corporate data without sanitization
  - No grounded truth (RAG/GraphRAG) for factual claims - pure hallucination risk
  - AI making consequential decisions without Chain-of-Thought (CoT) logging
  - AI can execute code or take actions without human approval (excessive agency)
- **P1 High**:
  - Missing hallucination monitoring/detection system
  - No prompt versioning system (behavior changes silently)
  - AI output not validated against expected schema
  - Missing AI safety guardrails (content filters, topic restrictions)
  - No human-in-the-loop for high-stakes AI decisions
  - CoT reasoning not externalized for debugging
  - AI identity not federated with corporate SSO/IAM
- **P2 Medium**:
  - Prompts not in centralized registry (Git-backed YAML, LangSmith, database)
  - No model-specific optimization tracking (which model/params prompt tuned for)
  - Missing AI interaction audit trail for compliance/forensics
  - No clear AI capability documentation for users
  - Prompt change management lacks peer review process
- **P3 Low**:
  - Hallucination registry not maintained (known model limitations)
  - AI usage guidelines not published to intranet
  - Missing model card/documentation
  - No AI ethics review process documented

**Compliance & Audit Requirements:**
- **P0 Critical**:
  - AI making regulated decisions (financial, medical, legal) without required disclosures
  - No immutable audit trail for AI decisions
- **P1 High**:
  - AI interactions not logged for forensic review
  - Missing DLP scanning on AI outputs
  - No SIEM integration for AI security events
- **P2 Medium**:
  - AI compliance documentation incomplete
  - No regular AI bias/fairness audits scheduled
- **P3 Low**:
  - Missing AI governance committee/process
  - No documented AI incident response plan

---

### Phase 3: P0-P3 Severity Weighting

Classify every finding by severity:
- **P0 - Critical** (blocks deployment): Security breaches, data loss, auth bypasses, prompt injection vulnerabilities, AI making uncontrolled decisions, high-carbon deployments with alternatives
- **P1 - High** (must fix before production): Major UX issues, performance blockers, a11y failures, missing LLM monitoring, no prompt versioning, unoptimized AI models
- **P2 - Medium** (fix in next sprint): Minor bugs, design inconsistencies, code quality, AI cost attribution gaps, inefficient algorithms
- **P3 - Low** (nice to have): Polish items, optimizations, documentation improvements, environmental disclosures

### Phase 4: Cross-Judge Conflict Detection

Flag when judges have:
- Scoring divergence >3 points on same component
- Contradictory findings (e.g., Performance says "use smaller model" vs Business says "need best quality")
- Domain overlap requiring resolution

**Common AI-Specific Conflicts:**
| Conflict | Resolution |
|----------|-----------|
| Performance: "Use smaller/faster model" vs Business: "Need highest quality" | Tiered model selection based on query complexity |
| Security: "Log all AI interactions" vs Privacy: "Minimize data retention" | Anonymized logging with configurable retention |
| Sustainability: "Batch requests" vs UX: "Real-time responses" | Batch background tasks, stream user-facing responses |
| DX: "Centralize prompts" vs Performance: "Inline for speed" | Centralized registry with build-time inlining |

### Phase 5: Output Generation

Generate **11 Corrective Prompts** in the output file - one per judge - formatted as:
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

| Profile | Security | Performance | UX | Visual | Data | Business | A11y | Infra | DX | Sustainability | AI Governance | Description |
|---------|----------|-------------|-----|--------|------|----------|------|-------|-----|----------------|---------------|-------------|
| `dev` | 0.4 | 0.4 | 0.6 | 0.4 | 0.5 | 0.3 | 0.3 | 0.2 | 0.4 | 0.2 | 0.3 | Local development |
| `hackathon` | 0.5 | 0.5 | 0.8 | 0.5 | 0.4 | 0.6 | 0.3 | 0.2 | 0.3 | 0.2 | 0.4 | Speed over polish |
| `mvp` | 0.7 | 0.7 | 0.9 | 0.7 | 0.7 | 0.8 | 0.6 | 0.5 | 0.5 | 0.5 | 0.6 | Minimum viable product |
| `staging` | 0.9 | 0.8 | 0.9 | 0.8 | 0.8 | 0.8 | 0.8 | 0.7 | 0.7 | 0.7 | 0.8 | Pre-production testing |
| `production` | 0.95 | 0.9 | 0.95 | 0.85 | 0.9 | 0.9 | 0.95 | 0.9 | 0.8 | 0.85 | 0.9 | Live deployment |
| `enterprise` | 0.98 | 0.95 | 0.95 | 0.9 | 0.95 | 0.95 | 0.98 | 0.95 | 0.9 | 0.95 | 0.98 | Enterprise compliance |

**Note**: `development` is an alias for `dev`

---

## AI Application Detection

**Auto-detect AI features** by scanning for:
- LLM provider SDK imports (openai, anthropic, google.generativeai, langchain, llamaindex)
- API endpoints with `/chat`, `/completion`, `/inference`, `/ai/` patterns
- Environment variables: `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `GEMINI_API_KEY`
- Prompt template files (`.prompt`, `.jinja2` with LLM context)
- RAG/vector database imports (chromadb, pinecone, weaviate, qdrant)

**If AI features detected**: Activate full AI-specific criteria for all judges
**If no AI features**: Skip AI-specific criteria, focus on traditional evaluation

---

## Example Invocations

```bash
# Evaluate local dev server (lenient)
/vibe-review http://localhost:5190 dev

# Evaluate codebase directory for MVP readiness
/vibe-review /path/to/my-project mvp

# Evaluate production deployment (strictest)
/vibe-review https://myapp.com production

# Evaluate enterprise AI application (maximum AI governance)
/vibe-review /path/to/ai-chatbot enterprise
```

---

## Playwright Troubleshooting & Best Practices

### Common Issue 1: Rate Limiting / DNS Attack Detection

**Symptom**: Security monitoring blocks browser access after opening multiple windows quickly. May see "DNS attack detected" or temporary access blocks.

**Prevention Protocol**:
```
IMPORTANT: When using Playwright for evidence collection, follow these rate-limiting guidelines:

1. **Sequential Tab Usage**: Open ONE tab at a time, complete evidence collection, then close before opening next
2. **Delay Between Actions**: Wait 2-3 seconds between major navigation actions
3. **Batch Wisely**: Group related evidence (e.g., all screenshots of one page) before navigating away
4. **Close Tabs Explicitly**: Use browser_close or browser_tabs(action="close") after each evidence batch
```

**If Blocked**:
1. Stop all Playwright operations immediately
2. Wait 60-90 seconds for security cooldown
3. Resume with slower pacing (5 second delays between navigations)
4. Consider splitting evaluation across multiple sessions if site is sensitive

**Implementation Pattern**:
```markdown
# Evidence collection with rate limiting
1. Navigate to homepage → Take screenshot → Capture accessibility snapshot → Wait 3s
2. Navigate to login page → Take screenshot → Capture form structure → Wait 3s
3. Navigate to main feature → Take screenshot → Capture network requests → Wait 3s
# Close browser between major sections if monitoring is aggressive
```

### Common Issue 2: Authentication-Required Pages

**Symptom**: Cannot evaluate pages behind login without credentials.

**Authentication Strategies**:

**Strategy A: Pre-Authenticated Session (Recommended)**
```markdown
1. Ask user for test credentials or request they log in manually first
2. Use browser_snapshot to verify logged-in state
3. Proceed with evaluation while session is active
```

**Strategy B: Automated Login Flow**
```markdown
1. Navigate to login page
2. Use browser_fill_form to enter credentials:
   - fields: [
       {name: "Email field", type: "textbox", ref: "[email-input-ref]", value: "test@example.com"},
       {name: "Password field", type: "textbox", ref: "[password-input-ref]", value: "***"}
     ]
3. Click submit button
4. Wait for redirect/dashboard load
5. Verify authentication succeeded before proceeding
```

**Strategy C: Evaluate Public + Document Private**
```markdown
1. Evaluate all publicly accessible pages with full Playwright automation
2. For authenticated pages, document what WOULD be evaluated
3. Request user provide screenshots of authenticated areas
4. Include "Authentication Required" section in report with manual evaluation notes
```

**Credential Handling Rules**:
- **NEVER** store credentials in vibe-review output files
- **NEVER** log credentials to console
- **ASK** user before attempting automated login
- **PREFER** test/demo accounts over production credentials
- **OFFER** to evaluate logged-out experience only if credentials are sensitive

### Common Issue 3: Browser Not Installed

**Symptom**: "Browser executable not found" or similar errors.

**Fix**: Run `mcp__playwright__browser_install` before starting evaluation.

### Fallback: Manual Evidence Mode

If Playwright issues persist, switch to **Manual Evidence Mode**:

```markdown
## Manual Evidence Mode

Playwright automation unavailable. Requesting manual evidence collection:

**User Actions Required**:
1. Open [TARGET URL] in your browser
2. Take screenshots of:
   - [ ] Homepage (desktop view)
   - [ ] Homepage (mobile view - use DevTools responsive mode)
   - [ ] Main navigation expanded
   - [ ] Key feature pages (list specific pages)
   - [ ] Any error states encountered
3. Open DevTools and capture:
   - [ ] Console errors (Console tab)
   - [ ] Network waterfall for initial page load (Network tab)
   - [ ] Lighthouse report (generate and export)
4. Paste screenshots into this conversation or save to project directory

**Evaluation will proceed with manual evidence once provided.**
```

---

## References

This evaluation framework incorporates criteria from:
- **OWASP Top 10** (2021) - Web Application Security
- **OWASP LLM Top 10** (2025) - LLM-Specific Security Risks
- **WCAG 2.1 AA** - Web Content Accessibility Guidelines
- **Green Software Foundation** - Sustainable Software Principles
- **AI Production Deployment Guidelines** (Raj/Michael Wood, 2025) - Enterprise AI Readiness

---

**Begin evaluation now.**

1. Determine project name from TARGET
2. Detect if AI features present (adjust criteria accordingly)
3. Create output file: `YYYYMMDD-[project-name]-vibe-review.md`
4. Use Playwright for browser evidence collection (URLs) or code analysis (directories)
5. Generate 11 corrective prompts prioritized by P0-P3 severity
6. Save all results to the output file in the project's root directory
