# Projeto de PLN: Chatbot de Notícias com RAG

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python)
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-Models-yellow?style=for-the-badge)

## Descrição

Este projeto implementa um chatbot de notícias baseado na arquitetura **RAG (Retrieval-Augmented Generation)**. O sistema coleta notícias em tempo real de portais brasileiros por meio de feeds RSS, processa e vetoriza esse conteúdo, e utiliza um Large Language Model (LLM) para gerar respostas contextualizadas em linguagem natural.

O objetivo é fornecer respostas fundamentadas exclusivamente nas informações encontradas nas notícias coletadas, reduzindo a ocorrência de respostas inventadas pelo modelo e mantendo a verificação das informações.

## Funcionalidades

- **Coleta de Dados**: Busca notícias de diversas fontes locais, regionais e nacionais do Brasil.  
- **Pré-processamento de Texto**: Limpeza de HTML e formatação do conteúdo para análise.  
- **Busca Semântica**: Utiliza o modelo `paraphrase-multilingual-MiniLM-L12-v2` para criar embeddings (vetores) das notícias.  
- **Indexação e Recuperação**: Armazena os vetores em um índice `FAISS` para buscas de similaridade.  
- **Geração Aumentada por Recuperação (RAG)**:  
  1. A pergunta do usuário é convertida em um vetor.  
  2. O FAISS recupera os artigos mais relevantes.  
  3. Os artigos recuperados são usados como contexto em um prompt para o LLM.  
  4. O LLM `HuggingFaceH4/zephyr-7b-beta` gera a resposta final baseada no contexto.  

## Tecnologias Utilizadas

- **Linguagem**: Python 3.10+  
- **Coleta de Dados**: `feedparser`, `BeautifulSoup4`  
- **Manipulação de Dados**: `pandas`, `numpy`  
- **Modelos de Linguagem e IA**:  
  - `transformers` (Hugging Face)  
  - `sentence-transformers`  
  - `torch` (PyTorch)  
  - `accelerate` e `bitsandbytes` para otimização e quantização de modelos em 4-bit  
- **Banco de Dados Vetorial**: `faiss-cpu` (Facebook AI Similarity Search)  
- **LLM para Geração**: `HuggingFaceH4/zephyr-7b-beta`  
- **Ambiente**: Jupyter Notebook  

## Execução do Projeto

**Requisitos de Hardware**  
- Para executar o LLM, é recomendável uma GPU NVIDIA com suporte a CUDA e pelo menos 12GB de VRAM.  


## Passos para Execução

1. **Clone o repositório**

   ```bash
   git clone https://github.com/LeandroJackson/rss2rag-chatbot.git
   cd rss2rag-chatbot
   ```

2. **Instale o Jupyter Notebook** (se ainda não tiver)

   ```bash
   pip install notebook
   ```

3. **Execute o Jupyter Notebook**

   ```bash
   jupyter notebook rss2rag.ipynb
   ```

4. No notebook, execute as células em ordem. A primeira célula já contém a instalação de todas as dependências necessárias, portanto não é preciso instalar manualmente via terminal.

---

## Exemplo de Uso

O usuário pode fazer perguntas sobre eventos atuais e o chatbot buscará as notícias mais relevantes para formular a resposta.

**Exemplo de Pergunta 1:**

> `Quais as novidades sobre a prefeitura de João Pessoa?`

**Exemplo de Pergunta 2:**

> `O dólar incidiu em apreciação ou em depreciação?`

O sistema recupera os documentos de contexto e gera uma resposta formal, conforme demonstrado no notebook.
