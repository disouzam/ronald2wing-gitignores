# The Contribution Lifecycle

> A 5-stage process for contributing new or updated `.gitignore` templates. Each stage has a goal, actions, and exit criteria.

---

## Principles

We operate on three principles:

1. **Be precise.** Templates that accidentally ignore important files cause real damage. Test your work.
2. **Be minimal.** Every pattern increases maintenance surface area. If a pattern isn't clearly justified, leave it out.
3. **Be consistent.** The collection's value is in its uniformity. When all templates follow the same structure, users can trust them without reading each one.

---

## Lifecycle Overview

```
STAGE 1          STAGE 2          STAGE 3          STAGE 4          STAGE 5
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  FIND    │───▶│  PLAN    │───▶│  WRITE   │───▶│  VERIFY  │───▶│  SHIP    │
│          │    │          │    │          │    │          │    │          │
│Find what │    │Design the│    │Build the │    │Prove it  │    │Submit    │
│to work on│    │template  │    │template  │    │works     │    │the PR    │
└──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
```

---

## Stage 1: Find

**Goal:** Identify the right thing to work on.

### Sources

| Source                                                               | Best for          |
| -------------------------------------------------------------------- | ----------------- |
| **Issue tracker** — issues labeled `help-wanted` or `new-template`   | New contributors  |
| **Missing technology** — popular tool/framework without a template   | Experienced users |
| **Template bugs** — wrong or missing pattern in an existing template | Experienced users |
| **Version updates** — new artifacts from a technology update         | Domain experts    |

### Checklist

- [ ] Search existing templates — does it already exist?
- [ ] Search open issues — is someone else working on it?
- [ ] Search closed issues/PRs — was it rejected before? Why?
- [ ] Check the official source — what does the project's own `.gitignore` look like?

If everything checks out, open an issue describing what you plan to do.

---

## Stage 2: Plan

**Goal:** Design before writing.

### Decision tree

```
New or modifying?
├── NEW TEMPLATE → Which category?
│   ├── Language?   → languages/   (modular, no security)
│   ├── Framework?  → frameworks/  (self-contained, security-first)
│   ├── Tool/CI?    → tools/
│   ├── IDE/Editor? → ides/
│   ├── OS?         → os/
│   └── Platform?   → platforms/
│
└── MODIFYING → What type?
    ├── Add patterns      → Determine correct section
    ├── Remove patterns   → Verify against official sources
    ├── Reorganize        → Follow TEMPLATE_STANDARDS.md section ordering
    └── Fix metadata      → Follow TEMPLATE_STANDARDS.md formatting
```

### Design rules

1. **Prefer official sources.** Check the technology's own `.gitignore` first. Community patterns come second.
2. **Eliminate, don't accumulate.** Each pattern must justify its existence.
3. **Respect the boundary.** Framework templates are self-contained. Language templates are modular. Never mix the two.
4. **Test assumptions.** A pattern that "should" work may not. Always test.

### Scope

| In scope                      | Out of scope                            |
| ----------------------------- | --------------------------------------- |
| Technology-specific artifacts | Generic catch-all patterns              |
| Build outputs that regenerate | Pattern explanations beyond one comment |
| Dependency directories        | Configuration instructions              |
| Cache and temp files          | Team workflow documentation             |
| IDE/editor artifacts          | Shell aliases or scripts                |
| Security-sensitive files      | Personal preferences                    |

---

## Stage 3: Write

**Goal:** Build the template following [TEMPLATE_STANDARDS.md](TEMPLATE_STANDARDS.md).

### Build checklist

