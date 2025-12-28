# AGENTS.md

> **Audience:** AI agents operating on this repository.  
> **Authoritative reference:** [`TEMPLATE_STANDARDS.md`](TEMPLATE_STANDARDS.md)

---

## Architecture

**Template factory** — no build, lint, test, or package manager. Every template is a standalone `.gitignore` file.

### Two Systems — pick one, never mix

|          | Framework                     | Modular                                  |
| -------- | ----------------------------- | ---------------------------------------- |
| Start    | `frameworks/<name>.gitignore` | `languages/<name>.gitignore`             |
| Security | Built-in (first section)      | **Must** add `common/security.gitignore` |
| Extras   | IDEs, OS only                 | common/\*, tools/\*, ides/\*, os/\*      |

### Hard Constraints

1. **Framework + Language = NEVER** — frameworks already contain language patterns.
2. **Language without Security = NEVER** — add `common/security.gitignore`.
3. **Combine with `sort -u` = ALWAYS** — `cat a b c | sort -u > .gitignore`.

---

## Creating or Editing

```
Language?    → languages/<name>.gitignore     (no security section)
Framework?   → frameworks/<name>.gitignore    (security section FIRST)
Tool/CI?     → tools/<name>.gitignore
IDE?         → ides/<name>.gitignore
OS?          → os/<name>.gitignore
Platform?    → platforms/<name>.gitignore
```

Naming, section ordering, header/metadata format → [`TEMPLATE_STANDARDS.md`](TEMPLATE_STANDARDS.md).  
Section ordering gotcha: some existing templates (e.g. `languages/rust.gitignore`) have non-standard sections — new templates must follow the canonical order.

---

## Combining Templates

1. **Pick core** — Framework OR language, never both.
2. **Add security** — `common/security.gitignore` for language templates.
3. **Layer extras** — Tools, IDEs, OS as needed.
4. **Deduplicate** — pipe through `sort -u`.
5. **Validate** — `git status --ignored` in a test repo.

---

## Verification

```bash
# Dedup check (must produce no output)
sort template.gitignore | uniq -d

# Smoke test (adapt touch files to template patterns)
mkdir /tmp/gitignore-test && cd /tmp/gitignore-test && git init
cp /path/to/template.gitignore .gitignore
touch .env .env.local credentials.json secret.key
git status --ignored   # All four should appear under "Ignored files"
```

Full procedure → [`TEMPLATE_STANDARDS.md §Quality Gates`](TEMPLATE_STANDARDS.md#quality-gates).

---

## Troubleshooting

```bash
git ls-files <path>          # Already tracked? Ignores don't apply.
git check-ignore -v <path>   # Which rule ignores this file?
git rm --cached <path>       # Untrack so ignore takes effect.
```
