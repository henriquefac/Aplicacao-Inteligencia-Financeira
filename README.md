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

2.  **Suba os containers**:
    No diretório raiz do projeto, execute:
    ```bash
    docker compose up -d
    ```

3.  **Aguarde a inicialização**:
    - O serviço `ollama` baixará automaticamente o modelo `mistral` na primeira execução. Isso pode levar alguns minutos dependendo da sua conexão de internet.
    - Você pode acompanhar o progresso com:
      ```bash
      docker compose logs -f ollama-pull-model
      ```

4.  **Acesse a aplicação**:
    - **Frontend (Streamlit)**: [http://localhost:8501](http://localhost:8501)
    - **Backend (API Docs)**: [http://localhost:8000/docs](http://localhost:8000/docs)

### 🛠️ Configurações e Variáveis de Ambiente

As configurações principais são gerenciadas via variáveis de ambiente no arquivo `docker-compose.yml`:

- `LLM_PROVIDER`: Define o provedor de LLM (padrão: `ollama`).
- `LLM_BASE_URL`: URL do serviço Ollama (dentro da rede do Docker: `http://ollama:11434`).
- `BASE_URL` (Frontend): URL do backend (dentro da rede do Docker: `http://backend:8000`).

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
