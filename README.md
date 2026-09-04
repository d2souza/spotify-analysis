# 🎵 Análise de Sucesso Musical no Spotify — 2023

> **Quais fatores estão mais associados ao número de streams das músicas presentes no ranking do Spotify em 2023?**

Este projeto nasceu de uma curiosidade simples: **o que faz uma música alcançar milhões de reproduções?**

É a característica da música? Seu ritmo, energia ou dançabilidade? A presença em playlists? A exposição em diferentes plataformas? Ou uma combinação desses fatores?

Para investigar essa questão, realizei uma **Análise Exploratória de Dados (EDA)** utilizando uma base com músicas presentes no ranking do Spotify em 2023. O objetivo não foi apenas encontrar correlações, mas entender os dados, identificar padrões, questionar hipóteses e, principalmente, reconhecer os limites das conclusões.

---

## 🎯 Objetivo

O objetivo principal é explorar quais fatores apresentam maior associação com o número de **streams** das músicas presentes no ranking de 2023.

A análise foi organizada em três grandes dimensões:

* 🎧 **Características musicais** — energia, dançabilidade, valência, acústica, BPM e outras métricas;
* 📈 **Distribuição e presença em plataformas** — playlists e rankings do Spotify, Apple Music, Deezer e Shazam;
* 👤 **Artistas e lançamentos** — frequência de aparição no ranking e período de lançamento.

### Pergunta principal

> **Quais características estão mais associadas ao número de streams das músicas presentes no ranking de 2023?**

### Hipóteses investigadas

1. Características musicais apresentam associação relevante com o número de streams.
2. A presença em playlists está associada a um maior volume de streams.
3. Alguns artistas concentram uma parcela relevante das músicas presentes no ranking.
4. O período de lançamento apresenta diferenças no desempenho das faixas.

---

## 📊 Sobre os dados

A base utilizada contém informações sobre músicas presentes no ranking do Spotify em 2023.

Entre as variáveis disponíveis estão:

| Grupo                    | Exemplos                                                                         |
| ------------------------ | -------------------------------------------------------------------------------- |
| Identificação            | Música, artista e quantidade de artistas                                         |
| Lançamento               | Ano, mês e dia de lançamento                                                     |
| Spotify                  | Streams, playlists e posição em charts                                           |
| Apple Music              | Playlists e charts                                                               |
| Deezer                   | Playlists e charts                                                               |
| Shazam                   | Charts                                                                           |
| Características musicais | BPM, tonalidade, modo                                                            |
| Áudio                    | Dançabilidade, energia, valência, acústica, instrumentalidade, vivacidade e fala |

**Fonte:** dataset de músicas do Spotify disponibilizado no Kaggle.

---

## 🧹 Preparação e qualidade dos dados

Antes de analisar os padrões, foi realizada uma etapa de preparação para reduzir problemas que poderiam comprometer os resultados.

Foram verificadas:

* dimensões da base;
* tipos de dados;
* valores ausentes;
* duplicidades;
* valores fora das faixas esperadas;
* variáveis numéricas armazenadas como texto.

Algumas variáveis numéricas, como `streams` e métricas de presença nas plataformas, precisaram ser convertidas para tipos numéricos.

Também foram analisados valores ausentes e possíveis duplicidades, incluindo músicas com o mesmo nome.

Essa etapa foi importante porque **uma análise não começa no gráfico — começa entendendo a qualidade dos dados que estão por trás dele.**

---

## 🔎 Análises realizadas

### 1. Características musicais

Foram exploradas características como:

* `danceability_%`
* `energy_%`
* `valence_%`
* `acousticness_%`
* `instrumentalness_%`
* `liveness_%`
* `speechiness_%`
* `bpm`

Foram utilizadas distribuições, estatísticas descritivas, agrupamentos e correlações para investigar se determinadas características musicais apresentam relação relevante com o número de streams.

Também foi analisada a relação entre **energia e dançabilidade**, buscando entender se músicas mais dançantes tendem a apresentar maior energia.

---

### 2. Distribuição e exposição × Streams

