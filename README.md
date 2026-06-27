# 🩺 Tech Challenge Fase 1 — Diagnóstico de Diabetes

> Solução de Machine Learning para diagnóstico de diabetes desenvolvida como entrega do Tech Challenge Fase 1 do programa PosTech FIAP — IA para Devs.

---

## 📋 Descrição do Projeto

O objetivo desse projeto é implementar um sistema inteligente de suporte ao diagnóstico médico, focado na **classificação de diabetes** a partir de dados clínicos estruturados.

O pipeline completo inclui:
- Análise Exploratória de Dados (EDA)
- Pré-processamento e limpeza dos dados
- Treinamento e comparação de modelos de Machine Learning
- Avaliação com métricas clínicas (foco em Recall) 
- Interpretabilidade com Feature Importance e SHAP

>*Por que Recall?*

>*Em aplicações médicas, falsos negativos são mais críticos que falsos positivos, pois um paciente doente classificado como saudável pode deixar de receber tratamento. Por isso, o modelo foi otimizado priorizando Recall.*
---

## 🗃️ Dataset

**Pima Indians Diabetes Dataset**
- Fonte: [Kaggle — mathchi/diabetes-data-set](https://www.kaggle.com/datasets/mathchi/diabetes-data-set/data)
- 768 pacientes, 8 features clínicas + 1 variável alvo (`Outcome`)
- O dataset considera mulheres a partir de 21 anos de idade descendentes da etnia Pima Indian
- Features: `Pregnancies`, `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`, `DiabetesPedigreeFunction`, `Age`
- Alvo: `Outcome` (0 = sem diabetes, 1 = com diabetes)

---

## ⚙️ Pré-requisitos

- Python 3.11+ (Os modelos foram treinados utilizando Python 3.14)
- pip
- Jupyter notebook

---

## ▶️ Como executar

- Toda a análise, e execução foi feita utilizando Jupyter Notebook
- Para executar basta utilizar o comando Run All / Executar tudo do Jupyter Notebook
- O próprio notebook instala as dependências na primeira célula 

---
### 📁 Estrutura do projeto

```text
Challenge/
│
├── dataset/
│   └── diabetes.csv
│
├── graficos/
│   ├── roc_curve.png
│   ├── shap_summary.png
│   └── confusion_matrix.png
│
├── notebook/
│   └── Diabetes_case_KnnImputer.ipynb
│
└── README.md
```

---
### 📊 Gráficos

Destaco aqui alguns resultados obtidos no treinamento dos modelos

![Matriz de Confusão](/graficos/grafico_matrizes_confusao.png)

Curva ROC
![Curva ROC](/graficos/curva_roc.png)

Shap Summary Plot
![Shap Summary Plot](/graficos/shap_summary_plot.png)


- Os gráficos gerados durante as análises do notebook estão salvos na pasta gráficos, porém podem ser melhor visualizados no próprio notebook

---
### Fluxo do projeto

Dataset

↓

EDA

↓

Pré-processamento

↓

Train/Test Split

↓

StandardScaler

↓

KNNImputer

↓

Treinamento

↓

Avaliação

↓

SHAP

---

### 💡Resultados obtidos

Para os pacientes com diabetes, os resultados obtidos foram esses:

| Modelo | Recall | Precision | F1 |
| ------ | ------ |-----------| -- |
| KNN | 0.57 | 0.69 | 0.63 |
| SVM⭐| **0.72** | 0.57 | 0.64 |
| RandomForest| 0.57 | 0.66 | 0.61|

**O SVM apresentou o melhor equilíbrio entre recall e capacidade de generalização.**

---

## 🔍 Interpretabilidade

A interpretabilidade foi executada sob o modelo com melhor resultado: **Support Vector Machine**

Foi realizada utilizando duas abordagens complementares:
- Permutation Importance para avaliar a importância global das variáveis.
- SHAP para explicar tanto o comportamento global quanto previsões individuais.


As features mais relevantes para o diagnóstico, segundo SHAP e Feature Importance:

1. **Glucose** — maior preditor de diabetes
2. **BMI** — segundo fator mais relevante 
3. **DiabetesPedigreeFunction** e **Age** - Seguem como fatores intermediários

---

## ⚠️ Aviso Clínico

Este modelo é uma **ferramenta de triagem e apoio**, não um sistema de diagnóstico definitivo. O(a) médico(a) deve sempre ter a palavra final no diagnóstico clínico.

---

## 🛠️ Tecnologias Utilizadas

- Python 3.14
- pandas, numpy
- scikit-learn
- matplotlib, seaborn
- permutation_importance
- shap
- jupyter

## 🎯 Conclusões

Neste trabalho, foram desenvolvidos três modelos de classificação (K-Nearest Neighbors, Random Forest e Support Vector Machine) para prever a presença de diabetes a partir de variáveis clínicas como glucose (glicose), BMI (IMC), Age (idade), pregnancies (gestações).

**Achados principais:**

1. **Glucose** é consistentemente a feature mais importante — alto nível de glicose é o principal preditor de diabetes, alinhado com o conhecimento clínico
2. **BMI**, **Pregnancies** e **Age** aparecem como próximos fatores mais relevantes
3. **Insulin** não mostrou muita relevância para o modelo apesar de ter uma correlação relevante com **Glucose**, talvez devido a ter uma alta porcentagens de dados faltantes.
3. **BloodPressure** e **SkinThickness** têm baixa importância — podem ter pouco poder preditivo neste dataset
4. O SHAP elenca claramente o ranking de features mais importantes na predição do modelo.
4. O SHAP Waterfall mostra como interpretar a predição de um paciente individual, tornando o modelo auditável por profissionais de saúde

**Implicação clínica:**

O modelo pode ser usado como ferramenta de triagem, priorizando pacientes com glicose elevada, IMC alto e idade avançada para avaliação médica detalhada. A transparência dos valores SHAP permite que o(a) médico(a) entenda e questione cada predição, mantendo o controle clínico sobre o diagnóstico final.

**Limitações:**
1. **Dados ausentes disfarçados de zero:** colunas como insulina (49% dos registros), espessura da pele (29,6%) e pressão (4,6%) continham valores zero fisiologicamente impossíveis, que precisaram ser substituídos pela mediana. Essa imputação massiva, especialmente na insulina, reduz a confiabilidade dessa variável — fato confirmado pelo gráfico SHAP, onde a insulina aparece com baixo impacto nas previsões, possivelmente por causa da imputação e não por ausência real de relevância clínica.
2. **Tamanho da amostra:** apenas 768 pacientes, o que limita a capacidade de generalização do modelo para outras populações.
3. **Origem dos dados:** o dataset é composto exclusivamente por mulheres de uma etnia específica (Pima Indians), o que pode não representar bem outras populações.
4. **Desbalanceamento de classes:** 65% dos pacientes não têm diabetes contra 35% que têm, o que pode enviesar o modelo a favor da classe majoritária.

**Conclusão final:** O modelo de Support Vector Machine se mostrou mais adequado para este treinamento, priorizando a identificação de casos positivos (maior recall). Contudo, dada a natureza crítica de diagnósticos médicos e as limitações dos dados, o modelo deve ser tratado como uma ferramenta complementar de apoio à decisão clínica, não como substituto da avaliação médica.