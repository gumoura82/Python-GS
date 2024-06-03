# Python-GS

# Projeto de Coleta e Análise de Dados Oceânicos

Este projeto coleta dados de sensores oceânicos, armazena-os em um banco de dados SQLite e gera visualizações para análise.

## Índice

- [Instalação](#instalação)
- [Uso](#uso)
- [Contribuição](#contribuição)
- [Licença](#licença)
- [Autores](#autores)

## Instalação

### Pré-requisitos

- Python 3.x
- Bibliotecas Python: `random`, `sqlite3`, `matplotlib`

### Passos para instalação

1. Clone o repositório:

    ```bash
    git clone https://github.com/gumoura82/Python-GS.git
    cd Python-GS
    ```

2. Instale as dependências:

    ```bash
    pip install matplotlib
    ```

## Uso

### Coletando e Armazenando Dados

1. Execute o script para coletar dados dos sensores e armazená-los no banco de dados:

    ```bash
    python moi.py
    ```

2. O script criará automaticamente a tabela `dados` no banco de dados `dados_oceanicos.db` se ainda não existir, coletará dados de três tipos de sensores (temperatura, salinidade e detecção de petróleo) e armazenará esses dados.

### Análise e Visualização de Dados

1. O script também executa uma análise básica dos dados coletados e exibe os resultados.
2. Além disso, gera gráficos das medições ao longo do tempo para cada tipo de sensor.

## Contribuição

Se você gostaria de contribuir, por favor, siga os seguintes passos:

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## Autores

- **Ygor Vieira Pontes RM - 555686** - *Desenvolvedor inicial*
- **Gustavo Oliveira de Moura RM - 555827** - *Desenvolvedor inicial*
- **Lynn Bueno Rosa RM - 551102** - *Desenvolvedor inicial*
