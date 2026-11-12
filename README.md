# stats-foundations

Fundamentos de estatística aplicada a **marketing data science**: cinco notebooks que ligam cada
conceito estatístico a uma decisão real de tráfego pago.

Sou gestor de tráfego (Meta Ads / Google Ads) e desenvolvedor. O objetivo do repositório não é
"aprender estatística do zero", e sim **dar nome técnico e método** às métricas que uso no dia a dia:
conversão, cliques, receita, testes A/B, intervalos de confiança. Todos os dados são sintéticos,
gerados com semente fixa, então qualquer pessoa reproduz os mesmos números.

> **English summary.** Five notebooks on applied statistics for marketing analytics: distributions
> behind campaign metrics, confidence intervals and hypothesis tests for A/B decisions, statistical
> power and sample size, multiple-testing corrections, bootstrap, and why correlation is not causation
> (confounding demo). Notebooks are written in Portuguese; data is synthetic and reproducible.

## Notebooks

| Notebook | Tema | Status |
|---|---|---|
| [`01-distribuicoes-marketing.ipynb`](01-distribuicoes-marketing.ipynb) | Três distribuições aplicadas a métricas reais de campanha: **Bernoulli → conversão**, **Poisson → cliques/eventos**, **log-normal → receita por cliente** | ✅ |
| [`02-intervalos-confianca-teste-hipotese.ipynb`](02-intervalos-confianca-teste-hipotese.ipynb) | **Intervalo de confiança** (Wilson) da taxa de conversão e por que ele supera o p-valor isolado; **teste de hipótese** de duas proporções (o A/B); ponte IC ↔ teste e visão **bayesiana** P(B>A) | ✅ |
| [`03-poder-amostra-multiplos-testes.ipynb`](03-poder-amostra-multiplos-testes.ipynb) | **Poder estatístico** e curvas de poder; **tamanho mínimo de amostra** (a conta por trás do planejamento de teste); **correção para múltiplos testes** (Bonferroni e Benjamini-Hochberg) e a armadilha dos ~40% de falso positivo | ✅ |
| [`04-bootstrap-intervalos-reamostragem.ipynb`](04-bootstrap-intervalos-reamostragem.ipynb) | **Bootstrap**: intervalos de confiança por reamostragem para *qualquer* métrica sem fórmula — ticket **mediano** (receita log-normal), e a **diferença** A/B | ✅ |
| [`05-correlacao-regressao-causalidade.ipynb`](05-correlacao-regressao-causalidade.ipynb) | **Correlação** (Pearson/Spearman) e **regressão linear**; demonstração de **confundidor** (gasto×receita) mostrando por que **correlação ≠ causação** — ponte para inferência causal | ✅ |

## O que cada notebook responde

- **01** — Minha conversão caiu de 9% para 7% com 80 leads. É queda real ou ruído?
- **02** — A variação B ganhou da A. Com que margem de erro, e qual a chance de B ser de fato melhor?
- **03** — Quantos leads preciso antes de subir o teste? E por que olhar 10 métricas gera ~40% de falso positivo?
- **04** — Como dar intervalo de confiança para ticket mediano ou ROAS, que não têm fórmula pronta?
- **05** — Gasto e receita sobem juntos. Quanto disso é efeito do anúncio e quanto é confundidor?

## Stack

- **Python 3.11+** gerenciado via [`uv`](https://docs.astral.sh/uv/)
- `numpy`, `pandas`, `scipy` — geração e análise de dados
- `matplotlib` — visualização
- `jupyterlab` / `ipykernel` — notebooks

## Como rodar

Pré-requisito: ter o [`uv`](https://docs.astral.sh/uv/getting-started/installation/) instalado.

```bash
# 1. Instalar as dependências e criar o ambiente (.venv) automaticamente
uv sync

# 2a. Abrir o JupyterLab
uv run jupyter lab

# 2b. OU, no VS Code: abra o .ipynb e selecione o kernel do .venv deste projeto
#     (Python 3.11 — caminho .venv/Scripts/python.exe)
```

O `uv` lê o `pyproject.toml` + `uv.lock` e reconstrói exatamente o mesmo ambiente em qualquer máquina.

## Estrutura

```text
stats-foundations/
├── 01-distribuicoes-marketing.ipynb
├── 02-intervalos-confianca-teste-hipotese.ipynb
├── 03-poder-amostra-multiplos-testes.ipynb
├── 04-bootstrap-intervalos-reamostragem.ipynb
├── 05-correlacao-regressao-causalidade.ipynb
├── pyproject.toml      # dependências (fonte da verdade)
├── uv.lock             # versões travadas (reprodutibilidade)
├── .python-version     # Python 3.11
└── README.md
```

## Por que distribuições importam para marketing

Toda métrica de campanha é uma variável aleatória. Saber **qual distribuição a gera** é o que
permite (a) construir intervalos de confiança corretos, (b) dimensionar testes A/B com poder
adequado e (c) não confundir ruído estatístico com efeito real. O notebook 01 estabelece essa base
ligando cada distribuição a uma métrica concreta de tráfego pago.

## Projeto relacionado

[`ab-test-simulado`](https://github.com/ghitflux/ab-test-simulado) aplica estes fundamentos num caso
completo: planejamento de amostra, análise, correção de múltiplas métricas e relatório executivo.

---

Hélcio Venâncio · [github.com/ghitflux](https://github.com/ghitflux) · Licença MIT

## Como este estudo foi feito

Este estudo foi construído com assistência de IA (Claude Code, da Anthropic), usada como par de programação.
Declaro a divisão do trabalho porque ela importa para quem avalia:

- **Meu:** o contexto de negócio (as perguntas são as que aparecem no dia a dia de quem gere mídia paga: a queda foi real ou ruído? quantos leads o teste precisa?), o estudo de cada conceito, a leitura crítica dos resultados e a decisão do que publicar e do que declarar como limitação.
- **Com o assistente:** a escolha do método, a implementação do código, dos testes e dos gráficos, e a redação,
  que revisei.
- **Como conferir:** os notebooks rodam do início ao fim e regeram todas as tabelas e figuras; os dados são sintéticos, com semente fixa.

É o mesmo jeito que trabalho nos sistemas que entrego: a IA acelera a implementação, e a responsabilidade pelo que
está escrito aqui é minha.

*In English: built with AI assistance (Claude Code) as a pair programmer. Direction, business context, critical
review of the results and the decision of what to publish are mine; method choice, implementation and writing were
done with the assistant and reviewed by me.*
