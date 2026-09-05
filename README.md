# Tech Challenge — Fase 2

Projeto de Machine Learning para classificação da qualidade de vinhos a partir de características físico-químicas, desenvolvido como parte do Tech Challenge — Fase 2.

O trabalho percorre uma pipeline completa de Ciência de Dados: análise exploratória, preparação dos dados, engenharia de atributos, tratamento de outliers, treinamento de modelos de classificação e comparação das métricas de desempenho.

## Objetivo

Construir e avaliar modelos capazes de classificar os vinhos em duas categorias:

- **Alta qualidade:** nota `>= 7`;
- **Baixa/média qualidade:** nota `< 7`.

Além da performance preditiva, o estudo busca entender o impacto da engenharia de atributos e da remoção de outliers sobre diferentes algoritmos de Machine Learning.

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook

## Dados

A base utilizada está disponível em [`data/WineQT.csv`](data/WineQT.csv) e contém **1.143 registros**.

As variáveis representam características físico-químicas dos vinhos, incluindo:

```text
fixed acidity
volatile acidity
citric acid
residual sugar
chlorides
free sulfur dioxide
total sulfur dioxide
density
pH
sulphates
alcohol
quality
```

A variável `Id` é utilizada apenas como identificador e não participa da modelagem.

A variável alvo foi transformada em uma classificação binária para diferenciar vinhos com nota igual ou superior a 7 dos demais.

A base é desbalanceada: apenas **159 registros** pertencem à classe de alta qualidade. Esse aspecto foi considerado durante a modelagem e a interpretação das métricas.

## Metodologia

### 1. Análise exploratória

O notebook realiza uma análise inicial da base para compreender:

- distribuição das variáveis;
- estatísticas descritivas;
- presença de valores ausentes;
- possíveis outliers;
- correlações entre os atributos;
- distribuição da variável de qualidade;
- balanceamento da variável alvo.

### 2. Preparação dos dados

A variável `quality` é convertida para uma variável binária utilizada como alvo da classificação.

Os dados são separados em conjuntos de treinamento e teste utilizando:

```text
80% treino
20% teste
random_state = 42
stratify = variável alvo
```

O uso de divisão estratificada preserva aproximadamente a proporção entre as classes nos dois conjuntos.

### 3. Cenários experimentais

Foram avaliadas três versões da base:

1. **Base original**;
2. **Base com novas variáveis**, incorporando engenharia de atributos;
3. **Base com novas variáveis e tratamento de outliers**.

A decisão de avaliar os cenários com e sem remoção de outliers é especialmente relevante porque a classe positiva possui poucos exemplos e a exclusão de observações pode reduzir ainda mais a amostra disponível para aprendizado.

### 4. Modelos

Três algoritmos de classificação foram comparados:

- Decision Tree Classifier;
- Logistic Regression;
- Random Forest Classifier.

Cada algoritmo foi treinado nos três cenários de dados, resultando em **9 experimentos**.

O Random Forest foi configurado com `200` árvores, `class_weight='balanced'`, profundidade máxima de `10` e `random_state=42`.

## Resultados

As métricas utilizadas para comparar os modelos foram **Accuracy, Precision, Recall e F1-Score**.

| Modelo | Accuracy | Precision | Recall | F1-Score |
|---|---:|---:|---:|---:|
| Decision Tree | 0.8603 | 0.5000 | 0.6250 | 0.5556 |
| Decision Tree + Variáveis Novas | 0.8690 | 0.5250 | 0.6562 | 0.5833 |
| Decision Tree + Variáveis Novas sem Outliers | 0.8889 | 0.5625 | 0.6667 | 0.6102 |
| Logistic Regression | 0.7948 | 0.3729 | 0.6875 | 0.4835 |
| Logistic Regression + Variáveis Novas | 0.7904 | 0.3621 | 0.6562 | 0.4667 |
| Logistic Regression + Variáveis Novas sem Outliers | 0.8357 | 0.4286 | **0.7778** | 0.5526 |
| Random Forest | 0.9127 | 0.7308 | 0.5938 | 0.6552 |
| Random Forest + Variáveis Novas | 0.9127 | **0.7727** | 0.5312 | 0.6296 |
| **Random Forest + Variáveis Novas sem Outliers** | **0.9324** | 0.7600 | 0.7037 | **0.7308** |

