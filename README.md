# 🛡️ Detecção de Anomalias & Classificação de Risco em Transações Financeiras

> **Solução de ponta a ponta que combina Regras de Negócio e Aprendizado de Máquina Não Supervisionado (Isolation Forest) para identificação precoce de comportamento suspeito e geração automatizada de relatórios executivos em PDF.**

---

## 🎯 O Problema de Negócio

Empresas e instituições financeiras processam milhares de transações diariamente. Avaliar manualmente cada transação é inviável, enquanto confiar **apenas em regras fixas** cria dois grandes problemas:

1. **Falsos Positivos Elevados:** Regras rígidas (ex: *bloquear tudo acima de R$ 500 de madrugada*) impactam negativamente a experiência de clientes legítimos.
2. **Ponto Cego para Padrões Complexos:** Fraudes atípicas e comportamentos anômalos multivariados passam despercebidos por regras condicionais simples.

## **A Solução**
Este projeto propõe uma **abordagem híbrida** que combina:
- **Rule-Based Engine (Motor de Regras):** Classificação imediata baseada em políticas operacionais de risco.
- **Machine Learning Não Supervisionado:** Detecção de anomalias com **Isolation Forest**, capaz de isolar pontos fora do padrão avaliando múltiplas variáveis simultaneamente, sem necessidade de dados previamente rotulados.
- **Relatório Automatizado (Data-to-Report):** Síntese automática dos resultados em um documento PDF executivo para tomada de decisão rápida pelas equipes de risco/operações.

---

## 🔬 O Que Foi Feito (Passo a Passo Técnico)

### 1. Modelagem e Engenharia de Dados
* **Geração da Base Transacional:** Criação de um dataset sintético ($N = 1.000$ transações) com variáveis de cliente, valor (distribuição exponencial realista), cidade, horário, dispositivo e status.
* **Perfis Comportamentais Históricos:** Agregação por cliente para calcular o valor médio histórico transacionado e o **desvio percentual relativo** de cada operação em relação ao comportamento padrão do usuário.

### 2. Motor de Regras (Score de Risco Estático)
Aplicação de regras condicionais cumulativas baseadas em limiares operacionais:
* **Regra 1 (Valor):** Transações acima de R$ 500 recebem +20 pontos; acima de R$ 1.000 somam +30 pontos adicionais.
* **Regra 2 (Janela Crítica):** Operações realizadas entre 00h e 05h somam +20 pontos.
* **Regra 3 (Status):** Transações previamente recusadas somam +20 pontos.
* **Faixas de Classificação:**
  * **Baixo Risco:** Score $\le 30$
  * **Médio Risco:** $31 \le \text{Score} \le 60$
  * **Alto Risco:** Score $> 60$

### 3. Detecção de Anomalias com Machine Learning
* **Algoritmo:** `IsolationForest` (Scikit-Learn).
* **Variáveis de Entrada (`features`):** `valor`, `hora`, `score_risco` e `desvio_percentual`.
* **Lógica do Modelo:** Isola anomalias construindo árvores de decisão aleatórias; observações com caminhos de isolamento mais curtos são classificadas como anômalias multivariadas.

### 4. Pipeline de Automação de Relatórios
* **Renderização Dinâmica:** Construção de um template HTML5/CSS3 estilizado com cartões de KPIs, tabela comparativa por nível de risco e chamadas executivas.
* **Exportação PDF:** Conversão automatizada via biblioteca `WeasyPrint` para gerar um arquivo PDF pronto para impressão ou envio executivo.

---

## 📈 Resultados e Insights Alcançados

| Métrica / Indicador | Resultado | Significado Operacional |
| :--- | :---: | :--- |
| **Volume Total Processado** | ~R$ 242.000,00 | Amostra representativa de $1.000$ transações |
| **Anomalias Detectadas (ML)** | **5,0%** | $50$ transações com alto grau de isolamento atípico |
| **Desvios Comportamentais (>100%)** | **~30%** | Operações que dobraram a média histórica individual do cliente |
| **Confronto ML x Regras** | **Complementar** | O algoritmo identificou transações anômalas mesmo dentro da faixa de "Baixo Risco" manual |

### Principais Ganhos:
* **Capacidade Preditiva Híbrida:** A IA captura anomalias sutis (ex: múltiplos desvios pequenos combinados com horários atípicos) que a regra manual isoladamente não pega.
* **Eficiência Operacional:** O relatório gerado automaticamente direciona a atenção dos analistas apenas para os $5\%$ de casos críticos.

---

## 🛠️ Tecnologias e Ferramentas

* **Linguagem:** Python 3.9+
* **Processamento de Dados:** Pandas, NumPy
* **Machine Learning:** Scikit-Learn (`IsolationForest`)
* **Geração de PDF e Estilização:** WeasyPrint, HTML5, CSS3
* **Ambiente de Desenvolvimento:** Google Colab / Jupyter Notebook

---

## 📂 Estrutura do Repositório

```text
├── .gitignore
├── README.md
├── requirements.txt
├── analise_risco_transacional.py    # Script completo do pipeline
└── Relatorio_Executivo_Risco.pdf    # Exemplo do PDF gerado automaticamente
