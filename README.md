# Tech Challenge — Fase 2

Projeto de Machine Learning para análise e classificação da qualidade de vinhos, desenvolvido como parte do Tech Challenge — Fase 2.

O repositório reúne a base utilizada, o notebook com a exploração e modelagem, as dependências do projeto e o material de apresentação em uma estrutura simples e direta.

## Objetivo

Desenvolver uma solução de Machine Learning para explorar os atributos físico-químicos dos vinhos e construir modelos capazes de classificar sua qualidade.

O trabalho contempla:

- análise exploratória dos dados;
- preparação da base para modelagem;
- treinamento e avaliação de modelos de classificação;
- comparação dos resultados obtidos;
- documentação do processo em notebook;
- apresentação dos principais resultados e conclusões.

## Tecnologias utilizadas

- Python
- Pandas
- scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook

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

## Dados

A base utilizada no projeto está disponível em [`data/WineQT.csv`](data/WineQT.csv).

Ela contém as variáveis utilizadas durante a análise exploratória e a etapa de modelagem de classificação da qualidade dos vinhos.

## Notebook

A análise completa está concentrada no notebook [`notebooks/tech_challenge_fase_2.ipynb`](notebooks/tech_challenge_fase_2.ipynb).

O notebook reúne o fluxo de trabalho do projeto, desde a leitura e exploração dos dados até as etapas de preparação, treinamento e avaliação dos modelos.

## Como executar

Clone o repositório e, na pasta do projeto, crie um ambiente virtual:

```bash
python -m venv .venv
```

Ative o ambiente virtual e instale as dependências:

```bash
pip install -r requirements.txt
```

Em seguida, inicie o Jupyter Notebook:

```bash
jupyter notebook
```

Abra o arquivo:

```text
notebooks/tech_challenge_fase_2.ipynb
```

## Apresentação

O material utilizado na apresentação do Tech Challenge está disponível em [`docs/apresentacao.pdf`](docs/apresentacao.pdf).

## Artefatos do projeto

- [Dataset utilizado](data/WineQT.csv)
- [Notebook de análise e modelagem](notebooks/tech_challenge_fase_2.ipynb)
- [Apresentação do projeto](docs/apresentacao.pdf)
- [Dependências Python](requirements.txt)

## Organização

A estrutura foi mantida propositalmente enxuta: somente os artefatos efetivamente utilizados no projeto são versionados. Pastas vazias ou sem implementação associada foram removidas para facilitar a navegação e a leitura do repositório.

## Autor

Rodrigo Scalioni
