# 5LTEP-L2 · Instância Recife (experimento de controle)

[![Testes](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml/badge.svg)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/tests.yml) [![Camada 2](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer2-recife%2Fmain%2Fdocs%2Fdata%2Fstatus.pt.json)](https://github.com/lsp3cesarschool/5ltep-layer2-recife/actions/workflows/layer2.yml) [![Licença: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[English](README.md) · **Português**

**A Camada 2 do 5L-TEP (políticas semânticas) aplicada ao portal de dados abertos da Prefeitura do Recife: outra
instância do [5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2), montada pelo autor como
caso de controle do estudo do IBAMA.**

| Recurso | O que há lá |
|---|---|
| 📊 **Dashboard** | [lsp3cesarschool.github.io/5ltep-layer2-recife](https://lsp3cesarschool.github.io/5ltep-layer2-recife/?lang=pt): regras, sinais, saúde das fontes, histórico |
| 📏 **Regras** | [`rules/`](rules/): um arquivo por verificação, para acidentes de trânsito, contratos e aditivos, licenças ambientais, pesagem de resíduos e notificações de arboviroses (só contagens) |
| 🏛️ **Instância principal** | [5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2): IBAMA, e a documentação completa |
| 🔁 **Outro controle** | [5ltep-layer2-aneel](https://github.com/lsp3cesarschool/5ltep-layer2-aneel): o portal da ANEEL |

> **Estado: demonstração de pesquisa.** Este repositório não é operado, afiliado nem endossado por
> a Prefeitura do Recife; só lê dados abertos de portais CKAN. As regras são exemplos escritos pelo autor: um sinal
> é algo a revisar, nunca um veredito sobre os dados. Só são publicadas contagens e números de
> registro, nunca valores dos portais.

## O que muda em relação à instância principal

Só a configuração e as regras: [`portal.json`](portal.json) nomeia este portal, e [`rules/`](rules/)
traz as verificações escritas para os datasets dele. O motor, o formato das regras, o validador, o
dashboard e os workflows são o mesmo código do
[5ltep-layer2](https://github.com/lsp3cesarschool/5ltep-layer2) (d9ee325). Algumas regras
reutilizam uma verificação da instância do IBAMA sobre outras colunas, que é o reuso que o estudo mede.

## Como rodar

```
python -m pip install -r requirements.txt
python main.py validate
python main.py run        # ensaio local: baixa as fontes, saídas em work/out
```

## Licença e citação

Código sob a [Licença MIT](LICENSE). Metadados de citação em [`CITATION.cff`](CITATION.cff).
