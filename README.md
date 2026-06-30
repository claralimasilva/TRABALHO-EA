# CVLI, vulnerabilidade socioeconômica e facções criminosas em Fortaleza

Análise estatística da relação entre **Crimes Violentos Letais e Intencionais (CVLI)**, indicadores de vulnerabilidade social (IDH de 2010 e renda média de 2022) e presença documentada de facções criminosas nas **Áreas Integradas de Segurança (AIS)** de Fortaleza.

**Autores:** Arthur Thomé Costa, Clara Lima Silva, Mateus Rodrigues da Silva, Miguel de Lima Amaral.

Trabalho de **Estatística Aplicada** — análise reproduzível no notebook [`Trabalho de Estatistica Aplicada.ipynb`](Trabalho%20de%20Estatistica%20Aplicada.ipynb).

---

## Sobre o projeto

A violência letal em Fortaleza se distribui de forma desigual no território urbano, concentrando-se em áreas de menor desenvolvimento humano e menor renda. Paralelamente, há documentação de domínios territoriais por organizações criminosas (Comando Vermelho, Guardiões do Estado, Terceiro Comando Puro) em bairros periféricos.

Este repositório integra dados oficiais de CVLI (SSPDS/CE), indicadores censitários e uma codificação qualitativa de presença de facções para responder:

> **Qual a relação entre CVLI, vulnerabilidade socioeconômica (IDH e renda) e presença de facções criminosas nas AIS de Fortaleza?**

**Hipótese exploratória:** áreas com menor IDH, menor renda e maior presença documentada de facções tendem a concentrar taxas mais elevadas de CVLI.

**Escopo da análise:** 21.197 registros de CVLI em Fortaleza (2009–2025), agregados nas **10 AIS do município** (5, 6, 8, 16, 17, 18, 19, 20, 21 e 22 — cobertura integral conforme Portaria 34/2026; sem recorte analítico), integrados a dados de população, IDH, renda e facções em 34 bairros codificados.

---

## Estrutura do repositório

```
.
├── Trabalho de Estatistica Aplicada.ipynb   # Notebook principal (análise completa)
├── requirements.txt                         # Dependências Python
├── dados/                                   # Bases de dados
│   ├── CVLI_2009-a-2025.xlsx                # CVLI por AIS (SSPDS/CE)
│   ├── populacao_por_bairro.xlsx            # População por bairro (Censo 2010)
│   ├── idh_por_bairro.xlsx                  # IDH por bairro (Censo 2010)
│   ├── renda_por_bairro_2022.csv            # Renda média por bairro (IPECE/IBGE 2022)
│   ├── ais_bairros.csv                      # Mapeamento bairro ↔ AIS (Portaria 34/2026)
│   ├── faccoes_bairros.xlsx                 # Codificação de facções por bairro
│   ├── faccoes_bairros.csv                  # Versão CSV da codificação
│   └── ipece_informe_272.pdf                # Informe IPECE nº 272 (referência)
├── figuras/                                 # Gráficos gerados pela análise
│   ├── grafico_01_serie_temporal_cvli.png   # Série temporal 2009–2025
│   ├── grafico_02_taxa_cvli_por_ais.png     # Taxa de CVLI por AIS em Fortaleza (10 AIS)
│   ├── grafico_03_idh_vs_taxa_cvli.png      # Dispersão IDH × taxa CVLI
│   ├── grafico_03b_renda_vs_taxa_cvli.png   # Dispersão renda × taxa CVLI
│   ├── grafico_04_boxplot_faccao.png        # Boxplot por presença de facção
│   ├── grafico_05_heatmap_correlacao.png    # Heatmap de correlações de Spearman
│   └── grafico_06_meio_empregado.png        # Meio empregado nas AIS com facção
├── Relatorio_Estatistica_Aplicada.md        # Relatório acadêmico completo
└── Relatorio_Estatistica_Aplicada.pdf       # Versão PDF do relatório
```

---

## Como executar

### Pré-requisitos

- Python 3.10 ou superior
- Jupyter Notebook ou JupyterLab

### Instalação

