# Template Design System

> **Definitive authority on template creation and maintenance.** Every template in this repository follows the standards defined here. If there is a conflict between this document and any other, this document governs.

---

## Design Principles

All standards derive from four principles. When in doubt, return to these.

### 1. Security at the Foundation

Security patterns are never optional. Framework templates embed them in the first section. Language templates require `common/security.gitignore` — never skip it. The most damaging Git mistakes involve committed credentials; templates must prevent this by default.

### 2. Self-Contained or Modular, Never Both

A template is either self-contained (framework — everything in one file) or modular (language — designed to combine). Templates that try to be both create confusion and duplicates. The boundary is bright and enforced.

### 3. Structure Enables Trust

Users should open any template and immediately understand its layout. The header, metadata, sections, and footer follow a consistent visual language. Uniformity makes templates scannable and predictable.

### 4. Minimize, Then Justify

Every pattern costs: maintenance, cognitive load, risk of over-matching. Default to exclusion. A pattern earns its place only when committed instances would cause real problems — broken builds, leaked credentials, bloated repositories.

---

## Template Anatomy

Every template has five structural zones.

```
┌─────────────────────────────────────┐
│ ZONE 1: HEADER                      │
│ Attribution, type, website, repo     │
├─────────────────────────────────────┤
│ ZONE 2: METADATA                    │
│ 7-field overview: type, purpose,     │
│ philosophy, combination, security,   │
│ practices, sources                   │
├─────────────────────────────────────┤
│ ZONE 3: SECTIONS                    │
│ Pattern groups with # ••••• dividers │
│ Patterns sorted alphabetically       │
├─────────────────────────────────────┤
│ ZONE 4: FOOTER                      │
│ Customization notes                  │
├─────────────────────────────────────┤
│ ZONE 5: COMBINATION RECIPES          │
│ cat commands for common setups       │
└─────────────────────────────────────┘
```

---

### Zone 1: Header (required)

```gitignore
# ==============================================================================
# Created by https://gitignores.com/
# [TEMPLATE TYPE] for [Technology Name]
# Website: [Official website URL]
# Repository: [Official repository URL]
# ==============================================================================
```

**Template type labels — use exactly as shown:**

| Label                              | Directory     |
| ---------------------------------- | ------------- |
| `LANGUAGE-SPECIFIC TEMPLATE`       | `languages/`  |
| `COMPREHENSIVE FRAMEWORK TEMPLATE` | `frameworks/` |
| `TOOL-SPECIFIC TEMPLATE`           | `tools/`      |
| `IDE/EDITOR TEMPLATE`              | `ides/`       |
| `OPERATING SYSTEM TEMPLATE`        | `os/`         |
| `PLATFORM-SPECIFIC TEMPLATE`       | `platforms/`  |
| `COMMON PATTERNS TEMPLATE`         | `common/`     |

**Example:**

```gitignore
# ==============================================================================
# Created by https://gitignores.com/
# COMPREHENSIVE FRAMEWORK TEMPLATE for Django
# Website: https://www.djangoproject.com/
# Repository: https://github.com/django/django
# ==============================================================================
```

---

### Zone 2: Metadata (required)

```gitignore
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# TEMPLATE OVERVIEW & USAGE NOTES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# • TEMPLATE TYPE: [exact type from table]
# • PURPOSE: [one-sentence description]
# • DESIGN PHILOSOPHY: [Self-contained | Modular]
# • COMBINATION GUIDANCE: [how to combine]
# • SECURITY CONSIDERATIONS: [notes]
# • BEST PRACTICES: [1-2 recommendations]
# • OFFICIAL SOURCES: [attribution]
```

**Design philosophy values:**

| Value                                              | Meaning                                                      |
| -------------------------------------------------- | ------------------------------------------------------------ |
| `Self-contained with all [Tech]-specific patterns` | Everything included; don't combine with language templates   |
| `Modular — combine with common templates`          | Language-only patterns; must add `common/security.gitignore` |