- [ ] File named correctly (lowercase, hyphens, no dots) — see [TEMPLATE_STANDARDS.md §Naming](TEMPLATE_STANDARDS.md#naming-conventions)
- [ ] File in correct directory
- [ ] Header with `Created by https://gitignores.com/` — see [TEMPLATE_STANDARDS.md §Zone 1](TEMPLATE_STANDARDS.md#zone-1-header-required)
- [ ] Metadata block with all 7 fields — see [TEMPLATE_STANDARDS.md §Zone 2](TEMPLATE_STANDARDS.md#zone-2-metadata-required)
- [ ] Sections in prescribed order with `# •••••` dividers — see [TEMPLATE_STANDARDS.md §Zone 3](TEMPLATE_STANDARDS.md#zone-3-sections)
- [ ] Footer with `TEMPLATE CUSTOMIZATION & BEST PRACTICES` — see [TEMPLATE_STANDARDS.md §Zone 4](TEMPLATE_STANDARDS.md#zone-4-footer-required)
- [ ] Combination recipes — see [TEMPLATE_STANDARDS.md §Zone 5](TEMPLATE_STANDARDS.md#zone-5-combination-recipes-strongly-recommended)

### Template type constraints

| Type          | Directory     | Security Section            | Notes                                                   |
| ------------- | ------------- | --------------------------- | ------------------------------------------------------- |
| **Framework** | `frameworks/` | REQUIRED (first)            | Full template; combine with IDEs/OS only                |
| **Language**  | `languages/`  | FORBIDDEN                   | Must pair with `common/security.gitignore`              |
| **Tool**      | `tools/`      | None                        | Combine with language or framework                      |
| **IDE**       | `ides/`       | None                        | Combine with anything                                   |
| **OS**        | `os/`         | None                        | Combine with anything; include all 3 for cross-platform |
| **Platform**  | `platforms/`  | None                        | Platform-specific development                           |
| **Common**    | `common/`     | `security.gitignore` has it | Designed for combination                                |

---

## Stage 4: Verify

**Goal:** Prove the template works.

### Quick smoke test

Run the smoke test from [TEMPLATE_STANDARDS.md §Verification](TEMPLATE_STANDARDS.md#verification), adapting the `touch` files to your template's patterns:

```bash
mkdir -p /tmp/gt-$$ && cd /tmp/gt-$$ && git init
cp /path/to/template.gitignore .gitignore
touch .env .env.local credentials.json secret.key  # adapt to your template
git status --ignored
```

### Spot check

Pick 3–5 patterns from your template and verify each:

```bash
git check-ignore -v node_modules/test.js    # Should show matching pattern
git check-ignore -v src/main.js             # Should produce no output
```

### Dedup check

```bash
sort template.gitignore | uniq -d           # Must produce no output
```

### Verification checklist

Verify all items in [TEMPLATE_STANDARDS.md §Quality Gates](TEMPLATE_STANDARDS.md#quality-gates):

- [ ] Syntax: `git check-ignore -v` returns no errors
- [ ] Dedup: `sort | uniq -d` produces empty output
- [ ] Alpha sort: each section's patterns in A–Z order
- [ ] Section order: matches prescribed template type order
- [ ] Zone completeness: all 4 required zones present
- [ ] Metadata accuracy: type, philosophy, and security fields match content
- [ ] Live test: `git status --ignored` works as expected
- [ ] Cross-check: consistent with sibling templates

---

## Stage 5: Ship

**Goal:** Submit the contribution.

### PR workflow

```bash
git checkout -b add-rust-template        # Descriptive branch name
git add frameworks/rust.gitignore
git commit -m "add rust framework template

- Security patterns for .env, credentials, certificates
- Build artifacts: target/, *.rlib, *.so
- Dependency cache: .cargo/"
git push origin add-rust-template
```

### PR description

```markdown
## Summary

[One sentence]

## Changes

- [Change 1]
- [Change 2]

## Design decisions

- Template type: [framework/language/tool/etc.] — why?
- Key patterns: [brief justification]

## Verification

- [ ] Tested with `git check-ignore`
- [ ] Tested with a real project
- [ ] No duplicate patterns
- [ ] Patterns alpha-sorted per section

## References

- Official .gitignore: [URL]
- Related issue: #[number]
```

### Common rejection reasons

| Reason                               | Prevention                                   |
| ------------------------------------ | -------------------------------------------- |
| Duplicate of existing template       | Search thoroughly in Stage 1                 |
| Wrong template type                  | Review decision tree in Stage 2              |
| Missing security section (framework) | Framework templates MUST have security first |
| Has security section (language)      | Language templates MUST NOT have security    |
| Patterns not alpha-sorted            | Sort each section before Stage 4             |
| No testing evidence                  | Run verification procedure in Stage 4        |
| Violates TEMPLATE_STANDARDS.md       | Read it before Stage 3                       |

---

## Anti-patterns

For a catalog of known template mistakes and how to avoid them, see [TEMPLATE_STANDARDS.md §Common Mistakes](TEMPLATE_STANDARDS.md#common-mistakes).

---

## Getting Help

- **Template standards:** [`TEMPLATE_STANDARDS.md`](TEMPLATE_STANDARDS.md) — definitive design system
- **Repository operations:** [`AGENTS.md`](AGENTS.md) — operations manual
- **Issues:** [GitHub Issues](https://github.com/ronald2wing/.gitignores/issues)
- **Online tool:** [gitignores.com](https://gitignores.com)
