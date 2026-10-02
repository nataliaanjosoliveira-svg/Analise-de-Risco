# 🛡️ Análise de Risco & Detecção de Anomalias em Transações Financeiras

Este projeto simula um pipeline completo de engenharia de dados, regras de negócio antifraude e **Machine Learning (Isolation Forest)** para identificação de transações suspeitas e geração automatizada de relatórios executivos em PDF.

---

## 📊 Visão Geral do Projeto

O objetivo é combinar **regras de negócio baseadas em heurísticas** (score de risco acumulado por valor, horário e status) com **Modelos Não Supervisionados (Machine Learning)** para detectar desvios comportamentais e padrões atípicos de transação.

### 🛠️ Principais Recursos
1. **Geração e Tratamento de Dados:** Simulação realista de transações financeiras com distribuições exponenciais de valores e variáveis categóricas.
2. **Motor de Regras (Rule-Based Risk Score):** Atribuição dinâmica de score com base em faixas de valor, horários críticos (madrugada) e recusas prévias.
3. **Análise de Desvio Comportamental:** Comparação de transações atípicas em relação ao histórico médio individual de cada cliente.
4. **Machine Learning (Isolation Forest):** Algoritmo de detecção de anomalias multivariado para isolamento de padrões fora do curva sem necessidade de rótulos prévios.
5. **Geração Automatizada de PDF:** Exportação de relatório corporativo executivo formatado via HTML/CSS e `WeasyPrint`.

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
* Python 3.9+
* Dependências do sistema Linux/Ubuntu para o `weasyprint` (se for rodar localmente):
  ```bash
  sudo apt-get install libpango-1.0-0 libpangoft2-1.0-0