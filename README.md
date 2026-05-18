<div align="center">

# 🔍 Documentation Drift Detector

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/Version-1.0.0-blue?style=for-the-badge&logo=semver)](https://github.com/Zarl-prog/doc-drift-detector/releases)
[![Made with Claude](https://img.shields.io/badge/Made%20with-Claude%20Sonnet%204-blueviolet?style=for-the-badge&logo=anthropic)](https://www.anthropic.com)
[![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Stars](https://img.shields.io/github/stars/Zarl-prog/doc-drift-detector?style=for-the-badge&logo=github&color=gold)](https://github.com/Zarl-prog/doc-drift-detector/stargazers)

<br/>

### 🚀 *Catch documentation rot before it catches you.*

**A Claude-powered skill that scans, detects, and fixes mismatches between your code and its documentation — automatically.**

<br/>

[🚀 Quick Start](#-quick-install) · [✨ Features](#-features) · [🧠 How It Works](#-how-it-works) · [💬 Example Prompts](#-example-prompts) · [🤝 Contributing](#-contributing)

<br/>

---

</div>

## 📖 What Is Documentation Drift?

Documentation drift happens when code evolves but its documentation doesn't keep up. This leads to:

- 📄 **Stale READMEs** with outdated installation steps or API references
- 💥 **Broken code examples** that no longer compile or run correctly
- 🕳️ **Orphaned sections** describing features that no longer exist
- 🔇 **Undocumented public APIs** that leave developers guessing
- 🐛 **Misleading docstrings** that describe old behavior

**Documentation Drift Detector** gives Claude the ability to catch all of these — and optionally fix them — in seconds.

<br/>

---

## ⚡ Quick Install

```bash
# Clone the repository
git clone https://github.com/Zarl-prog/doc-drift-detector.git
cd doc-drift-detector

# Install dependencies
pip install -r requirements.txt

# Add the skill to Claude
cp skill.md ~/.claude/skills/doc-drift-detector.md
```

> **Requires:** Python 3.8+, Claude Sonnet 4+, Git 2.0+ *(optional, for git-diff scanning)*

<br/>

---

## ✨ Features

| Feature | Description | Status |
|--------|-------------|--------|
| ✅ **README Drift Detection** | Finds stale install steps, outdated badges, broken links | Stable |
| ✅ **Docstring Validator** | Checks function signatures against their docstrings | Stable |
| ✅ **Code Example Auditor** | Verifies code blocks in docs still reflect real code | Stable |
| ✅ **Orphaned Section Finder** | Detects docs for features that no longer exist | Stable |
| ✅ **Undocumented API Scanner** | Surfaces public functions/classes with no docs | Stable |
| ✅ **Auto-Fix Mode** | Rewrites stale docs using Claude — with your approval | Stable |
| 🔄 **Git-Diff Aware Scanning** | Only checks files changed since last commit | Beta |
| 🔄 **PR Pre-flight Check** | Runs automatically before pull requests | Beta |
| 🧪 **Onboarding Audit Mode** | Full repo scan for new contributors | Planned |

<br/>

---

## 📂 Project Structure

```
doc-drift-detector/
│
├── 📁 skill/
│   ├── 📄 skill.md               ← Claude skill definition
│   ├── 🐍 scanner.py             ← Core drift detection engine
│   └── 🔧 fixer.py               ← Auto-fix module (Claude-powered)
│
├── 📁 prompts/
│   ├── 💬 detect_prompt.txt      ← Detection system prompt
│   └── ✏️  fix_prompt.txt         ← Rewrite system prompt
│
├── 📁 examples/
│   ├── 🗂️  sample_project/        ← Demo repo with intentional drift
│   └── 📊 sample_report.json     ← Example drift report output
│
├── 📁 tests/
│   └── 🧪 test_scanner.py        ← Unit tests
│
├── 📄 requirements.txt
├── 📄 SKILL.md                   ← Skill creator metadata
└── 📖 README.md                  ← You are here!
```

<br/>

---

## 🧠 How It Works

**1️⃣ Trigger Detection**

You invoke the skill — via a natural language prompt, the `/doc-drift` command, or automatically before a PR. Claude loads the skill context and begins its analysis.

**2️⃣ Code Parsing**

The scanner walks your repository, extracting public APIs, function signatures, class definitions, and module-level docstrings from your Python (and optionally JS/TS) source files.

**3️⃣ Documentation Indexing**

Claude reads your documentation files — READMEs, wikis, inline docstrings, code examples in Markdown — and maps them to the source symbols they describe.

**4️⃣ Drift Analysis**

Using Claude Sonnet 4, each doc–code pair is compared semantically (not just textually). Claude identifies:
- Signature mismatches in docstrings
- Code blocks that no longer reflect real behavior
- References to deleted or renamed symbols
- Public symbols with zero documentation coverage

**5️⃣ Report Generation**

A structured drift report is produced, grouped by severity: 🔴 **Critical**, 🟡 **Warning**, 🟢 **Info**.

**6️⃣ Optional Auto-Fix**

With `--fix` mode enabled, Claude rewrites the stale documentation, shows you a diff, and awaits your approval before writing changes.

<br/>

---

## 💬 Example Prompts

> 🗣️ *"Is the documentation up to date?"*

> 🗣️ *"/doc-drift scan src/ docs/"*

> 🗣️ *"Scan my README and check if the code examples still work."*

> 🗣️ *"Before I open this PR, check if anything in the docs is now stale."*

> 🗣️ *"Find all public functions in utils.py that are missing docstrings."*

> 🗣️ *"Run a full onboarding audit — I want a clean repo for new contributors."*

> 🗣️ *"Detect drift and auto-fix any stale docstrings, but ask me before saving."*

<br/>

---

## 📊 Sample Output

```
🔍 Documentation Drift Report
════════════════════════════════════════════
📁 Scanned: 24 files  |  ⏱️ Time: 3.2s  |  🔗 Git: main@a3f92c1

🔴 CRITICAL  (2 issues)
  ✗ README.md:47 — Code example calls `connect(host, port)` but signature
                    is now `connect(url, timeout=30)`
  ✗ api/auth.py — `generate_token()` is public but has no docstring

🟡 WARNING   (5 issues)
  ⚠ docs/setup.md:12 — References `pip install old-package-name` (renamed)
  ⚠ utils/parser.py:88 — Docstring mentions `--verbose` flag (removed)
  ⚠ README.md:103 — Section "Legacy XML Support" describes removed feature
  ⚠ core/client.py — 3 public methods undocumented: send(), retry(), close()
  ⚠ docs/api.md:67 — Orphaned section: `Client.batch_send` no longer exists

🟢 INFO      (3 issues)
  ℹ changelog.md — 4 entries reference v0.x which is EOL
  ℹ README.md — Badge links to old CI provider (Travis CI → GitHub Actions)
  ℹ docs/config.md — Example config uses deprecated key `db_host`

════════════════════════════════════════════
🎯 Score: 71/100  |  Run with --fix to auto-repair 6 of 10 issues
```

<br/>

---

## 🛠️ Configuration

Create a `.doc-drift.yml` in your project root to customize behavior:

```yaml
# .doc-drift.yml
scan:
  source_dirs: ["src/", "lib/"]
  doc_dirs: ["docs/", "README.md"]
  languages: ["python", "typescript"]
  ignore: ["**/migrations/**", "**/generated/**"]

thresholds:
  fail_on: critical          # critical | warning | any
  min_score: 80              # 0–100 drift health score

fix:
  auto_fix: false            # require approval before writing
  style: concise             # concise | verbose | numpy | google

git:
  enabled: true
  scan_since: last_commit    # last_commit | last_tag | HEAD~5
```

<br/>

---

## 🔗 Trigger Reference

| Trigger | When It Fires |
|--------|---------------|
| `"is the documentation up to date?"` | Natural language prompt |
| `/doc-drift` | Slash command |
| `--pre-pr` flag | Before opening a pull request |
| Code file modified | Watches for file change events |
| `onboarding-audit` | Full repo sweep for new contributors |
| After major refactor | Keyword detection in commit messages |

<br/>

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

<div align="center">

<a href="https://github.com/Zarl-prog">
  <img src="https://github.com/Zarl-prog.png" width="60px" style="border-radius: 50%;" alt="Zarl-prog"/>
  <br/>
  <sub><b>Zarl-prog</b></sub>
</a>

<br/><br/>

[![Fork](https://img.shields.io/badge/🍴%20Fork%20the%20Repo-181717?style=for-the-badge&logo=github)](https://github.com/Zarl-prog/doc-drift-detector/fork)
[![Open Issue](https://img.shields.io/badge/🐛%20Open%20an%20Issue-red?style=for-the-badge&logo=github)](https://github.com/Zarl-prog/doc-drift-detector/issues/new)
[![Submit PR](https://img.shields.io/badge/🚀%20Submit%20a%20PR-brightgreen?style=for-the-badge&logo=github)](https://github.com/Zarl-prog/doc-drift-detector/pulls)

</div>

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting changes. All contributors are expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md).

<br/>

---

## 📜 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for full details.

<br/>

---

<div align="center">

**Built with 🤍 and Claude Sonnet 4 by [Zarl-prog](https://github.com/Zarl-prog)**

[![Made with Claude](https://img.shields.io/badge/Powered%20by-Claude%20Sonnet%204-blueviolet?style=flat-square&logo=anthropic)](https://www.anthropic.com)
[![MIT License](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)
[![Maintained](https://img.shields.io/badge/Maintained-yes-green.svg?style=flat-square)](https://github.com/Zarl-prog/doc-drift-detector/graphs/commit-activity)

*If this skill saved your docs, consider giving it a ⭐ — it helps more developers find it!*

</div>
