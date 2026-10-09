# 5LTEP-L2 · Recife instance (control experiment)

[![Tests](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml/badge.svg)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml) [![Layer 2](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer2-recife%2Fmain%2Fdocs%2Fdata%2Fstatus.json)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/layer2.yml) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**English** · [Português](LEIAME.md)

**5L-TEP Layer 2 (semantic policies) applied to the open data portal of the city of Recife: another instance of
[5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2), set up by the author as a control case
for the IBAMA study.**

| Resource | What you find there |
|---|---|
| 📊 **Dashboard** | [lsp3cesarschool.github.io/5ltep-layer2-recife](https://lsp3cesarschool.github.io/5ltep-layer2-recife/?lang=en): rules, signals, source health, history |
| 📏 **Rules** | [`rules/`](rules/): one file per check, for traffic accidents, contracts and amendments, environmental licences, waste weighing and arbovirus notifications (counts only) |
| 🏛️ **Main instance** | [5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2): IBAMA, and the full documentation |
| 🔁 **Other control** | [5ltep-layer2-aneel](https://github.com/lsp3cesarschool/5ltep-layer2-aneel): the ANEEL portal |

> **Status: research demonstration.** This repository is not operated by, affiliated with or endorsed
> by Recife; it only reads open data from CKAN portals. The rules are examples written by the author:
> a signal is something to review, never a verdict on the data. Only counts and record numbers are
> published, never values from the portals.

## What differs from the main instance

Only the configuration and the rules: [`portal.json`](portal.json) names this portal, and
[`rules/`](rules/) holds the checks written for its datasets. The engine, the rule format, the
validator, the dashboard and the workflows are the same code as
[5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2) (d9ee325). Some rules reuse a
check of the IBAMA instance on other columns, which is the reuse the study measures.

## Run it

```
python -m pip install -r requirements.txt
python main.py validate
python main.py run        # local test run: downloads the sources, outputs in work/out
```

## License and citation

Code under the [MIT License](LICENSE). Citation metadata in [`CITATION.cff`](CITATION.cff).
