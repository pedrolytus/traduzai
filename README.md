# TraduzAI - Pipeline de Tradução Automatizada de PDFs

## Visão Geral
O TraduzAI é uma aplicação desktop desenvolvida em Python para a tradução automatizada de documentos em formato PDF. O sistema extrai o texto original, realiza o particionamento em blocos (chunking) e consome a API de inteligência artificial do Google Gemini (modelo 2.5 Flash) para gerar traduções precisas, mantendo o contexto global da obra por meio de Engenharia de Prompt Dinâmica.

## Arquitetura e Tecnologias
Este projeto adota práticas de Engenharia de Software e DevOps para garantir resiliência e facilidade de manutenção.
* **Linguagem:** Python 3
* **Interface Gráfica:** Tkinter (Interface nativa e leve)
* **Processamento de PDF:** PyPDF2
* **Inteligência Artificial:** `google-generativeai` (Gemini 2.5 Flash)
* **Gerenciamento de Credenciais:** `python-dotenv` (Variáveis de ambiente)
* **Exportação de Dados:** `markdown` e `python-docx`
* **Concorrência:** `threading` (Processamento em segundo plano)

## Funcionalidades Principais (MVP - Fase 1)
1. **Particionamento de Texto (Chunking):** Divisão do documento em blocos de páginas para respeitar o limite de contexto do modelo e evitar perda de formatação.
2. **Engenharia de Prompt com Auto-Reflexão:** O agente analisa o texto antes da tradução para identificar o domínio de conhecimento (ex: psicologia, tecnologia) e aplicar o jargão acadêmico correto.
3. **Resiliência de Rede (Exponential Backoff):** Algoritmo de recuo exponencial que captura erros de limite de cota (Erro 429) e pausa a execução progressivamente (15s, 30s, 60s...) sem interromper a aplicação.
4. **Persistência em Tempo Real (Write-on-the-fly):** O texto é gravado em disco a cada bloco traduzido, garantindo que o progresso não seja perdido em caso de falha crítica.
5. **Exportação Multi-formato:** Geração automática do resultado final em `.md`, `.html` (estilizado para leitura em navegadores) e `.docx` (Microsoft Word).
6. **Sandbox de Teste:** Interface integrada para validação rápida de prompts e verificação de conectividade da API.

## Pré-requisitos e Instalação

1. Clone o repositório.
2. Crie e ative um ambiente virtual (venv):
   `python -m venv venv`
   `.\venv\Scripts\activate` (No Windows)
3. Instale as dependências:
   `pip install PyPDF2 google-generativeai python-dotenv markdown python-docx`
4. Crie um arquivo `.env` na raiz do projeto contendo a sua chave de API:
   `GEMINI_API_KEY=sua_chave_aqui`

## Como Executar
Com o ambiente virtual ativado, execute o script principal no terminal:
`python main.py`