## Melhor modelo

O melhor desempenho global foi obtido pelo **Random Forest com novas variáveis e remoção de outliers**.

Principais métricas:

```text
Accuracy:  93,24%
Precision: 76,00%
Recall:    70,37%
F1-Score:  0,7308
```

O modelo apresentou o melhor equilíbrio entre capacidade geral de classificação e identificação da classe minoritária, alcançando simultaneamente a maior acurácia e o maior F1-Score entre os cenários testados.

## Principais conclusões

A comparação dos experimentos evidencia três resultados importantes:

- **Random Forest apresentou o desempenho mais consistente**, superando Decision Tree e Logistic Regression na maior parte dos cenários.
- **Engenharia de atributos não trouxe ganhos uniformes.** No Random Forest, por exemplo, as novas variáveis aumentaram a precisão de `0,7308` para `0,7727`, mas reduziram o recall de `0,5938` para `0,5312`.
- **O tratamento de outliers teve impacto relevante.** Após a remoção dos valores discrepantes, os três algoritmos obtiveram seus melhores resultados dentro de suas respectivas famílias de experimentos.

A Logistic Regression com tratamento de outliers atingiu o maior **Recall** de todos os testes (`0,7778`), mostrando maior sensibilidade para identificar vinhos de alta qualidade. Porém, seu baixo nível de precisão resultou em F1-Score inferior ao Random Forest.

Já o Random Forest final apresentou um equilíbrio mais favorável entre **Precision (`0,7600`)** e **Recall (`0,7037`)**, justificando sua escolha como melhor solução do estudo.

## Considerações metodológicas

Como a classe de alta qualidade representa uma parcela pequena da base, a acurácia isoladamente não é suficiente para avaliar os modelos.

Por esse motivo, Precision, Recall e principalmente F1-Score são importantes para comparar os experimentos. Um modelo poderia obter alta acurácia simplesmente privilegiando a classe majoritária e ainda assim apresentar baixa capacidade de identificar os vinhos de alta qualidade.

Os resultados apresentados correspondem ao conjunto de dados e à divisão treino/teste adotados neste estudo. Não devem ser interpretados como garantia de desempenho em dados externos sem uma etapa adicional de validação.

## Notebook

Todo o fluxo analítico está disponível em:

[`notebooks/tech_challenge_fase_2.ipynb`](notebooks/tech_challenge_fase_2.ipynb)

O notebook contém:

- exploração dos dados;
- análise de distribuição e correlação;
- análise e tratamento de outliers;
- criação da variável alvo;
- engenharia de atributos;
- separação treino/teste;
- treinamento dos modelos;
- matrizes de confusão;
- cálculo das métricas;
- comparação dos experimentos;
- conclusão do estudo.

## Como executar

Clone o repositório e crie um ambiente virtual:

```bash
python -m venv .venv
```

Ative o ambiente e instale as dependências:

```bash
pip install -r requirements.txt
```

Em seguida, inicie o Jupyter Notebook:

```bash
jupyter notebook
```

Abra:

```text
notebooks/tech_challenge_fase_2.ipynb
```

## Apresentação

O material utilizado na apresentação do Tech Challenge está disponível em:

[`docs/apresentacao.pdf`](docs/apresentacao.pdf)

## Artefatos do projeto

- [Dataset utilizado](data/WineQT.csv)
- [Notebook de análise e modelagem](notebooks/tech_challenge_fase_2.ipynb)
- [Apresentação do projeto](docs/apresentacao.pdf)
- [Dependências Python](requirements.txt)

## Estrutura do repositório

```text
tech-challenge-fase-2/
├── README.md
├── .gitignore
├── requirements.txt
├── data/
│   └── WineQT.csv
├── notebooks/
│   └── tech_challenge_fase_2.ipynb
└── docs/
    └── apresentacao.pdf
```

## Autor

Rodrigo Scalioni
