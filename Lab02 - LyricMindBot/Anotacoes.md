# 🎧 LyricMind Bot – Análise Inteligente de Letras com IA

Este projeto é um fluxo construído no [n8n](https://n8n.io/) que integra o Telegram com a API da OpenAI para criar um chatbot inteligente capaz de analisar letras de músicas em múltiplos níveis, com suporte a múltiplos idiomas e comandos interativos.

## ✨ Funcionalidades

O bot permite que o usuário envie comandos via Telegram contendo **uma URL com a letra da música**. Ele então:

- 🎤 `/get_lyrics`: Retorna a **letra completa** com **tradução linha a linha para PT-BR**
- 💡 `/interpret_lyrics`: Gera uma **interpretação emocional e simbólica** da música
- 📚 `/study_lyrics`: Analisa **expressões idiomáticas, gírias e figuras de linguagem**
- 🧠 `/summarize_lyrics`: Cria um **resumo objetivo** da letra
- 📖 `/vocabulary_lyrics`: Destaca **vocabulário relevante** com tradução e explicações
- ✍️ `/lyrics_poetic_analysis`: Realiza uma **análise poética e estilística**
- 🆘 Comandos inválidos ou incompletos geram **respostas amigáveis com exemplos e instruções**

## 🧱 Arquitetura do Fluxo

### 📥 Entrada

- Webhook `POST /MusicAiBot` recebe mensagens de texto do Telegram
- Bloco `If` detecta se a mensagem contém texto
- Validação se o comando é `/start` ou outro
- Extração da URL da mensagem (quando aplicável)
- Requisição HTTP baixa o conteúdo da letra
- Código JavaScript (`CleanUp`) limpa o HTML e extrai apenas o texto
- Novo bloco `If` (`Mensagem Válida?`) verifica se o comando é suportado:
  - Se for reconhecido, envia para o `Switch`
  - Se não for, envia uma **mensagem de erro amigável com orientações**

### 🔄 Roteamento por Comando

- O `Switch` direciona o conteúdo limpo para o prompt correto da OpenAI com base no comando:
  - `/get_lyrics`, `/interpret_lyrics`, `/study_lyrics`, `/summarize_lyrics`, `/vocabulary_lyrics`, `/lyrics_poetic_analysis`
- Comandos não reconhecidos ou malformados são tratados e respondidos de forma clara

### 🧠 Processamento com IA

- O texto limpo da letra é enviado para o modelo **OpenAI GPT** com **prompts especializados**
- Os prompts estão adaptados para cada comando, considerando:
  - Tradução linha a linha
  - Interpretação emocional
  - Análise linguística e poética
  - Resumo e vocabulário
- O prompt de `/start` também responde no idioma do usuário (detectado pelo Telegram)

### 📤 Resposta

- As respostas são geradas pela IA e enviadas ao Telegram com formatação **Markdown V2**
- O usuário recebe as análises diretamente no chat

## 🛠️ Requisitos

- Conta e token de **Telegram Bot**
- Conta e chave da API da **OpenAI**
- Instância do **n8n** com os seguintes nós habilitados:
  - `Webhook`, `Set`, `Switch`, `If`, `NoOp`
  - `HTTP Request`, `JavaScript Code`
  - `Telegram`, `OpenAI`

## 🚀 Como usar

1. Configure as credenciais do Telegram e OpenAI no n8n
2. Importe o arquivo `.json` do projeto
3. Ative o fluxo e configure seu webhook com a URL pública gerada
4. Envie comandos para o bot no Telegram como:

```bash
/start
/get_lyrics https://www.letras.mus.br/lana-del-rey/summertime-sadness/
/interpret_lyrics https://genius.com/Eminem-lose-yourself-lyrics
````

## 📌 Observações

* A limpeza do HTML utiliza expressões regulares no JavaScript para extrair o texto da letra
* O modelo da OpenAI pode ser ajustado via parâmetros `temperature` e `maxTokens`
* O projeto **não possui suporte a voz ou imagem**
* Apenas **mensagens de texto** são processadas no fluxo atual
* A resposta de erro cobre:

  * Comandos desconhecidos
  * Comandos corretos porém sem URL

## 📄 Licença

Este projeto é open-source e pode ser utilizado e adaptado livremente.

```
