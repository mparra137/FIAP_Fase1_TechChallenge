# 🩺 Tech Challenge Fase 1 — Diagnóstico de Diabetes

> Solução de Machine Learning para diagnóstico de diabetes desenvolvida como entrega do Tech Challenge Fase 1 do programa PosTech FIAP — IA para Devs.

---

## 📋 Descrição do Projeto

Este projeto implementa um sistema inteligente de suporte ao diagnóstico médico, focado na **classificação de diabetes** a partir de dados clínicos estruturados.

O pipeline completo inclui:
- Análise Exploratória de Dados (EDA)
- Pré-processamento e limpeza dos dados
- Treinamento e comparação de modelos de Machine Learning
- Avaliação com métricas clínicas (foco em Recall)
- Interpretabilidade com Feature Importance e SHAP

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

- Python 3.11+
- pip

---

## 🔍 Interpretabilidade

As features mais relevantes para o diagnóstico, segundo SHAP e Feature Importance:

1. **Glucose** — maior preditor de diabetes (SHAP médio: 0.9498)
2. **BMI** — segundo fator mais relevante (SHAP médio: 0.6511)
3. **Pregnancies** — terceiro fator (SHAP médio: 0.4182)

---

## ⚠️ Aviso Clínico

Este modelo é uma **ferramenta de triagem e apoio**, não um sistema de diagnóstico definitivo. O(a) médico(a) deve sempre ter a palavra final no diagnóstico clínico.

---

## 🛠️ Tecnologias Utilizadas

- Python 3.11
- pandas, numpy
- scikit-learn
- matplotlib, seaborn
- shap
- jupyter