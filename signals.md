# Signals in https://dados.recife.pe.gov.br

Plain-text summary of the latest run of Layer 2 (semantic policies), for readers that do not run
the JavaScript of the [dashboard](https://lsp3cesarschool.github.io/5ltep-layer2-recife/).
Generated automatically by the publish job from the checked results; do not edit by hand. A signal is a record to review, never a verdict on the data. Only counts are
shown here: the record numbers are on the dashboard and in [`docs/data/rules/`](docs/data/rules/),
and no value read from the portals is published. Times are UTC.

- **Run:** [37937376104](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/runs/37937376104), finished 2026-10-09 13:31 UTC (github-actions)
- **Rules:** 12 (12 evaluated, 0 not evaluated)
- **Sources:** 6 CKAN resources (6 available)
- **Records flagged:** 117
- **L2 pass rate:** 100.0% (checks without a signal / 941,257 checks in scope; one check per record and rule)

Signal types: `mismatch` (the check failed), `key not found` (no matching record in the other
source), `missing value`, `invalid value` (unreadable as the declared type), `ambiguous key` (more
than one match). Records outside a rule's scope (`where`) are not signals.

## Rules (most signals first)

| Rule | Records read | Signals | Previous run | Signal types |
|---|---:|---:|---:|---|
| [Fatal victims above the total number of victims](rules/traffic/fatal-victims-above-victims.yaml) | 12,016 | 55 | 55 | mismatch 55 |
| [Amendment ending before it starts](rules/contracts/amendment-end-before-start.yaml) | 13,390 | 40 | 40 | mismatch 40 |
| [Licence issued before the request was filed](rules/licensing/licence-issued-before-request.yaml) | 49,924 | 15 | 15 | mismatch 15 |
| [Contract ending before it starts](rules/contracts/contract-end-before-start.yaml) | 7,912 | 6 | 6 | mismatch 6 |
| [Net weight different from initial minus final weight](rules/waste/weighing-net-weight-balance.yaml) | 381,128 | 1 | 1 | mismatch 1 |
| [Amendment without a matching contract in the extract](rules/contracts/amendment-without-contract.yaml) | 13,390 | 0 | 0 | none |
| [Birth date after the dengue notification](rules/health/dengue-birth-after-notification.yaml) | 22,641 | 0 | 0 | none |
| [Dengue first symptoms dated after the notification](rules/health/dengue-symptoms-after-notification.yaml) | 22,641 | 0 | 0 | none |
| [Licensed enterprise located outside Recife](rules/licensing/enterprise-coordinates-outside-recife.yaml) | 49,924 | 0 | 0 | none |
| [Municipal licence valid until a date before it was issued](rules/licensing/licence-validity-before-issue.yaml) | 49,924 | 0 | 0 | none |
| [Accident recorded without victims but with victims counted](rules/traffic/no-victim-accident-with-victims.yaml) | 12,016 | 0 | 0 | none |
| [Weighing ending before it starts](rules/waste/weighing-end-before-start.yaml) | 381,128 | 0 | 0 | none |

## Source health

| Resource | Role | Status | Size | Download | Used by |
|---|---|---|---:|---:|---|
| dados.recife.pe.gov.br › contratos › Termo Aditivo | primary | available | 6.0 MB | 3.9 s | amendment-end-before-start, amendment-without-contract |
| dados.recife.pe.gov.br › contratos › Contratos | primary | available | 3.7 MB | 0.9 s | amendment-without-contract, contract-end-before-start |
| dados.recife.pe.gov.br › casos-de-dengue-zika-e-chikungunya › Casos de Dengue 202[245] | primary | available | 13.2 MB | 2.4 s | dengue-birth-after-notification, dengue-symptoms-after-notification |
| dados.recife.pe.gov.br › licenciamento-ambiental › Licenciamento Ambiental | primary | available | 40.5 MB | 5.9 s | enterprise-coordinates-outside-recife, licence-issued-before-request, licence-validity-before-issue |
| dados.recife.pe.gov.br › acidentes-de-transito-com-e-sem-vitimas › Acidentes de Trânsito 202[234] | primary | available | 3.7 MB | 2.3 s | fatal-victims-above-victims, no-victim-accident-with-victims |
| dados.recife.pe.gov.br › pesagem-de-coletas-de-residuos › Pesagem de Resíduos - 201[234] | primary | available | 82.6 MB | 7.0 s | weighing-end-before-start, weighing-net-weight-balance |
