# 🎶 LyricMindBot – Telegram Bot para Análise de Letras com IA via n8n

![LyricMind Bot em ação](./lyricmind-demo.gif)

Este projeto conecta o Telegram ao **n8n** com automações baseadas em **IA** para **análise de letras de músicas**.  
Ao enviar um **comando + link da letra da música**, o bot retorna traduções, interpretações, vocabulário e análises poéticas com base na letra fornecida.

---

## ⚙️ Funcionalidades

- 📥 Recebe comandos via Telegram
- 🌐 Extrai e limpa o conteúdo de uma URL com letra de música
- 🔤 Processa o texto usando **modelos da OpenAI (GPT-4 Turbo)**
- 📄 Gera diferentes tipos de análise textual para a letra

---

## 💬 Comandos Suportados

| Comando                   | Descrição                                                                 |
|--------------------------|---------------------------------------------------------------------------|
| `/start`                 | Envia uma mensagem de boas-vindas com instruções                          |
| `/get_lyrics`            | Retorna a **letra original + tradução linha a linha**                     |
| `/interpret_lyrics`      | Fornece uma **interpretação emocional e simbólica** da letra              |
| `/study_lyrics`          | Destaca **gírias, expressões idiomáticas e figuras de linguagem**         |
| `/summarize_lyrics`      | Gera um **resumo conciso** da música em até 5 frases                     |
| `/vocabulary_lyrics`     | Lista **palavras relevantes** com significado e tradução                  |
| `/lyrics_poetic_analysis`| Apresenta uma **análise poética e literária** da letra                    |

---

## 🧠 Como Funciona

1. O usuário envia um dos comandos com a URL de uma música (ex: `/get_lyrics https://www.letras.mus.br/...`)
2. O n8n faz o download da página e extrai o texto limpo
3. O texto é enviado para a OpenAI com instruções específicas por comando
4. O bot retorna a resposta diretamente no Telegram

---

## 🔐 Credenciais Necessárias

> Após importar o workflow no seu ambiente n8n, configure as credenciais:

### 1. **Telegram API**

- Criar via: `Credenciais → Telegram API`
- Inserir o token fornecido pelo [BotFather](https://t.me/BotFather)

### 2. **OpenAI API**

- Criar via: `Credenciais → OpenAI`
- Inserir sua `API Key` válida (modelo usado: `gpt-4`)

---

## 📌 Observações

- O webhook configurado no projeto é:  
  `https://<seu-servidor>/webhook/MusicAiBot`
- O projeto **não armazena nenhuma informação** após o uso
- Comandos malformados ou não reconhecidos recebem mensagens de erro amigáveis
- Testado com `n8n v1.100.1 (Self-hosted)`

---

## 👨‍💻 Desenvolvedor

> Desenvolvido por **Raphael de Carvalho Florencio**  
> Telegram: [@rapha_dunha](https://t.me/rapha_dunha)  
> Foco em soluções com IA + Automação com n8n

---