```bash
# Clone o repositório e entre na pasta do projeto
cd "TRABALHO EA"

# Crie e ative um ambiente virtual (recomendado)
python -m venv .venv
source .venv/bin/activate   # Linux/macOS
# .venv\Scripts\activate    # Windows

# Instale as dependências
pip install -r requirements.txt
```

**Dependências principais:** `pandas`, `openpyxl`, `matplotlib`, `seaborn`, `scipy`, `jupyter`.

### Rodando o notebook

```bash
jupyter notebook "Trabalho de Estatistica Aplicada.ipynb"
```

Ou abra o arquivo diretamente no VS Code / Cursor com extensão Jupyter.

> **Nota:** os dados em `dados/` devem estar presentes antes da execução. O notebook lê os arquivos a partir de `DATA_DIR = Path("dados")`.

---

## Principais resultados

### Perfil dos registros (Fortaleza, n = 21.197)

| Variável | Categoria predominante | Frequência |
|----------|------------------------|------------|
| Gênero | Masculino | 19.756 (93,2%) |
| Meio empregado | Arma de fogo | 18.900 (89,2%) |
| Natureza | Homicídio doloso | 20.506 (96,7%) |

### Indicadores por AIS (2009–2025)

| AIS | População | IDH (2010) | Renda média 2022 (R$) | CVLI total | Taxa /100 mil | Facção |
|-----|-----------|------------|------------------------|------------|---------------|--------|
| 16 | 256.096 | 0,221 | 1.914 | 3.151 | **1.230,4** | Sim (CV) |
| 17 | 246.309 | 0,202 | 1.554 | 2.796 | **1.135,2** | Sim (CV) |
| 20 | 245.531 | 0,250 | 1.695 | 2.426 | **988,1** | Sim (CV) |
| 19 | 285.064 | 0,329 | 3.212 | 2.702 | **947,9** | Sim (CV) |
| 21 | 295.202 | 0,248 | 1.945 | 2.728 | **924,1** | Sim (GDE/CV) |
| 5 | 154.782 | 0,437 | 3.099 | 1.200 | 775,3 | **Não** |
| 18 | 360.551 | 0,333 | 2.258 | 2.578 | 715,0 | Sim (CV) |
| 22 | 162.327 | 0,575 | 6.803 | 1.061 | 653,6 | Sim (CV) |
| 8 | 172.541 | 0,645 | 7.134 | 973 | 563,9 | Sim (CV) |
| 6 | 281.645 | 0,436 | 3.279 | 1.582 | 561,7 | Sim (CV/GDE) |

### Correlações (nível AIS, n = 10)

| Par de variáveis | Pearson | Spearman (ρ) |
|------------------|---------|--------------|
| IDH 2010 × taxa CVLI | −0,852 | **−0,855** |
| Renda 2022 × taxa CVLI | −0,697 | **−0,842** |
| IDH 2010 × Renda 2022 | — | **+0,903** |
| População × taxa CVLI | — | ≈ +0,10 |
| Presença de facção × taxa CVLI | — | ≈ +0,06 |

### Teste de Mann-Whitney (taxa CVLI: com vs. sem facção)

- **Resultado:** U = 5,0; **p = 0,5000** (não significativo)
- **Grupos:** 9 AIS com facção vs. 1 AIS sem facção (AIS 5 — Centro)
- **Medianas:** com facção ≈ 924/100 mil; sem facção ≈ 775/100 mil

### Síntese dos achados

1. **Concentração espacial:** as cinco AIS com maiores taxas (16, 17, 20, 19 e 21) ficam na periferia, com IDH entre 0,20 e 0,33 e renda entre as mais baixas.
2. **Vulnerabilidade e CVLI:** IDH e renda correlacionam-se fortemente e negativamente com a taxa de CVLI (Spearman ≈ −0,85 e ≈ −0,84).
3. **Facções:** 9 das 10 AIS possuem facção documentada; a diferença de medianas não é estatisticamente significativa (p ≈ 0,50), em razão do desbalanceamento dos grupos (9 vs. 1).
4. **Arma de fogo:** nas nove AIS com facção, cerca de **90%** dos CVLIs envolvem arma de fogo (~20 mil registros).
5. **Exceções:** a **AIS 5** (Centro) tem taxa elevada (775/100 mil) sem registro de facção; a **AIS 6** tem facção, mas taxa relativamente menor (562/100 mil).

