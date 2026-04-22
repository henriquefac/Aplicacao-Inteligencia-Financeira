# Aplicação de Inteligência Financeira

Este projeto unifica uma interface frontend (Streamlit) com um backend (FastAPI) e um serviço de IA local (Ollama).

## 🚀 Como Executar com Docker Compose

A maneira mais fácil de subir toda a aplicação é utilizando o Docker Compose. Isso configurará automaticamente o frontend, o backend e o serviço do Ollama com o modelo `mistral`.

### Pré-requisitos

- Docker instalado
- Docker Compose instalado

### Passo a Passo

1.  **Clone o repositório** (se ainda não o fez):
    ```bash
    git clone <url-do-repositorio>
    cd <diretorio-do-projeto>
    ```

2.  **Configure as variáveis de ambiente**:
    Crie um arquivo `.env` na raiz do projeto baseado no exemplo fornecido:
    ```bash
    cp .env.example .env
    ```
    Edite o arquivo `.env` e adicione sua **OpenRouter API Key** para habilitar os modelos de IA em nuvem (ou mantenha o Ollama para uso 100% local).

3.  **Suba os containers**:
    No diretório raiz do projeto, execute:
    ```bash
    docker compose up -d
    ```

4.  **Aguarde a inicialização**:
    - O serviço `ollama` baixará automaticamente o modelo `mistral` na primeira execução. Isso pode levar alguns minutos dependendo da sua conexão de internet.
    - Você pode acompanhar o progresso com:
      ```bash
      docker compose logs -f ollama-pull-model
      ```

    - **Frontend (Streamlit)**: [http://localhost:8501](http://localhost:8501)
    - **Backend (API Docs)**: [http://localhost:8000/docs](http://localhost:8000/docs)

### 🔑 Configuração do OpenRouter (Recomendado)

Esta aplicação utiliza o **OpenRouter** como provedor principal de IA por oferecer acesso gratuito a modelos potentes como o Llama 3 e Gemma.
1. Crie uma conta em [openrouter.ai](https://openrouter.ai/).
2. Gere uma chave de API em [Keys](https://openrouter.ai/keys).
3. Insira a chave no seu arquivo `.env` na variável `OPENROUTER_API_KEY`.

O **Ollama** é configurado automaticamente como fallback local caso o OpenRouter falhe ou não tenha chave configurada.

As configurações principais são gerenciadas via arquivo `.env`. Veja o arquivo [.env.example](.env.example) para a lista completa de variáveis.

Principais variáveis:
- `OPENROUTER_API_KEY`: Sua chave do OpenRouter.
- `LLM_PROVIDER`: Define o provedor de LLM (`openrouter` ou `ollama`).
- `LLM_MODEL`: Modelo usado no Ollama (padrão: `mistral`).

## 📁 Estrutura do Projeto

- `backend/`: API FastAPI para processamento de dados e integração com LLM.
- `frontend/`: Interface Streamlit para visualização de métricas e chat de IA.
- `docker-compose.yml`: Orquestração de todos os serviços.

## 🛑 Parando a Aplicação

Para parar e remover os containers:
```bash
docker compose down
```

Se desejar remover também os volumes (limpando os dados salvos e modelos do Ollama):
```bash
docker compose down -v
```
