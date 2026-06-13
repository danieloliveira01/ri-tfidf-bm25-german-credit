# Sistema de Recuperação da Informação para Identificação de Perfis de Crédito Semelhantes

Autores:\
Daniel de Oliveira Silva \
Analissa Haga


Este projeto apresenta a implementação de um Sistema de Recuperação da Informação (SRI) aplicado à identificação de perfis semelhantes de clientes em bases de crédito. A proposta consiste em transformar registros tabulares em documentos textuais, permitindo a utilização de técnicas clássicas de Recuperação da Informação para localizar clientes com características próximas às de uma consulta fornecida.

O trabalho foi desenvolvido como atividade prática da disciplina de Recuperação da Informação e contempla a implementação de métodos de indexação, ranqueamento e avaliação amplamente utilizados na literatura da área.

---

## Objetivo

O objetivo deste projeto é avaliar a aplicação de técnicas de Recuperação da Informação em dados originalmente estruturados, utilizando o conjunto de dados German Credit Data.

Para isso, cada registro da base é convertido em um documento textual composto por pares atributo-valor. Em seguida, diferentes modelos de recuperação são utilizados para identificar perfis semelhantes aos perfis consultados.

Os modelos avaliados foram:

- TF-IDF (implementação manual)
- BM25 (modelo probabilístico)

---

## Dataset

Foi utilizado o conjunto de dados **German Credit Data**, amplamente empregado em pesquisas de análise de crédito e aprendizado de máquina.

A base contém aproximadamente 1.000 registros de clientes, incluindo atributos como:

- Idade
- Sexo
- Ocupação
- Tipo de moradia
- Conta corrente
- Conta poupança
- Finalidade do crédito

### Representação textual

Cada registro é convertido para um documento textual no formato:

```text
age_senior sex_male job_2 housing_own saving_unknown checking_little
```

Essa estratégia permite que algoritmos clássicos de Recuperação da Informação sejam aplicados diretamente sobre os dados.

---

## Pré-processamento

Durante a construção do corpus foram realizadas as seguintes etapas:

- Conversão para letras minúsculas;
- Tokenização dos documentos;
- Normalização dos atributos;
- Discretização da variável idade.

A idade foi agrupada em quatro faixas:

| Faixa | Intervalo |
|---------|---------|
| young | ≤ 25 anos |
| adult | 26 a 40 anos |
| middle | 41 a 60 anos |
| senior | > 60 anos |

Exemplo:

```text
age_67
```

torna-se:

```text
age_senior
```

Essa transformação reduz a dispersão do vocabulário e favorece a recuperação de perfis semelhantes.

---

## Modelo TF-IDF

O modelo vetorial foi implementado manualmente, sem o uso de bibliotecas prontas para cálculo de TF-IDF.

As etapas implementadas incluem:

1. Construção do vocabulário;
2. Cálculo da frequência dos termos (TF);
3. Cálculo da frequência inversa dos documentos (IDF);
4. Geração da matriz TF-IDF;
5. Cálculo da Similaridade do Cosseno;
6. Ranqueamento dos documentos.

O peso de cada termo é calculado por:

\[
TFIDF(t,d)=TF(t,d)\times IDF(t)
\]

onde:

\[
IDF(t)=\log\left(\frac{N}{1+DF(t)}\right)
\]

---

## Modelo BM25

Além do TF-IDF, foi implementada uma avaliação utilizando o modelo probabilístico BM25.

Parâmetros utilizados:

```text
k1 = 1.5
b  = 0.75
```

O BM25 foi empregado como método de comparação para avaliar o desempenho dos rankings gerados.

---

## Avaliação Experimental

A base foi dividida em:

- 900 documentos para o corpus;
- 100 documentos para consultas (queries).

A relevância foi definida com base no atributo **Purpose**, utilizado apenas durante a avaliação.

As métricas utilizadas foram:

- Precision@10 (P@10)
- Precision@20 (P@20)
- Precision@50 (P@50)
- Precision@100 (P@100)
- Mean Average Precision (MAP)

---

## Resultados

### TF-IDF

| Métrica | Resultado |
|----------|----------:|
| P@10 | 0.2720 |
| P@20 | 0.2595 |
| P@50 | 0.2520 |
| P@100 | 0.2472 |
| MAP | 0.2473 |

### BM25

| Métrica | Resultado |
|----------|----------:|
| P@10 | 0.2450 |
| P@20 | 0.2515 |
| P@50 | 0.2486 |
| P@100 | 0.2523 |
| MAP | 0.2460 |

### Comparação

| Métrica | TF-IDF | BM25 |
|----------|----------:|----------:|
| P@10 | **0.2720** | 0.2450 |
| P@20 | **0.2595** | 0.2515 |
| P@50 | **0.2520** | 0.2486 |
| P@100 | 0.2472 | **0.2523** |
| MAP | **0.2473** | 0.2460 |

Os resultados indicam desempenho semelhante entre os modelos, com ligeira vantagem do TF-IDF nas primeiras posições do ranking.

---

## Estrutura do Projeto

```text
.
├── trabalho_ri.ipynb
├── german_credit_data.csv
├── README.md
└── resultados/
```

---

## Tecnologias Utilizadas

- Python
- Google Colab
- NumPy
- Pandas
- Matplotlib
- NLTK
- Rank-BM25

---

## Como Executar

1. Clone o repositório:

```bash
git clone https://github.com/SEU-USUARIO/ri-tfidf-bm25-german-credit.git
```

2. Acesse a pasta:

```bash
cd ri-tfidf-bm25-german-credit
```

3. Abra o notebook no Google Colab ou Jupyter Notebook.

4. Execute as células em sequência.

---

## Artigo

Este código foi desenvolvido como parte do artigo:

**Aplicação de Técnicas de Recuperação da Informação para Identificação de Perfis Semelhantes em Bases de Crédito Utilizando TF-IDF e BM25**

---

## Autor

**Daniel de Oliveira Silva**

Curso Superior de Tecnologia em Ciência de Dados

Faculdade de Tecnologia (Fatec)

---

## Licença

Este projeto foi desenvolvido para fins acadêmicos e educacionais.