Uma das principais análises do projeto foi investigar a relação entre o desempenho das músicas e sua presença em diferentes plataformas.

Foram analisadas métricas como:

* playlists do Spotify;
* playlists da Apple Music;
* playlists do Deezer;
* charts do Spotify;
* charts da Apple Music;
* charts do Deezer;
* charts do Shazam.

Além da correlação de Pearson, utilizei **correlação de Spearman**, especialmente útil para avaliar associações monotônicas e reduzir a influência de relações que não sejam necessariamente lineares.

---

### 3. Distribuição dos streams

A variável `streams` apresenta uma distribuição bastante assimétrica.

Por isso, além da análise dos valores originais, foi utilizada uma transformação logarítmica:

```python
log_streams = np.log1p(df['streams'])
```

Isso permitiu visualizar melhor a distribuição dos dados e compreender a concentração de músicas em diferentes níveis de popularidade.

---

### 4. Análise temporal

Também investiguei o período de lançamento das músicas.

Foram analisados:

* ano de lançamento;
* mês de lançamento;
* volume de músicas por período;
* streams por ano;
* streams por mês.

Um cuidado importante foi considerar que **streams são acumulados ao longo do tempo**.

Assim, uma música lançada anos antes de 2023 pode ter tido muito mais tempo para acumular reproduções do que uma música lançada próximo ao final de 2023.

Por esse motivo, diferenças entre períodos de lançamento não foram interpretadas automaticamente como evidência de que determinado período seja "melhor" para lançar uma música.

---

### 5. Artistas

Também foi investigada a frequência com que determinados artistas aparecem na base e a relação entre essa frequência e o volume de streams.

Uma das perguntas analisadas foi:

> **Artistas que aparecem mais vezes no ranking também apresentam maior volume de streams?**

Essa análise ajuda a diferenciar **frequência de presença** de **desempenho individual das músicas**.

---

## 📌 Principais resultados

### 🎧 Características musicais não explicam o sucesso sozinhas

As características musicais analisadas apresentam associações relativamente fracas com o número de streams.

Isso sugere que características como energia, dançabilidade, valência e BPM, isoladamente, não são suficientes para explicar o desempenho observado das músicas.

Em outras palavras:

> **Não parece existir uma única "fórmula musical" capaz de explicar quais músicas alcançam maior número de streams.**

---

### 📈 Presença em playlists apresenta associação muito mais forte

As métricas relacionadas à distribuição e presença em playlists apresentaram associações consideravelmente mais fortes com os streams.

Entre os resultados observados, destacam-se especialmente:

* presença em playlists do Spotify;
* presença em playlists da Apple Music.

Isso aponta para uma relação importante entre **exposição/distribuição e desempenho observado**.

Porém, existe uma distinção fundamental:

> **Correlação não significa causalidade.**

Uma música pode receber mais streams porque foi adicionada a mais playlists. Porém, também é possível que músicas que já apresentam maior popularidade recebam mais espaço em playlists.

A análise identifica uma associação — não determina qual variável causa a outra.

---

### 👤 Frequência de um artista não significa necessariamente maior desempenho

A presença recorrente de um artista no ranking não implica automaticamente que suas músicas tenham maior volume de streams.

Isso reforça a importância de analisar diferentes métricas em conjunto, em vez de utilizar apenas a quantidade de aparições como indicador de sucesso.

---

### 📅 O período de lançamento precisa ser interpretado com cautela

Músicas lançadas em anos anteriores podem apresentar números acumulados de streams significativamente maiores simplesmente por terem permanecido disponíveis por mais tempo.

Portanto, comparar diretamente os streams de músicas lançadas em períodos diferentes pode introduzir um viés temporal.

---

## 🧠 Uma das principais conclusões

O resultado mais interessante desta análise não foi descobrir uma característica musical "mágica".

Foi justamente o contrário.

Os dados indicam que **o desempenho observado das músicas está muito mais associado a métricas de distribuição e exposição do que às características musicais isoladas analisadas neste projeto**.

Isso muda a forma de enxergar a pergunta inicial.

