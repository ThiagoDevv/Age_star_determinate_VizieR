# Predição de Idade Estelar utilizando Modelos de Regressão

Este repositório contém o desenvolvimento de um pipeline de Machine Learning focado na predição contínua da idade de estrelas. O projeto utiliza dados astrofísicos provenientes do catálogo VizieR para treinar, validar e otimizar algoritmos de regressão, mapeando a relação não-linear entre as propriedades estelares e seu estágio evolutivo.

## 🎯 Objetivo do Projeto
Desenvolver um modelo preditivo de alta precisão para estimar a idade estelar e, por meio de inferência algorítmica (Feature Importance), validar as variáveis astrofísicas de maior impacto na evolução estelar.

## 📊 Conjunto de Dados
Os dados foram extraídos do catálogo VizieR e contêm as seguintes *features* independentes (variáveis preditoras):
* `Mass`: Massa estelar.
* `logL`: Logaritmo da Luminosidade.
* `log.Teff`: Logaritmo da Temperatura Efetiva.
* `B-V`: Índice de Cor.
* `Vmag`: Magnitude Visual Absoluta/Aparente.
* **Variável Alvo (Target):** `Age` (Idade).

## ⚙️ Metodologia e Modelagem Predita

O projeto seguiu uma abordagem evolutiva na complexidade dos modelos de regressão, utilizando a métrica **RMSE (Root Mean Squared Error)** para avaliação de desempenho e controle de generalização. Os dados foram divididos em conjuntos de treino e teste (70/30) utilizando o `train_test_split`.

### 1. Modelo Paramétrico (Baseline)
* **Algoritmo:** Linear Regression
* **Desempenho (Teste RMSE):** `1.40`
* **Análise:** O erro elevado evidenciou que os pressupostos de linearidade não são adequados para representar a complexidade das relações físicas da evolução estelar.

### 2. Modelo Não-Paramétrico (Controle de Variância)
* **Algoritmo:** Decision Tree Regressor
* **Desempenho Inicial (Sem poda):** RMSE Treino `0.10` | RMSE Teste `0.72` (*Alto Overfitting*)
* **Otimização (Hyperparameter Tuning):** Após ajustar o hiperparâmetro `max_depth=7` para limitar o crescimento da árvore e forçar a generalização, o modelo alcançou uma performance mais robusta.
* **Desempenho Otimizado:** RMSE Treino `0.39` | RMSE Teste `0.68`

### 3. Modelo de Ensemble (Arquitetura Final)
* **Algoritmo:** Random Forest Regressor (`n_estimators=100`)
* **Desempenho Final:** RMSE Treino `0.19` | RMSE Teste `0.55`
* **Análise:** A agregação de múltiplas árvores reduziu drasticamente a variância do modelo isolado, atingindo o menor erro preditivo do projeto e estabilizando as predições para dados não vistos.

## 🔍 Extração de Insights: Importância das Variáveis (Feature Importance)

A abstração matemática do algoritmo Random Forest permitiu extrair o peso de cada variável na redução das impurezas dos nós (Feature Importance). Os resultados validam conceitos fundamentais da astrofísica:

| Variável | Importância (%) | Interpretação Física |
| :--- | :--- | :--- |
| **`Mass`** | 67.4% | Principal determinante da vida estelar. Dita a taxa de fusão nuclear. |
| **`logL`** | 16.5% | Indicador crucial do estágio evolutivo (ex: saída da Sequência Principal). |
| **`log.Teff`**| 13.9% | Mensuração de temperatura correlacionada à evolução no Diagrama HR. |
| **`B-V`** | 1.3% | Redundante, pois a variância já é capturada pelo `log.Teff`. |
| **`Vmag`** | 0.8% | Redundante em relação ao `logL`. |

*(Adicione aqui a imagem do gráfico gerado no projeto: `![Gráfico de Feature Importance](caminho_para_a_imagem.png)`)*

## 🛠️ Tecnologias e Bibliotecas Utilizadas
* **Linguagem:** Python 3
* **Manipulação de Dados:** `pandas`, `numpy`
* **Visualização:** `matplotlib`, `seaborn`
* **Machine Learning:** `scikit-learn` (`LinearRegression`, `DecisionTreeRegressor`, `RandomForestRegressor`, `train_test_split`, métricas de erro)
