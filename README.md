# .gitignores

> A systematic collection of `.gitignore` templates — from single-file framework templates to multi-template combinations covering your entire toolchain.

**Online generator:** [gitignores.com](https://gitignores.com)

---

## How It Works

Pick the approach that matches your project.

### Framework Templates

Pick **one** file from `frameworks/`. Done.

Framework templates are self-contained — they bundle security, language, and tool patterns into a single file.

```bash
cp frameworks/react.gitignore .gitignore
```

**What's inside:** security patterns → build artifacts → dependencies → framework-specific patterns → testing artifacts.

### Modular Templates

Pick a **language** template, add **security**, then layer tools, IDEs, and OS patterns as needed.

```bash
cat languages/python.gitignore \
    common/security.gitignore \
    tools/docker.gitignore \
    ides/visual-studio-code.gitignore | sort -u > .gitignore
```

### The cardinal rule

> Framework + Language = **NEVER**. Frameworks already contain language patterns. Combining them creates duplicates.

---

## Getting Started

**Download a single template:**

```bash
curl -o .gitignore https://raw.githubusercontent.com/ronald2wing/.gitignores/master/frameworks/react.gitignore
```

**Clone and use locally:**

```bash
git clone https://github.com/ronald2wing/.gitignores.git ~/.gitignores
cp ~/.gitignores/frameworks/react.gitignore .gitignore
```

**Use the web generator:** [gitignores.com](https://gitignores.com)

---

## Template Catalog

| Category       | Count | Purpose                                  | Pick when                              |
| -------------- | ----- | ---------------------------------------- | -------------------------------------- |
| **Frameworks** | 34    | Self-contained, security-first           | Using React, Django, Rails, etc.       |
| **Languages**  | 31    | Language patterns (modular, no security) | Custom stacks needing granular control |
| **Tools**      | 37    | Build tools, CI/CD, package managers     | Adding Docker, GitHub Actions, etc.    |
| **IDEs**       | 14    | Editor config and cache                  | VS Code, IntelliJ, Vim, etc.           |
| **Common**     | 7     | Shared patterns (security, cache, logs)  | Always pair with language templates    |
| **OS**         | 3     | OS-specific artifacts                    | Cross-platform teams                   |
| **Platforms**  | 3     | Platform development patterns            | Android, iOS, Unity                    |

---

## Recipes

### Single framework + your editor

```bash
cat frameworks/react.gitignore \
    ides/visual-studio-code.gitignore | sort -u > .gitignore
```

### Custom language stack

```bash
# Python data pipeline with Docker and GitLab CI
cat languages/python.gitignore \
    common/security.gitignore \
    tools/docker.gitignore \
    tools/gitlab-ci.gitignore | sort -u > .gitignore
```

### Full toolchain

```bash
# Next.js, Docker, GitHub Actions, VS Code, cross-platform OS
cat frameworks/nextjs.gitignore \
    tools/docker.gitignore \
    tools/github-actions.gitignore \
    ides/visual-studio-code.gitignore \
    os/linux.gitignore \
    os/macos.gitignore \
    os/windows.gitignore | sort -u > .gitignore
```

---

## FAQ

**Framework or language template?**
Framework = you're using a named framework (React, Django, Laravel). Language = you're mixing tools at a lower level.

**Why doesn't the Python template include security patterns?**
Language templates are pure — only language patterns. Security lives in `common/security.gitignore` so it's shared without duplication.

**My .gitignore isn't working.**
See [AGENTS.md §Troubleshooting](AGENTS.md#troubleshooting) for a complete diagnostic workflow.

**How do I request a new template?**
Open an issue. Check [existing templates](https://github.com/ronald2wing/.gitignores) and open issues first.

---

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the contribution lifecycle.  
See [`TEMPLATE_STANDARDS.md`](TEMPLATE_STANDARDS.md) for the template design system.  
See [`AGENTS.md`](AGENTS.md) for the repository operations manual.

**Repository:** [github.com/ronald2wing/.gitignores](https://github.com/ronald2wing/.gitignores)
