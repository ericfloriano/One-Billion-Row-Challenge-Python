# 📊 Um Bilhão de Linhas: Desafio de Processamento de Dados com Python

## 🚀 Visão Geral

Este projeto tem como objetivo mostrar como **processar um arquivo massivo de 1 bilhão de linhas (~14GB)** usando Python e bibliotecas modernas para extrair estatísticas como temperatura mínima, média e máxima por estação meteorológica — tudo isso com foco em eficiência e performance.

Inspirado no famoso [One Billion Row Challenge](https://github.com/gunnarmorling/1brc), originalmente proposto em Java, a proposta aqui é mostrar como Python também pode resolver este tipo de tarefa.

## 📓 Estrutura do Arquivo

Cada linha do arquivo representa uma medição de temperatura de uma estação meteorológica, no formato:
```
<string: nome da estação>;<double: medição>
```

Exemplo de 10 linhas:
```
Hamburg;12.0
Bulawayo;8.9
Palembang;38.8
St. Johns;15.2
Cracow;12.6
Bridgetown;26.9
Istanbul;6.2
Roseau;34.4
Conakry;31.2
Istanbul;23.0
```

## 🎯 Objetivo

Para cada estação, calcular:
- **Temperatura mínima**
- **Temperatura média** (arredondada para uma casa decimal)
- **Temperatura máxima**

Os resultados devem ser exibidos em uma tabela ordenada pelo nome da estação:

| station      | min_temperature | mean_temperature | max_temperature |
|--------------|-----------------|------------------|-----------------|
| Abha         | -31.1           | 18.0             | 66.5            |
| Abidjan      | -25.9           | 26.0             | 74.6            |
| Abéché       | -19.8           | 29.4             | 79.9            |
| Accra        | -24.8           | 26.4             | 76.3            |
| Addis Ababa  | -31.8           | 16.0             | 63.9            |
| Adelaide     | -31.8           | 17.3             | 71.5            |
| Aden         | -19.6           | 29.1             | 78.3            |
| Ahvaz        | -24.0           | 25.4             | 72.6            |
| Albuquerque  | -35.0           | 14.0             | 61.9            |
| Alexandra    | -40.1           | 11.0             | 67.9            |
| ...          | ...             | ...              | ...             |
| Yangon       | -23.6           | 27.5             | 77.3            |
| Yaoundé      | -26.2           | 23.8             | 73.4            |
| Yellowknife  | -53.4           | -4.3             | 46.7            |
| Yerevan      | -38.6           | 12.4             | 62.8            |
| Yinchuan     | -45.2           | 9.0              | 56.9            |
| Zagreb       | -39.2           | 10.7             | 58.1            |
| Zanzibar City| -26.5           | 26.0             | 75.2            |
| Zürich       | -42.0           | 9.3              | 63.6            |
| Ürümqi       | -42.1           | 7.4              | 56.7            |
| İzmir        | -34.4           | 17.9             | 67.9            |

## 🧰 Dependências

Para executar os scripts deste projeto, você precisará das seguintes bibliotecas:

* Polars: `0.20.3`
* DuckDB: `0.10.0`
* Dask[complete]: `^2024.2.0`

## ⚙️ Como Executar



Para executar este projeto e reproduzir os resultados:

1. Clone o repositório

2. Defina o Python com `pyenv local 3.12.1`

3. Configure o ambiente:
```
poetry env use 3.12.1
poetry install --no-root
poetry lock
```

4. Gere o arquivo de testes:
```
python src/create_measurements.py
```
_(A geração do arquivo pode levar cerca de 10 minutos.)_

5. Certifique-se de instalar as versões especificadas das bibliotecas Dask, Polars e DuckDB

6. Execute os scripts com:
```
poetry run python src/using_python.py
poetry run python src/using_pandas.py
poetry run python src/using_dask.py
poetry run python src/using_polars.py
poetry run python src/using_duckdb.py` 
```

## Resultados

Os testes foram realizados em um laptop equipado com um processador M1 da Apple e 8GB de RAM. As implementações utilizaram abordagens puramente Python, Pandas, Dask, Polars e DuckDB. Os resultados de tempo de execução para processar o arquivo de 1 bilhão de linhas são apresentados abaixo:

| Implementação | Tempo |
| --- | --- |
| Bash + awk | 25 minutos |
| Python | 20 minutos |
| Python + Pandas | 263 sec |
| Python + Dask | 155.62 sec  |
| Python + Polars | 33.86 sec |
| Python + Duckdb | 14.98 sec |

## 🔧 Bônus

Verifique se as ferramentas utilizadas no script (`wc`, `head`, `pv`, `awk`, e `sort`) estão instaladas em seu sistema. Se necessário instale `pv` (Pipe Viewer) pode precisar ser instalado manualmente.

### Instalando o Pipe Viewer (pv)

Se você não tem o `pv` instalado, pode facilmente instalá-lo usando o gerenciador de pacotes do seu sistema. Por exemplo:

* No Ubuntu/Debian:
    
    ```bash
    sudo apt-get update
    sudo apt-get install pv
    ```
    
* No macOS (usando [Homebrew](https://brew.sh/)):
    
    ```bash
    brew install pv
    ```
    
### Preparando o Script

1. Dê permissão de execução para o arquivo script. Abra um terminal e execute:
    
    ```bash
    chmod +x process_measurements.sh
    ```

2. Rode o script. Abra um terminal e execute:
   
   ```bash
   ./src/using_bash_and_awk.sh 1000
   ```

Neste exemplo, apenas as primeiras 1000 linhas serão processadas.

Ao executar o script, você verá a barra de progresso (se pv estiver instalado corretamente) e, eventualmente, a saída esperada no terminal ou em um arquivo de saída, se você decidir modificar o script para direcionar a saída.

## 🧠 Conclusão

Este desafio destacou claramente a eficácia de diversas bibliotecas Python na manipulação de grandes volumes de dados. Métodos tradicionais como Bash (25 minutos), Python puro (20 minutos) e até mesmo o Pandas (5 minutos) demandaram uma série de táticas para implementar o processamento em "lotes", enquanto bibliotecas como Dask, Polars e DuckDB provaram ser excepcionalmente eficazes, requerendo menos linhas de código devido à sua capacidade inerente de distribuir os dados em "lotes em streaming" de maneira mais eficiente. O DuckDB se sobressaiu, alcançando o menor tempo de execução graças à sua estratégia de execução e processamento de dados.

Esses resultados enfatizam a importância de selecionar a ferramenta adequada para análise de dados em larga escala, demonstrando que Python, com as bibliotecas certas, é uma escolha poderosa para enfrentar desafios de big data.

## Agradecimentos

- Obrigado:
    - [Luciano](https://suajornadadedados.com.br/) pela aula no JD
    - [Koen Vossen](https://github.com/koenvo) pela implementação em Polars
    - [Arthur Julião](https://github.com/ArthurJ) pela implementação em Python e Bash 