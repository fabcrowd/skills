# User-Level Claude Instructions

## Rule Hierarchy

1. `common/development-workflow` — **PRIMARY**: plan → TDD → review → commit
2. `common/testing`, `common/security`, `common/agents`, `common/coding-style` — extend primary
3. `typescript/*`, `python/*`, `web/*` — language-scoped, apply to matching file types
4. Karpathy mindset (below) — **supplementary**: governs *how to think*, not *what to do*; defer to ECC rules on any conflict
5. Skill invocation triggers (below) — apply alongside all of the above

---

## Karpathy Mindset (Supplementary)

**Think Before Coding** — Don't assume. Surface tradeoffs. If multiple interpretations exist, present them — don't pick silently. If something is unclear, stop and ask.

**Simplicity First** — Minimum code that solves the problem. No features beyond what was asked, no abstractions for single-use code, no error handling for impossible scenarios.

**Surgical Changes** — Touch only what you must. Don't "improve" adjacent code. Don't refactor things that aren't broken. Match existing style. Every changed line should trace directly to the user's request.

---

## Skill Library

Skills are the **primary workflow surface**. They live in `~/.claude/skills/ecc/` and `~/.claude/.agents/skills/`. Invoke them proactively — don't wait for the user to ask. Each skill's `SKILL.md` contains detailed patterns; load it when the trigger condition matches.

**Rule:** Before writing custom code for any established pattern, check if a skill covers it.

---

## When to Invoke Each Skill

### Research & Discovery
| Trigger | Skill |
|---------|-------|
| User says "research", "deep dive", "investigate", "what's the state of" | `deep-research` |
| Starting a new feature — check for existing libs/tools first | `search-first` |
| Market sizing, competitor analysis, technology evaluation, investor due diligence | `market-research` |
| API or library docs question before implementing | `documentation-lookup` |

### Web3 / DeFi / Crypto (Primary Domain)
| Trigger | Skill |
|---------|-------|
| Any Solidity AMM, liquidity pool, or swap contract | `defi-amm-security` |
| Reading token balances, formatting amounts, any `decimals()` call | `evm-token-decimals` |
| Building an autonomous trading agent or bot with wallet authority | `llm-trading-agent-security` |
| Hashing with `keccak256` in Node.js/TypeScript | `nodejs-keccak256` |

### Backend Development
| Trigger | Skill |
|---------|-------|
| Designing REST or GraphQL API endpoints | `api-design` |
| Repository, service, or controller layer architecture | `backend-patterns` |
| Database schema changes, zero-downtime migrations | `database-migrations` |
| PostgreSQL query optimization, indexing, connection pooling | `postgres-patterns` |
| Docker, CI/CD, health checks, rollback strategy | `deployment-patterns` |
| Docker Compose networking, volumes, container security | `docker-patterns` |

### Security
| Trigger | Skill |
|---------|-------|
| Auth, user input, secrets, payments, API endpoints | `security-review` |
| Scan Claude Code config for vulnerabilities | `security-scan` |
| Any code touching wallets, private keys, transaction signing | `llm-trading-agent-security` |

### Code Quality & Testing
| Trigger | Skill |
|---------|-------|
| Any new feature or bug fix | `tdd-workflow` |
| Build, lint, typecheck, test all at once | `verification-loop` |
| Playwright E2E tests for critical flows | `e2e-testing` |
| AI model evaluation or regression testing | `eval-harness` |

### TypeScript / Node.js
| Trigger | Skill |
|---------|-------|
| TypeScript project patterns, strict typing, module structure | `coding-standards` |
| MCP server authoring | `mcp-server-patterns` |
| Next.js 16+ or Turbopack | `nextjs-turbopack` |
| Bun as runtime, bundler, or test runner | `bun-runtime` |

### Context & Token Management
| Trigger | Skill |
|---------|-------|
| After research phase, before implementation | `strategic-compact` — suggest `/compact` |
| Long session with multiple completed milestones | `strategic-compact` |
| Iterative subagent context refinement | `iterative-retrieval` |

---

## Proactive Skill Use — Decision Tree

```
User starts a task
  │
  ├─ Involves research? → deep-research or search-first FIRST
  │
  ├─ Involves crypto/DeFi/EVM?
  │   ├─ Solidity contract? → defi-amm-security
  │   ├─ Token amounts/decimals? → evm-token-decimals
  │   ├─ Trading bot/agent? → llm-trading-agent-security
  │   └─ Keccak hashing in JS/TS? → nodejs-keccak256
  │
  ├─ Involves backend/API?
  │   ├─ New endpoint design → api-design
  │   ├─ DB schema change → database-migrations
  │   └─ Architecture → backend-patterns
  │
  ├─ Writing new code? → tdd-workflow (tests first)
  │
  ├─ Security-sensitive code? → security-review
  │
  └─ Long session / phase boundary? → strategic-compact
```

---

## User Context

- **Primary domain:** Web3, DeFi, crypto backends (EVM, Solidity, ethers.js/viem, Node.js/TypeScript)
- **Research style:** Researches the internet before building — always use `search-first` and `deep-research` skills
- **Quality priority:** Never sacrifice code quality or test coverage for token savings
- **Token optimization:** Use `strategic-compact` at phase boundaries; default model is `sonnet`, switch to `opus` for deep architectural reasoning
- **Stack:** TypeScript-first backend; Python for scripts/data

---

## Full Skill Catalog

All 182 skills are in `~/.claude/skills/ecc/`. Key directories:

```
Research:        deep-research, market-research, search-first, exa-search
Web3/DeFi:       defi-amm-security, evm-token-decimals, llm-trading-agent-security, nodejs-keccak256
Backend:         backend-patterns, api-design, database-migrations, postgres-patterns
Deploy:          deployment-patterns, docker-patterns
Security:        security-review, security-scan
Testing:         tdd-workflow, verification-loop, e2e-testing, eval-harness
TypeScript:      coding-standards, mcp-server-patterns, nextjs-turbopack, bun-runtime
Context:         strategic-compact, iterative-retrieval
Content/Biz:     article-writing, market-research, investor-materials, investor-outreach
```

To read any skill's full pattern: `Read ~/.claude/skills/ecc/<skill-name>/SKILL.md`
