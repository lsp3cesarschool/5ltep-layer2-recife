# Signals in https://dados.recife.pe.gov.br

Plain-text summary of the latest run of Layer 2 (semantic policies), for readers that do not run
the JavaScript of the [dashboard](https://lsp3cesarschool.github.io/5ltep-layer2-recife/).
Generated automatically by the publish job from the checked results; do not edit by hand. A signal is a record to review, never a verdict on the data. Only counts are
shown here: the record numbers are on the dashboard and in [`docs/data/rules/`](docs/data/rules/),
and no value read from the portals is published. Times are UTC.

- **Run:** [40674382639](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/runs/40674382639), finished 2026-10-28 11:05 UTC (github-actions)
- **Rules:** 12 (0 evaluated, 12 not evaluated)
- **Sources:** 6 CKAN resources (0 available)
- **Records flagged:** 0
- **L2 pass rate:** – (checks without a signal / 0 checks in scope; one check per record and rule)

Signal types: `mismatch` (the check failed), `key not found` (no matching record in the other
source), `missing value`, `invalid value` (unreadable as the declared type), `ambiguous key` (more
than one match). Records outside a rule's scope (`where`) are not signals.

## Rules (most signals first)

| Rule | Records read | Signals | Previous run | Signal types |
|---|---:|---:|---:|---|
| [Amendment ending before it starts](rules/contracts/amendment-end-before-start.yaml) | – | – | – | not evaluated: fonte "recife_aditivos" (dados.recife.pe.gov.br › contratos › Termo Aditivo): portal não respondeu: tempo esgotado (60 s) |
| [Amendment without a matching contract in the extract](rules/contracts/amendment-without-contract.yaml) | – | – | – | not evaluated: fonte "recife_aditivos" (dados.recife.pe.gov.br › contratos › Termo Aditivo): portal não respondeu: tempo esgotado (60 s) |
| [Contract ending before it starts](rules/contracts/contract-end-before-start.yaml) | – | – | – | not evaluated: fonte "recife_contratos" (dados.recife.pe.gov.br › contratos › Contratos): portal não respondeu: tempo esgotado (60 s) |
| [Birth date after the dengue notification](rules/health/dengue-birth-after-notification.yaml) | – | – | – | not evaluated: fonte "recife_dengue" (dados.recife.pe.gov.br › casos-de-dengue-zika-e-chikungunya › Casos de Dengue 202[245]): portal não respondeu: tempo esgotado (60 s) |
| [Dengue first symptoms dated after the notification](rules/health/dengue-symptoms-after-notification.yaml) | – | – | – | not evaluated: fonte "recife_dengue" (dados.recife.pe.gov.br › casos-de-dengue-zika-e-chikungunya › Casos de Dengue 202[245]): portal não respondeu: tempo esgotado (60 s) |
| [Licensed enterprise located outside Recife](rules/licensing/enterprise-coordinates-outside-recife.yaml) | – | – | – | not evaluated: fonte "recife_licencas" (dados.recife.pe.gov.br › licenciamento-ambiental › Licenciamento Ambiental): portal não respondeu: tempo esgotado (60 s) |
| [Fatal victims above the total number of victims](rules/traffic/fatal-victims-above-victims.yaml) | – | – | – | not evaluated: fonte "recife_acidentes" (dados.recife.pe.gov.br › acidentes-de-transito-com-e-sem-vitimas › Acidentes de Trânsito 202[234]): portal não respondeu: tempo esgotado (60 s) |
| [Licence issued before the request was filed](rules/licensing/licence-issued-before-request.yaml) | – | – | – | not evaluated: fonte "recife_licencas" (dados.recife.pe.gov.br › licenciamento-ambiental › Licenciamento Ambiental): portal não respondeu: tempo esgotado (60 s) |
| [Municipal licence valid until a date before it was issued](rules/licensing/licence-validity-before-issue.yaml) | – | – | – | not evaluated: fonte "recife_licencas" (dados.recife.pe.gov.br › licenciamento-ambiental › Licenciamento Ambiental): portal não respondeu: tempo esgotado (60 s) |
| [Accident recorded without victims but with victims counted](rules/traffic/no-victim-accident-with-victims.yaml) | – | – | – | not evaluated: fonte "recife_acidentes" (dados.recife.pe.gov.br › acidentes-de-transito-com-e-sem-vitimas › Acidentes de Trânsito 202[234]): portal não respondeu: tempo esgotado (60 s) |
| [Weighing ending before it starts](rules/waste/weighing-end-before-start.yaml) | – | – | – | not evaluated: fonte "recife_pesagem" (dados.recife.pe.gov.br › pesagem-de-coletas-de-residuos › Pesagem de Resíduos - 201[234]): portal não respondeu: tempo esgotado (60 s) |
| [Net weight different from initial minus final weight](rules/waste/weighing-net-weight-balance.yaml) | – | – | – | not evaluated: fonte "recife_pesagem" (dados.recife.pe.gov.br › pesagem-de-coletas-de-residuos › Pesagem de Resíduos - 201[234]): portal não respondeu: tempo esgotado (60 s) |

## Source health

| Resource | Role | Status | Size | Download | Used by |
|---|---|---|---:|---:|---|
| dados.recife.pe.gov.br › contratos › Termo Aditivo | primary | failed: portal não respondeu: tempo esgotado (60 s) | – | – | amendment-end-before-start, amendment-without-contract |
| dados.recife.pe.gov.br › contratos › Contratos | primary | failed: portal não respondeu: tempo esgotado (60 s) | – | – | amendment-without-contract, contract-end-before-start |
| dados.recife.pe.gov.br › casos-de-dengue-zika-e-chikungunya › Casos de Dengue 202[245] | primary | failed: portal não respondeu: tempo esgotado (60 s) | – | – | dengue-birth-after-notification, dengue-symptoms-after-notification |
| dados.recife.pe.gov.br › licenciamento-ambiental › Licenciamento Ambiental | primary | failed: portal não respondeu: tempo esgotado (60 s) | – | – | enterprise-coordinates-outside-recife, licence-issued-before-request, licence-validity-before-issue |
| dados.recife.pe.gov.br › acidentes-de-transito-com-e-sem-vitimas › Acidentes de Trânsito 202[234] | primary | failed: portal não respondeu: tempo esgotado (60 s) | – | – | fatal-victims-above-victims, no-victim-accident-with-victims |
| dados.recife.pe.gov.br › pesagem-de-coletas-de-residuos › Pesagem de Resíduos - 201[234] | primary | failed: portal não respondeu: tempo esgotado (60 s) | – | – | weighing-end-before-start, weighing-net-weight-balance |
