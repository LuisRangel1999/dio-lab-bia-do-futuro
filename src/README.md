# Código da Aplicação

Esta pasta contém o código responsável pelo funcionamento do **Theo, o Orientador de Criptomoedas**.

## Estrutura

```text
src/
├── app.py              # Aplicação principal e interface do agente
├── README.md           # Documentação do código da aplicação
└── requirements.txt    # Dependências do projeto
```

## Tecnologias Utilizadas

- **Python** — Linguagem utilizada no desenvolvimento
- **Streamlit** — Interface de chat da aplicação
- **Ollama** — Execução local do modelo de linguagem
- **Requests** — Comunicação entre a aplicação e a API do Ollama
- **JSON/CSV** — Leitura dos dados da base de conhecimento

## Dependências

O projeto utiliza as seguintes bibliotecas Python:

```text
streamlit
requests
```

As bibliotecas `json` e `csv` fazem parte da biblioteca padrão do Python.

O **Ollama** não é instalado pelo `pip`, pois é uma aplicação separada responsável pela execução local do modelo de linguagem.

## Como Rodar

### 1. Instalar as dependências

Na raiz do projeto:

```bash
pip install -r src/requirements.txt
```

### 2. Iniciar o Ollama

Verifique se o Ollama está instalado e se o modelo utilizado pelo projeto está disponível.

```bash
ollama serve
```

### 3. Rodar a aplicação

Na raiz do projeto:

```bash
streamlit run src/app.py
```

Após iniciar, o Streamlit disponibilizará a aplicação no navegador.

## Funcionamento

A aplicação:

1. Carrega os arquivos JSON e CSV da pasta `data`;
2. Monta o contexto com informações do usuário, histórico e base de conhecimento;
3. Combina esse contexto com o **System Prompt** do Theo;
4. Envia a solicitação para o modelo executado pelo Ollama;
5. Exibe a resposta na interface do Streamlit.