**Security considerations by template type:**

| Template type     | Required text                                                   |
| ----------------- | --------------------------------------------------------------- |
| Framework         | `Includes security patterns for .env files and credentials`     |
| Language          | `No security patterns included — add common/security.gitignore` |
| Common (security) | `Comprehensive security patterns for protecting sensitive data` |

---

### Zone 3: Sections

**Section divider format:**

```gitignore
# ••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••
# SECTION TITLE
# ••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••
# Optional: one-line description
```

**Section ordering:**

_Framework templates:_

1. Security & Sensitive Data Protection _(always first)_
2. Build Artifacts & Distribution
3. Dependency Management & Package Cache
4. Development & Runtime Artifacts
5. Framework-Specific Patterns
6. Testing & Quality Assurance

_Language templates:_

1. Build Artifacts & Distribution
2. Dependency Management & Package Cache
3. Development & Runtime Artifacts
4. Language-Specific Patterns
5. Testing & Quality Assurance

_Other template types:_ Use relevant sections from above, ordered generic→specific.

**Pattern formatting:**

- Sort alphabetically within each section (case-insensitive)
- One pattern per line; no inline comments on pattern lines
- Descriptive comments for non-obvious patterns
- No trailing whitespace
- No duplicate patterns anywhere in the file

---

### Zone 4: Footer (required)

```gitignore
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# TEMPLATE CUSTOMIZATION & BEST PRACTICES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# 1. REVIEW: Examine all patterns before use
# 2. CUSTOMIZE: Adapt to your project's specific structure
# 3. TEST: Use `git check-ignore` to verify patterns
# 4. SECURE: Always protect sensitive data and credentials
# 5. UPDATE: Review periodically as technology evolves
```

---

### Zone 5: Combination Recipes (strongly recommended)

Include at minimum one combination example. Framework templates should show combinations with IDEs and OS templates. Language templates should show `common/security` and a fuller toolchain example.

```gitignore
# EXAMPLE COMBINATION:
# cat frameworks/react.gitignore \
#     ides/visual-studio-code.gitignore \
#     os/macos.gitignore | sort -u > .gitignore
```

---

## Naming Conventions

### General rules