Em vez de perguntar apenas:

> *"O que existe dentro da música?"*

também precisamos perguntar:

> *"Onde essa música está sendo exposta e distribuída?"*

Essa foi uma das principais aprendizagens que levei desta análise.

---

## ⚠️ Limitações

Uma análise exploratória precisa deixar claro o que seus dados **não** conseguem responder.

Entre as principais limitações deste projeto:

* a base representa um conjunto de músicas presentes no ranking, e não necessariamente todas as músicas lançadas em 2023;
* `streams` representa um valor acumulado, favorecendo músicas mais antigas;
* correlação não implica causalidade;
* presença em playlists pode ser tanto um fator associado à exposição quanto consequência da popularidade;
* existem valores ausentes em algumas variáveis;
* não estão disponíveis informações como investimento em divulgação, campanhas de marketing, orçamento promocional ou outras variáveis externas;
* os resultados devem ser interpretados como **associações observadas na base**, e não como regras gerais para determinar o sucesso de uma música.

---

## 🛠️ Tecnologias utilizadas

* **Python**
* **Pandas** — manipulação, limpeza e análise dos dados
* **NumPy** — operações numéricas e transformação dos dados
* **Matplotlib** — visualização de dados
* **Seaborn** — visualizações estatísticas
* **Jupyter Notebook** — desenvolvimento e documentação da análise

---

## 📂 Estrutura do projeto

```text
.
├── data/
│   └── spotify-2023.csv
│
├── notebook/
│   └── Análise_de_sucesso_musical_(dados_de_2023).ipynb
│
└── README.md
```

> A estrutura acima representa a organização recomendada para a versão disponibilizada no GitHub.

---

## ▶️ Como executar

### 1. Clone o repositório

```bash
git clone SEU_REPOSITORIO
```

### 2. Acesse a pasta do projeto

```bash
cd SEU_PROJETO
```

### 3. Instale as dependências

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 4. Execute o Jupyter Notebook

```bash
jupyter notebook
```

Depois, abra o notebook localizado na pasta `notebook/`.

---

## 📓 Notebook

A análise completa, incluindo o processo de preparação dos dados, exploração, visualizações, correlações e interpretações, está disponível no notebook do projeto.

**Notebook:** `Análise_de_sucesso_musical_(dados_de_2023).ipynb`

---

## 🚀 Próximos passos

Este projeto foi desenvolvido como uma análise exploratória. Algumas possibilidades de evolução seriam:

* analisar o **tempo desde o lançamento** de cada música;
* aprofundar a análise exclusivamente nas músicas lançadas em 2023;
* investigar padrões relacionados aos artistas;
* explorar gêneros musicais, caso uma fonte de dados adequada seja incorporada;
* aplicar modelos estatísticos para investigar relações entre múltiplas variáveis simultaneamente;
* incorporar dados externos relacionados à exposição, redes sociais ou outros indicadores de popularidade.

Essas extensões poderiam ajudar a separar melhor fatores relacionados à **popularidade acumulada**, **tempo de exposição** e **distribuição**.

---

## 👨‍💻 Sobre mim

**Daniel Souza**

Estudante de Ciência da Computação, interessado em tecnologia, programação e análise de dados.

Este projeto faz parte da minha construção de portfólio e representa uma etapa do meu aprendizado em análise exploratória de dados com Python.

Mais do que apresentar gráficos, meu objetivo neste projeto foi praticar uma habilidade que considero essencial para trabalhar com dados:

> **transformar uma pergunta em uma investigação, transformar dados em evidências e transformar evidências em conclusões que façam sentido.**

### 🔗 LinkedIn

**Daniel Souza** — `/in/daniel-souza-43891912a/`

---

## ⭐ Se este projeto foi útil para você

Se você chegou até aqui, obrigado por dedicar um tempo para conhecer o meu projeto.

Feedbacks, sugestões e críticas construtivas são sempre bem-vindos — especialmente porque este portfólio representa um processo contínuo de aprendizado.

**Obrigado por visitar o projeto!!! 🎵📊**
