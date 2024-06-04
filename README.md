# Projeto de Monitoramento de Dados Oceânicos

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

## Código

```python
import random
import sqlite3
import matplotlib.pyplot as plt

# Definição da classe Sensor
class Sensor:
    def __init__(self, sensor_id, tipo):
        self.sensor_id = sensor_id
        self.tipo = tipo
    
    def coletar_dados(self):
        if self.tipo == 'temperatura':
            return round(random.uniform(10.0, 30.0), 2)
        elif self.tipo == 'salinidade':
            return round(random.uniform(30.0, 40.0), 2)
        elif self.tipo == 'detecção de petróleo':
            return random.choice([True, False])

# Função para criar a tabela no banco de dados
def criar_tabela():
    conn = sqlite3.connect('dados_oceanicos.db')
    cursor = conn.cursor()
    cursor.execute('''CREATE TABLE IF NOT EXISTS dados (
                        id INTEGER PRIMARY KEY,
                        sensor_id INTEGER,
                        tipo TEXT,
                        valor REAL,
                        timestamp DATETIME DEFAULT CURRENT_TIMESTAMP)''')
    conn.commit()
    conn.close()

# Função para armazenar dados no banco de dados
def armazenar_dados(sensor_id, tipo, valor):
    conn = sqlite3.connect('dados_oceanicos.db')
    cursor = conn.cursor()
    cursor.execute("INSERT INTO dados (sensor_id, tipo, valor) VALUES (?, ?, ?)",
                   (sensor_id, tipo, valor))
    conn.commit()
    conn.close()

# Criando a tabela no banco de dados
criar_tabela()

# Criando sensores
sensores = [
    Sensor(sensor_id=1, tipo='temperatura'),
    Sensor(sensor_id=2, tipo='salinidade'),
    Sensor(sensor_id=3, tipo='detecção de petróleo')
]

# Coletando dados dos sensores
dados_coletados = {sensor.sensor_id: sensor.coletar_dados() for sensor in sensores}

# Armazenando dados coletados no banco de dados
for sensor in sensores:
    valor = dados_coletados[sensor.sensor_id]
    armazenar_dados(sensor.sensor_id, sensor.tipo, valor)

print("Dados Coletados:", dados_coletados)

# Funções para análise de dados
def analisar_temperatura(temperatura):
    if temperatura < 15.0 or temperatura > 25.0:
        return "Anomalia na temperatura detectada"
    return "Temperatura dentro dos padrões"

def analisar_salinidade(salinidade):
    if salinidade < 32.0 or salinidade > 37.0:
        return "Anomalia na salinidade detectada"
    return "Salinidade dentro dos padrões"

def analisar_petroleo(deteccao):
    if deteccao:
        return "Vazamento de petróleo detectado"
    return "Nenhum vazamento de petróleo detectado"

# Função para exibir resultados
def exibir_resultados(dados):
    for sensor_id, dado in dados.items():
        if sensor_id == 1:
            resultado = analisar_temperatura(dado)
        elif sensor_id == 2:
            resultado = analisar_salinidade(dado)
        elif sensor_id == 3:
            resultado = analisar_petroleo(dado)
        print(f"Sensor {sensor_id}: {resultado}")

# Exibindo resultados
exibir_resultados(dados_coletados)

# Função para visualizar dados coletados
def visualizar_dados():
    conn = sqlite3.connect('dados_oceanicos.db')
    cursor = conn.cursor()
    cursor.execute("SELECT timestamp, valor FROM dados WHERE tipo = 'temperatura'")
    dados_temperatura = cursor.fetchall()
    cursor.execute("SELECT timestamp, valor FROM dados WHERE tipo = 'salinidade'")
    dados_salinidade = cursor.fetchall()
    cursor.execute("SELECT timestamp, valor FROM dados WHERE tipo = 'detecção de petróleo'")
    dados_petroleo = cursor.fetchall()
    conn.close()

    # Preparando dados para o gráfico
    tempos_temp = [x[0] for x in dados_temperatura]
    valores_temp = [x[1] for x in dados_temperatura]
    tempos_sal = [x[0] for x in dados_salinidade]
    valores_sal = [x[1] for x in dados_salinidade]
    tempos_pet = [x[0] for x in dados_petroleo]
    valores_pet = [x[1] for x in dados_petroleo]

    # Criando gráficos
    plt.figure(figsize=(14, 6))

    # Gráfico de Temperatura
    plt.subplot(1, 3, 1)
    plt.plot(tempos_temp, valores_temp, label='Temperatura', color='blue')
    plt.xlabel('Tempo')
    plt.ylabel('Temperatura (°C)')
    plt.title('Temperatura ao longo do tempo')
    plt.xticks(rotation=45)

    # Gráfico de Salinidade
    plt.subplot(1, 3, 2)
    plt.plot(tempos_sal, valores_sal, label='Salinidade', color='green')
    plt.xlabel('Tempo')
    plt.ylabel('Salinidade (PSU)')
    plt.title('Salinidade ao longo do tempo')
    plt.xticks(rotation=45)

    # Gráfico de Detecção de Petróleo
    plt.subplot(1, 3, 3)
    plt.plot(tempos_pet, valores_pet, label='Detecção de Petróleo', color='red')
    plt.xlabel('Tempo')
    plt.ylabel('Detecção (0 ou 1)')
    plt.title('Detecção de Petróleo ao longo do tempo')
    plt.xticks(rotation=45)

    plt.tight_layout()
    plt.show()

# Visualizando dados coletados
visualizar_dados()