> **Atenção:** correlação não implica causalidade. Descompassos temporais (IDH 2010, renda 2022, CVLI até 2025), mudanças nas fronteiras das AIS e possíveis vieses de registro (ex.: queda abrupta em 2019, com 654 casos) limitam inferências causais.

---

## Visualizações

### Série temporal de CVLI (2009–2025)

Crescimento até o pico de 2014 (2.002 casos), queda acentuada em 2019 (654 casos) e estabilização posterior entre 700 e 1.250 casos anuais.

![CVLI em Fortaleza por ano (2009–2025)](figuras/grafico_01_serie_temporal_cvli.png)

### Taxa de CVLI por AIS em Fortaleza

Gráfico com as **10 AIS do município** (todas as unidades presentes na base da SSPDS). Maiores taxas na AIS 16 (~1.230/100 mil), AIS 17 (~1.135/100 mil) e AIS 20 (~988/100 mil). A AIS 5 destaca-se com taxa elevada (~775/100 mil) sem registro de facção.

![Taxa de CVLI por AIS em Fortaleza](figuras/grafico_02_taxa_cvli_por_ais.png)

### IDH × taxa de CVLI

Associação visual entre menor IDH e maior taxa de CVLI (Pearson ≈ −0,85; Spearman ≈ −0,85).

![IDH × Taxa de CVLI por AIS](figuras/grafico_03_idh_vs_taxa_cvli.png)

### Renda média 2022 × taxa de CVLI

Padrão semelhante ao IDH: violência concentrada nas AIS de menor renda (Spearman ≈ −0,84).

![Renda média 2022 × Taxa de CVLI por AIS](figuras/grafico_03b_renda_vs_taxa_cvli.png)

### Taxa de CVLI por presença de facção

Mediana maior nas AIS com facção (≈ 924/100 mil) do que na AIS 5 sem facção (≈ 775/100 mil), porém sem significância estatística (p ≈ 0,50).

![Distribuição da taxa de CVLI por presença de facção](figuras/grafico_04_boxplot_faccao.png)

### Matriz de correlação de Spearman

Correlações fortemente negativas entre renda/IDH e taxa de CVLI; correlação fraca entre presença de facção e taxa (ρ ≈ +0,06).

![Correlação de Spearman entre variáveis (nível AIS)](figuras/grafico_05_heatmap_correlacao.png)

### Meio empregado nas AIS com facção

Predomínio de arma de fogo (~90% dos CVLIs) nas nove AIS com facção documentada.

![CVLI por meio empregado nas AIS com facção documentada](figuras/grafico_06_meio_empregado.png)

---

## Relatório completo

Para a versão acadêmica com metodologia detalhada, discussão e limitações:

- [Relatorio_Estatistica_Aplicada.md](Relatorio_Estatistica_Aplicada.md) — relatório em Markdown
- [Relatorio_Estatistica_Aplicada.pdf](Relatorio_Estatistica_Aplicada.pdf) — relatório em PDF

---

## Referências

- SSPDS/CE — [CVLI 2009–2025](https://www.sspds.ce.gov.br/)
- Fortaleza Dados Abertos — [IDH e dados demográficos por bairro](https://dados.fortaleza.ce.gov.br/)
- IPECE — [Informe nº 272 — Renda média por bairro (Censo 2022)](https://www.ipece.ce.gov.br/wp-content/uploads/sites/45/2025/08/ipece_informe_272_05_ago2025.pdf)
- PNUD — [Radar IDHM 2024](https://www.undp.org/pt/brazil/publications/radar-idhm-evolucao-do-idhm-e-de-seus-componentes-periodo-de-2012-2024)
- SUPESP/SSPDS — Áreas Integradas de Segurança (AIS), Portaria 34/2026
- IBGE — Censo Demográfico 2010 e 2022
