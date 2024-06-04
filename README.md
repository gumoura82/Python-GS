# P# Projeto de Monitoramento de Dados Oceânicos

## Descrição do Projeto
Este projeto consiste em um sistema de monitoramento de dados oceânicos, utilizando sensores para coletar informações como temperatura, salinidade e detecção de petróleo. Os dados são armazenados em um banco de dados SQLite e analisados quanto à conformidade com os padrões esperados. Além disso, é possível visualizar graficamente a evolução desses dados ao longo do tempo.

## Instruções de Uso

### 1. Criação da Tabela no Banco de Dados
A tabela é criada automaticamente ao executar o código, se ainda não existir. O banco de dados utilizado é `dados_oceanicos.db`.

### 2. Execução do Código
Certifique-se de ter as bibliotecas `sqlite3` e `matplotlib` instaladas.

Execute o script Python para coletar dados dos sensores, armazená-los no banco de dados e realizar análises.

### 3. Análise de Dados
Após a coleta, os dados são analisados para verificar se estão dentro dos padrões esperados para temperatura, salinidade e detecção de petróleo.

### 4. Visualização Gráfica
Os dados coletados podem ser visualizados graficamente utilizando a função `visualizar_dados()`. Serão exibidos gráficos separados para temperatura, salinidade e detecção de petróleo ao longo do tempo.

## Requisitos e Dependências
- **Python 3.x**
- **Bibliotecas**:
  - `sqlite3`: Utilizada para interação com o banco de dados SQLite.
  - `matplotlib`: Utilizada para criar os gráficos de visualização dos dados.
  - `random`: Utiliza números aleatórios, para simular o sensor. 

## Detalhes Adicionais

### Classe Sensor (`Sensor`)
Define diferentes tipos de sensores (temperatura, salinidade, detecção de petróleo).

#### Método `coletar_dados()`
Simula a coleta de dados com valores aleatórios para cada tipo de sensor.

### Banco de Dados SQLite (`dados_oceanicos.db`)
Armazena os dados coletados, incluindo `sensor_id`, `tipo`, `valor` e `timestamp`.

### Análise de Dados
Funções que verificam se os valores coletados estão dentro dos padrões esperados:

- `analisar_temperatura()`
- `analisar_salinidade()`
- `analisar_petroleo()`

### Visualização Gráfica (`visualizar_dados()`)
Utiliza `matplotlib` para plotar gráficos de temperatura, salinidade e detecção de petróleo ao longo do tempo.
