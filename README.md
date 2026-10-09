# 5LTEP-L2 · Recife instance (control experiment)

[![Tests](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml/badge.svg)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml) [![Layer 2](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer2-recife%2Fmain%2Fdocs%2Fdata%2Fstatus.json)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/layer2.yml) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**English** · [Português](LEIAME.md)

**12 domain rules that cross CKAN open data portals, applied to the portal of the City of Recife.**
People write the rules after the data is published, one check per file. Every week the engine of
this layer evaluates each rule: it reads the published files, flags the records that deserve a
second look and shows them on a dashboard. A signal is an invitation to review, never a verdict on
the data.

| Resource | What you find there |
|---|---|
| 📊 **Dashboard** | [lsp3cesarschool.github.io/5ltep-layer2-recife](https://lsp3cesarschool.github.io/5ltep-layer2-recife/?lang=en): each rule with its signals, charts and record numbers; source health, download and processing speed, history and provenance |
| 📏 **Rules** | [`rules/`](rules/): one check per file, in plain YAML |
| 📁 **Results** | [`results/`](results/) and [`docs/data/`](docs/data/): what each run writes (counts, record numbers, hashes) |
| 🏛️ **Main instance** | [5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2) (IBAMA): the full documentation and the rule manual; [dashboard](https://lsp3cesarschool.github.io/5ltep-layer2/?lang=en) |
| 🔁 **Other control** | [5ltep-layer2-aneel](https://github.com/lsp3cesarschool/5ltep-layer2-aneel) ([dashboard](https://lsp3cesarschool.github.io/5ltep-layer2-aneel/?lang=en)): the same code on the portal of ANEEL |

> **Status: research demonstration.** This repository is part of a master's research project and
> is maintained by its author. It is not operated by, affiliated with or endorsed by the City of
> Recife or any other publisher; it only reads open data from CKAN portals. The rules are examples
> written by the author.

## Use case in one paragraph

A journalist wants to count traffic deaths in Recife using the city's accident records. When an
accident lists more fatal victims than victims, or a "no victim" accident lists victims, the count
depends on which field the journalist happens to read. The rules in this repository check those two
fields, and also the dates of municipal environmental licences and of contracts and amendments,
whether every amendment has its contract in the published extract, the balance of the waste
collection weighings and the order of the dates in dengue notifications. Dengue data are health
data, so those rules publish only counts and charts, never record numbers. The city publishes one
resource per year and the header changes from one year to another, so each rule reads only the years
that have the columns it needs.

## Key terms

| Term | Meaning here |
|---|---|
| **Rule** | A YAML file in `rules/` with a description for people and a check for the engine. Every file in `rules/` is active; subfolders only organise them. |
| **Source** | The CKAN resource a rule reads (portal, dataset, exact resource name and format), or several resources of one dataset matched by a name pattern, together with how to open the file and which columns to read. |
| **Template** | The fixed check a rule fills in: `lookup-equals`, `lookup-exists`, `temporal-order`, `field-comparison` or `flag-when`. Rules never contain SQL or code. |
| **Signal** | A record that failed the check or could not be checked (missing or unreadable value, key not found). Something to review, not a verdict. |
| **Record number** | The line of the record in the published file (1 is the first line after the header), valid for the bytes whose SHA-256 the run records. |
| **Source health** | Whether each portal answered and each resource downloaded during a run. A rule whose source failed is marked "not evaluated"; it is never evaluated halfway. |

## How a rule looks

```
schema_version: "1.0"
rule_version: "0.3.0"
origin: cross_reference
description:  {language, title, text, justification, exceptions, examples}
sources:      {name: {portal, dataset, resource, archive, file, columns}}
check:        {template, parameters, where, timeline}
```

The file name is the rule's identifier. A single contract,
[`schema/rule-v1.schema.json`](schema/rule-v1.schema.json), describes the format of every rule, and
`python main.py validate` checks each file against it and makes sure that every column the check
uses has been declared. The rule manual in the main repository explains each field.

## How a run works

[`.github/workflows/layer2.yml`](.github/workflows/layer2.yml) runs every Wednesday at 04:30 UTC and
can also be started by hand. The **evaluate** job, which has a read-only token, downloads each CKAN
resource once, however many rules use it, and records whether each portal and resource was
available. It then reads only the declared columns, evaluates every rule with DuckDB without
external access and uploads the outputs as an artifact. The **publish** job checks that artifact
with `python main.py accept` (only the expected files, valid JSON, record lists made only of
numbers, earlier history preserved) and commits `results/` and `docs/data/`. Each run also records
the download speed of this portal and of the others, and how long each phase took.

## Data handling and privacy

This repository is designed to comply with Brazil's General Data Protection Law (LGPD, Law
13,709/2018), including for data the portals already publish openly. In practice, files are
downloaded during the run and deleted when it ends; on GitHub, the runner itself is discarded after
the job. The engine reads only the columns a rule declares, and publishes only counts, record
numbers, SHA-256 hashes and metadata that CKAN already publishes, never a value read from the
portals. Rules on health or education data use `exposure: counts`, so they publish counts and charts
but no record numbers. The datasets keep their publishers' licences, which the dashboard lists with
links.

## Run it locally

```
python -m pip install -r requirements.txt
python main.py validate
python -m pytest
python main.py run        # local test run: downloads the sources, outputs in work/out
```

A local run is only a test: published results come from GitHub Actions alone.

## Repository layout

```
main.py            command line (validate, run, accept)
src/               loader, validator, templates, fetch, engine, outputs, accept
schema/            JSON Schema of the rule format
rules/             one file per rule, in subfolders
portal.json        the portal of this instance
docs/              dashboard (data/ is written by the runs)
results/           results of the runs
tests/             automated tests
```

## License and citation

The code is under the [MIT License](LICENSE). Citation metadata is in
[`CITATION.cff`](CITATION.cff).

