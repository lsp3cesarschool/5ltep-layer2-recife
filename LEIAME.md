# 5LTEP-L2 · Instância Recife (experimento de controle)

[![Testes](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml/badge.svg)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml) [![Camada 2](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer2-recife%2Fmain%2Fdocs%2Fdata%2Fstatus.pt.json)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/layer2.yml) [![Licença: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[English](README.md) · **Português**

**Regras de domínio, escritas por pessoas depois que os dados existem, que cruzam portais de dados
abertos CKAN: 12 regras sobre o portal da Prefeitura do Recife.** Toda semana cada regra lê os
arquivos publicados, conta os registros que merecem um segundo olhar e os mostra num dashboard. Um
sinal é algo a revisar, nunca um veredito sobre os dados.

| Recurso | O que há lá |
|---|---|
| 📊 **Dashboard** | [lsp3cesarschool.github.io/5ltep-layer2-recife](https://lsp3cesarschool.github.io/5ltep-layer2-recife/?lang=pt): cada regra com seus sinais, gráficos e números de registro, saúde das fontes, velocidade de download e de processamento, histórico, proveniência |
| 📏 **Regras** | [`rules/`](rules/): um arquivo por verificação, em YAML legível |
| 📁 **Resultados** | [`results/`](results/) e [`docs/data/`](docs/data/): gravados a cada rodada (contagens, números de registro, hashes) |
| 🏛️ **Instância principal** | [5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2) (IBAMA): a documentação completa e o manual de regras; [dashboard](https://lsp3cesarschool.github.io/5ltep-layer2/?lang=pt) |
| 🔁 **Outro controle** | [5ltep-layer2-aneel](https://github.com/lsp3cesarschool/5ltep-layer2-aneel) ([dashboard](https://lsp3cesarschool.github.io/5ltep-layer2-aneel/?lang=pt)): o portal da ANEEL |

> **Estado: demonstração de pesquisa.** Este repositório faz parte de um projeto de mestrado e é
> mantido pelo autor. Não é operado, afiliado nem endossado pela Prefeitura do Recife nem por outro publicador; só lê
> dados abertos de portais CKAN. As regras são exemplos escritos pelo autor.

## Caso de uso em um parágrafo

Um jornalista conta as mortes no trânsito do Recife a partir dos registros de acidentes da prefeitura.
Se um acidente traz mais vítimas fatais que vítimas, ou um acidente "sem vítima" traz vítimas, a
contagem depende do campo que se lê. As regras deste repositório conferem esses dois campos, as
datas das licenças ambientais municipais e dos contratos e aditivos, se todo aditivo tem seu contrato
no extrato publicado, o balanço das pesagens da coleta de resíduos e a ordem das datas das
notificações de dengue. Dengue é dado de saúde: essas regras publicam só contagens e gráficos, nunca
números de registro. A prefeitura publica um recurso por
ano, e o cabeçalho muda entre os anos: cada regra lê só os anos que têm as colunas de que precisa.

## Termos-chave

| Termo | Significado aqui |
|---|---|
| **Regra** | Um arquivo YAML em `rules/`: uma descrição para pessoas e uma verificação para o motor. Arquivo em `rules/` está ativo; subpastas só organizam. |
| **Fonte** | Um recurso CKAN (portal, dataset, nome e formato exatos do recurso), ou vários recursos de um dataset por padrão de nome, com o modo de abrir o arquivo e as colunas a ler. |
| **Modelo** | A verificação fixa que a regra preenche: `lookup-equals`, `lookup-exists`, `temporal-order`, `field-comparison`, `flag-when`. Regras nunca trazem SQL nem código. |
| **Sinal** | Registro que não passou na verificação, ou que não pôde ser verificado (valor ausente ou ilegível, chave não encontrada). Algo a revisar, não um veredito. |
| **Número de registro** | A linha do registro no arquivo publicado (1 = primeira linha após o cabeçalho), válida para os bytes cujo SHA-256 a rodada registra. |
| **Saúde das fontes** | Se cada portal respondeu e cada recurso foi baixado numa rodada; regra com fonte em falha fica "não avaliada", nunca avaliada pela metade. |

## Como é uma regra

```
schema_version: "1.0"
rule_version: "0.3.0"
origin: cross_reference
description:  {language, title, text, justification, exceptions, examples}
sources:      {name: {portal, dataset, resource, archive, file, columns}}
check:        {template, parameters, where, timeline}
```

O nome do arquivo é o identificador da regra. [`schema/rule-v1.schema.json`](schema/rule-v1.schema.json)
é o contrato do formato, um arquivo para todas as regras; `python main.py validate` confere o esquema
e se toda coluna usada pela verificação está declarada. O manual de regras do repositório principal
explica cada campo.

## Como funciona uma rodada

[`.github/workflows/layer2.yml`](.github/workflows/layer2.yml) roda toda quarta-feira às 04:30 UTC (ou
manualmente). O job **evaluate**, com token só de leitura, baixa cada recurso CKAN uma vez (não importa
quantas regras o usem), registra se cada portal e recurso estava disponível, lê só as colunas
declaradas, avalia cada regra com DuckDB sem acesso externo e envia as saídas como artefato. O job
**publish** confere o artefato (`python main.py accept`: só os arquivos esperados, JSON válido, listas
só com números de registro, histórico anterior preservado) e faz o commit de `results/` e `docs/data/`.
Cada rodada registra também a velocidade de download deste portal e dos demais, e o tempo de cada etapa.

## Tratamento de dados e privacidade

Os arquivos são baixados durante a rodada e apagados ao final; no GitHub, o próprio runner é
descartado depois do job. O motor lê só as colunas que a regra declara. O que se publica são
contagens, números de registro, hashes SHA-256 e metadados publicados pelo CKAN, nunca um valor lido
dos portais. Regras sobre dados de saúde ou educação usam `exposure: counts`: publicam só contagens e
gráficos, nunca números de registro. Os datasets mantêm as licenças de seus publicadores, indicadas
com link no dashboard.

## Como rodar localmente

```
python -m pip install -r requirements.txt
python main.py validate
python -m pytest
python main.py run        # ensaio local: baixa as fontes, saídas em work/out
```

Rodada local é ensaio: resultados publicados vêm só do GitHub Actions.

## Organização do repositório

```
main.py            linha de comando (validate, run, accept)
src/               leitor, validador, modelos, download, motor, saídas, aceite
schema/            JSON Schema do formato de regra
rules/             um arquivo por regra, em subpastas
portal.json        o portal desta instância
docs/              dashboard (data/ é gravado pelas rodadas)
results/           resultados das rodadas
tests/             testes automáticos
```

## Licença e citação

Código sob a [Licença MIT](LICENSE). Metadados de citação em [`CITATION.cff`](CITATION.cff).