| Rule                     | Example                                                                    |
| ------------------------ | -------------------------------------------------------------------------- |
| All lowercase            | `react.gitignore`, not `React.gitignore`                                   |
| Hyphens for spaces       | `spring-boot.gitignore`, `visual-studio-code.gitignore`                    |
| Strip special characters | `csharp.gitignore` (C#), `nextjs.gitignore` (Next.js)                      |
| Based on official name   | `adonisjs.gitignore` (AdonisJS), `ruby-on-rails.gitignore` (Ruby on Rails) |

### JavaScript naming rule

For JavaScript technologies, derive the filename from the GitHub repository name:

- Strip the organization prefix: `facebook/react` → `react`
- Remove dots: `vercel/next.js` → `nextjs`
- Exception: if the repo name is unrelated to the official name (e.g., `adonisjs/core` where "core" ≠ "adonisjs"), use the official name (`adonisjs`)

| Technology | GitHub Repo         | File                   |
| ---------- | ------------------- | ---------------------- |
| React      | `facebook/react`    | `react.gitignore`      |
| Next.js    | `vercel/next.js`    | `nextjs.gitignore`     |
| Vue.js     | `vuejs/vue`         | `vue.gitignore`        |
| Angular    | `angular/angular`   | `angular.gitignore`    |
| Express.js | `expressjs/express` | `express.gitignore`    |
| Node.js    | `nodejs/node`       | `node.gitignore`       |
| AdonisJS   | `adonisjs/core`     | `adonisjs.gitignore`   |
| TypeScript | —                   | `typescript.gitignore` |

### Additional examples

| Technology         | File                           | Rule                     |
| ------------------ | ------------------------------ | ------------------------ |
| Visual Studio Code | `visual-studio-code.gitignore` | Hyphens for spaces       |
| C#                 | `csharp.gitignore`             | Official name conversion |
| .NET               | `dotnet.gitignore`             | Strip dots               |
| Spring Boot        | `spring-boot.gitignore`        | Hyphens for spaces       |
| Ruby on Rails      | `ruby-on-rails.gitignore`      | Hyphens for spaces       |

---

## Security Patterns

### Framework templates

MUST include a security section as the **first** section. Minimum patterns:

```gitignore
.env
.env.*
.env.*.local
.env.local
```

Add ecosystem-relevant patterns: certificates, cloud credentials, database files. See `common/security.gitignore` for the canonical reference.

`common/security.gitignore` organizes patterns into:

1. Environment Variables & Configuration
2. Credentials & Secrets Management
3. Certificates & Cryptographic Keys
4. SSH Keys & Authentication
5. Cloud Provider Configuration
6. Database & Data Storage Files

### Language templates

MUST NOT include security patterns. Metadata must state: `Must combine with common/security.gitignore`.

---

## Quality Gates

Before finalizing any template:

| Gate                  | Verification                                                 |
| --------------------- | ------------------------------------------------------------ |
| **Syntax**            | `git check-ignore -v <test-file>` — no errors                |
| **Dedup**             | `sort template.gitignore \| uniq -d` — empty output          |
| **Alpha sort**        | Visual check: each section's patterns in A-Z order           |
| **Section order**     | Security first (frameworks), then prescribed order           |
| **Zone completeness** | All 4 required zones present; zone 5 recommended             |
| **Metadata accuracy** | Type, philosophy, and security fields match template content |
| **Live test**         | `git status --ignored` in a test repo — works as expected    |
| **Cross-check**       | Compare against sibling templates for consistency            |

---

## Verification

### Smoke test

```bash
mkdir -p /tmp/gt-$$ && cd /tmp/gt-$$ && git init
cp /path/to/template.gitignore .gitignore
touch .env .env.local credentials.json secret.key
git status --ignored
# Expected: all four files listed under "Ignored files"
```

### Spot check

```bash
git check-ignore -v node_modules/test.js  # Should show matching pattern
git check-ignore -v src/main.js           # Should produce no output
```

### Combined templates

```bash
cat a.gitignore b.gitignore c.gitignore | sort -u > .gitignore
git check-ignore -v .env  # Should match from common/security
```

---

## Common Mistakes

| Mistake                                | Cause                               | Fix                                                                                     |
| -------------------------------------- | ----------------------------------- | --------------------------------------------------------------------------------------- |
| Security section in language template  | Copied from framework template      | Remove all security patterns                                                            |
| Missing security in framework template | Started from language template      | Add security as first section                                                           |
| Unsorted patterns                      | Added without sorting               | Sort each section alphabetically                                                        |
| Metadata mismatch                      | Copy-paste error                    | Match metadata to template content                                                      |
| `!unignore` without context            | Negation without path anchors       | Spell out paths to unignore explicitly                                                  |
| `*.log` too broad                      | Catches `changelog.md`              | Use directory-specific: `logs/*.log`                                                    |
| Wrong directory                        | Followed wrong category             | Review decision tree in [AGENTS.md §Creating or Editing](AGENTS.md#creating-or-editing) |
| Kitchen-sink templates                 | Adding every pattern "just in case" | Add only patterns with clear justification                                              |
| Copy-paste from another project        | Ignores unique technology needs     | Research the technology's own artifacts                                                 |
| Ignoring official sources              | Misses recommended patterns         | Check official repos first                                                              |
| Skipping verification                  | Broken patterns get merged          | Run full verification procedure every time                                              |

---

**Maintained by:** [gitignores.com](https://gitignores.com)  
**Repository:** [github.com/ronald2wing/.gitignores](https://github.com/ronald2wing/.gitignores)
