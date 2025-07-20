# 🎧 LyricMind Bot – Análise Inteligente de Letras com IA

Este projeto é um fluxo construído no [n8n](https://n8n.io/) que integra o Telegram com a API da OpenAI para criar um chatbot inteligente capaz de analisar letras de músicas em múltiplos níveis, com suporte a múltiplos idiomas e comandos interativos.

## ✨ Funcionalidades

O bot permite que o usuário envie comandos via Telegram contendo URLs de letras de músicas. Ele então:

- 🎤 `/get_lyrics`: Retorna a **letra completa** com **tradução para PT-BR** (se necessário)
- 💡 `/interpret_lyrics`: Gera uma **interpretação emocional e simbólica** da música
- 📚 `/study_lyrics`: Analisa **expressões idiomáticas, gírias e figuras de linguagem**
- 🧠 `/summarize_lyrics`: Cria um **resumo objetivo** da letra
- 📖 `/vocabulary_lyrics`: Destaca **vocabulário relevante** com tradução e explicações
- ✍️ `/lyrics_poetic_analysis`: Realiza uma **análise poética e estilística**

## 🧱 Arquitetura do Fluxo

### 📥 Entrada
- Webhook `POST /MusicAiBot` recebe as mensagens do Telegram
- Filtro (`If`) identifica comandos válidos ou mensagens genéricas
- Extração de URL (caso aplicável)
- Requisição HTTP para baixar o conteúdo da letra
- Limpeza de HTML bruto com JavaScript (`CleanUp`)

### 🧠 Processamento com IA
Utiliza a OpenAI para interpretar ou responder aos comandos com base nos prompts configurados:

- Saudação e ajuda (`/start`)
- Retorno da letra (`/get_lyrics`)
- Interpretação emocional (`/interpret_lyrics`)
- Estudo linguístico (`/study_lyrics`)
- Resumo da música (`/summarize_lyrics`)
- Vocabulário relevante (`/vocabulary_lyrics`)
- Análise poética e estilística (`/lyrics_poetic_analysis`)

### 📤 Resposta
- As respostas são formatadas em **Markdown V2** e enviadas diretamente de volta ao Telegram

### 🛑 Fallback
- Comandos não reconhecidos recebem uma resposta padrão com orientações para uso correto

## 🛠️ Requisitos

- Conta e token de **Telegram Bot**
- Conta e chave da API da **OpenAI**
- Instância do **n8n** com os seguintes nós habilitados:
  - `Webhook`
  - `Set`, `Switch`, `If`, `NoOp`
  - `HTTP Request`
  - `JavaScript Code`
  - `Telegram`
  - `OpenAI`

## 🚀 Como usar

1. Configure as credenciais do Telegram e da OpenAI no n8n
2. Importe o arquivo `.json` deste projeto no n8n
3. Ative o fluxo e configure o webhook na API do Telegram com a URL gerada
4. Interaja com o bot no Telegram utilizando os comandos abaixo:

```bash
/start
/get_lyrics https://www.letras.mus.br/lana-del-rey/summertime-sadness/
/interpret_lyrics https://genius.com/Eminem-lose-yourself-lyrics
````

## 📌 Observações

* A limpeza de HTML utiliza expressões regulares para extrair apenas o conteúdo textual da página
* O modelo da OpenAI pode ser personalizado com ajustes nos parâmetros `temperature` e `max tokens`
* As respostas são adaptadas ao idioma nativo do usuário (ex: português, inglês, etc.)

## 📄 Licença

Este projeto é open-source e pode ser utilizado e adaptado livremente.

```
