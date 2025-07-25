# Análise de Sentimentos em Textos de Redes Sociais

## 🎯 Objetivo do Projeto

Este projeto tem como objetivo desenvolver um modelo de Machine Learning capaz de classificar o sentimento de textos curtos (semelhantes a posts de redes sociais) em três categorias: **Positivo**, **Negativo** e **Neutro**.

O ciclo de vida completo do projeto foi explorado, desde a análise e limpeza dos dados, passando pelo treinamento e otimização de diferentes modelos, até a criação de uma ferramenta funcional para realizar predições em tempo real.

## 📂 Estrutura do Repositório

```
.
├── data
│   ├── raw/
│   │   └── sentimentdataset.csv       # Dataset original
│   └── processed/
│       └── sentimentdataset_tratado_v2.csv # Dataset limpo e enriquecido
├── modelos_salvos
│   └── modelo_final_otimizado.joblib  # Modelo campeão salvo
├── notebooks
│   ├── 01_analise_exploratoria.ipynb  # Análise, limpeza e visualização dos dados
│   ├── 02_modelagem_comparativa.ipynb # Treinamento inicial (Logistic Regression vs. Random Forest)
│   ├── 03_otimizacao_de_modelos.ipynb # Otimização do modelo com balanceamento de classes
│   └── 04_predicoes_finais.ipynb      # Uso do modelo para predições interativas
└── README.md                          # Este arquivo
```

## 🛠️ Metodologia

O projeto foi dividido em quatro notebooks principais, seguindo um fluxo de trabalho lógico:

### 1. Análise Exploratória de Dados (`01_analise_exploratoria.ipynb`)
- **Limpeza Inicial:** Remoção de colunas desnecessárias e tratamento de tipos de dados.
- **Simplificação de Sentimentos:** Agrupamento de dezenas de sentimentos específicos em três categorias principais (Positivo, Negativo, Neutro).
- **Visualização:**
  - Análise da distribuição de classes, revelando um dataset levemente desbalanceado, com predominância de sentimentos positivos.
  - Análise de engajamento (Likes e Retweets), mostrando que posts neutros e positivos geravam mais interação.
  - Criação de Nuvens de Palavras, que ajudaram a identificar ruídos no texto (como a palavra "like").
  - Análise temporal, mostrando picos de atividade no início da tarde e da noite.

### 2. Modelagem Inicial (`02_modelagem_comparativa.ipynb`)
- **Pré-processamento de Texto:** Implementação de uma pipeline de limpeza robusta com conversão para minúsculas, remoção de URLs e pontuações, uso de *stopwords* e **lematização**.
- **Comparação de Modelos:** Treinamento e avaliação de dois modelos base: `Regressão Logística` e `Random Forest`.
- **Diagnóstico:** Ambos os modelos apresentaram acurácia baixa (~62%) e um `recall` muito fraco para as classes minoritárias (Negativo e Neutro), indicando um comportamento "preguiçoso" devido ao desbalanceamento dos dados.

### 3. Otimização do Modelo (`03_otimizacao_de_modelos.ipynb`)
- **Técnica de Otimização:** A estratégia de `class_weight='balanced'` foi aplicada aos modelos para penalizar erros nas classes minoritárias.
- **Resultados:** A **Regressão Logística** demonstrou uma melhora espetacular:
  - A acurácia geral saltou de **62% para 74%**.
  - O `recall` da classe "Negativo" aumentou de 0.25 para **0.72** (+188%).
  - O modelo se tornou muito mais justo e preditivo para todas as classes.

### 4. Predições Finais (`04_predicoes_finais.ipynb`)
- **Aplicação Prática:** O melhor modelo (`Regressão Logística Otimizada`) foi carregado para realizar predições.
- **Ferramenta Interativa:** Foi criada uma interface simples no notebook para que o usuário possa inserir frases em inglês e receber a classificação de sentimento em tempo real.

## 📊 Resultados Finais

O modelo campeão, uma **Regressão Logística com `class_weight='balanced'`**, alcançou uma **acurácia de 74%** no conjunto de teste. Mais importante que o valor absoluto, o modelo final demonstrou um bom equilíbrio entre `precision` e `recall` para todas as três classes, tornando-o uma ferramenta confiável e útil.

| Classe | Precision | Recall | F1-Score |
|---|---|---|---|
| **Negativo** | 0.74 | 0.72 | 0.73 |
| **Neutro** | 0.69 | 0.55 | 0.61 |
| **Positivo** | 0.77 | 0.87 | 0.82 |

## 🚀 Como Executar o Projeto

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/statvin/analise-sentimentos.git
    cd analise-sentimentos
    ```

2.  **Crie um ambiente virtual (recomendado):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```

3.  **Instale as dependências:**
    (Recomenda-se criar um arquivo `requirements.txt` com as bibliotecas)
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn nltk joblib jupyter
    ```

4.  **Execute os notebooks:**
    Inicie o Jupyter Lab ou Notebook e execute os arquivos na ordem numérica para reproduzir todo o processo.
    ```bash
    jupyter lab
    ```

## 💻 Tecnologias Utilizadas

- Python 3.12.6
- Pandas e NumPy para manipulação de dados
- Matplotlib e Seaborn para visualização
- NLTK para pré-processamento de texto
- Scikit-learn para modelagem e avaliação de Machine Learning
- Jupyter Notebooks como ambiente de desenvolvimento

---
*Autor: Vinícius Ramos*
