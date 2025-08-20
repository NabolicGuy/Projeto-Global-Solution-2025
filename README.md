# 🌧️ Global Solution 2025 — Enchentes: como Data Science pode ajudar

Projeto aplicado que usa **ciência de dados** para **estimar risco de enchentes** e apoiar **resposta rápida**. O fluxo combina:
1) **Tratamento + modelagem** em Python (`GS2025.ipynb`)
2) **Visualização executiva** em Power BI (tendências, hotspots, impacto)

> **Objetivo:** transformar dados ambientais e socioeconômicos em **alertas acionáveis** para reduzir perdas humanas e materiais.

---

## 🔬 O que foi feito no notebook (`GS2025.ipynb`)

### 1) EDA e qualidade dos dados
- Inspeção de **tipos, nulos e duplicados**; amostras e `describe()`.
- **Distribuições e correlações** (heatmap) para entender relações entre variáveis.
- Gráficos de **contagem por região vs. risco** (entender hotspots).

### 2) Features e target
- **Variáveis usadas:**  
  `chuva_mm`, `nivel_rio_m`, `previsao_temp_c`, `umidade_%`, `idh`, `populacao`, `regiao`.
- **Target:** `risco_enchente` (0/1).
- **Codificação:** `regiao` com `LabelEncoder` (modelo árvore não exige padronização).
- **Balanceamento:** `class_weight='balanced'` no classificador.

### 3) Modelo e avaliação
- **Modelo:** `RandomForestClassifier` (robusto a não linearidades e outliers).
- **Split:** `train_test_split(..., stratify=y, test_size=0.2, random_state=42)`.
- **Métricas:** `classification_report` (precisão, recall, f1) e **matriz de confusão**.
- **Interpretabilidade:** gráfico de **importância de variáveis**.

### 4) Geração de alertas (Early Warning)
- Probabilidades via `predict_proba`.
- **Regra de decisão:** alerta quando **P(risco)=classe_1 ≥ 0.70** (threshold conservador para reduzir falsos positivos).
- **Saída:** tabela de alertas com `data`, `regiao`, `chuva_mm`, `nivel_rio_m`, `prob_risco` e **mensagem de ação imediata**.
- **Export:** `alertas_gerados.csv` (útil para integração com canais operacionais).

> **Stack:** Python (Pandas, NumPy, Scikit-learn), Seaborn/Matplotlib, Jupyter/Colab.

---

## 📊 Dashboard (Power BI)
- **KPIs**: incidência de risco, ocorrências por período, severidade/impacto estimado.
- **Segmentações**: por **região**, clima (chuva/umidade/temperatura) e perfis socioeconômicos (ex.: **IDH, população**).
- **Tendência temporal**: evolução de risco vs. variáveis hidrometeorológicas.
- **Exploração**: filtros interativos para priorizar **hotspots** e janelas críticas.

👉 **Acesse o dashboard público:**  
**https://app.powerbi.com/view?r=eyJrIjoiNDVjN2NmNTktMmE5ZC00NWFhLWI3ZTUtYzIxZTI5YTNlOWZjIiwidCI6IjExZGJiZmUyLTg5YjgtNDU0OS1iZTEwLWNlYzM2NGU1OTU1MSIsImMiOjR9**
