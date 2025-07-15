# 🧪 Repositório de Laboratórios N8N

Este repositório reúne **laboratórios testados no N8N**, organizados por pastas individuais. Cada laboratório inclui um **workflow funcional**, um arquivo com **anotações úteis** sobre o processo de construção e um `README.md` descritivo para facilitar a reprodução e o aprendizado.

---

## 🎯 Objetivo

> Documentar experimentos reais com o N8N, facilitar o reaproveitamento de fluxos e apoiar outros desenvolvedores na criação de automações com IA, bots, APIs e mais.

---

## 📁 Estrutura de Diretórios

Cada laboratório é armazenado em um diretório com a seguinte estrutura:

```

lab01-nome-do-projeto/
├── Anotacoes.md       # Dicas, comandos, URLs e notas técnicas do projeto
├── README.md          # Explicação funcional do fluxo N8N
├── workflow\.json      # Exportação oficial do fluxo N8N

```

Exemplo real:
```

lab01-telegram-messaging-agent/
├── Anotacoes.md
├── README.md
├── TelegramMusicBot.json

````

---

## ✅ Laboratórios Disponíveis

| ID       | Nome do Projeto                             | Descrição                                              | Status     |
|----------|---------------------------------------------|--------------------------------------------------------|------------|
| `lab01`  | Telegram Messaging Agent for TextAudioImages | Bot que processa texto, voz e imagem com GPT + Whisper | ✅ Testado |

> Novos labs serão adicionados conforme os testes forem sendo realizados.

---

## 🚀 Como Usar

1. Clone o repositório:

    ```bash
   git clone https://github.com/seu-usuario/n8n-labs.git
   cd n8n-labs
    ```

2. Navegue até o diretório do laboratório desejado:

   ```bash
   cd lab01-telegram-messaging-agent
   ```

3. Leia o arquivo `README.md` e as `Anotacoes.md` do lab.

4. Importe o `workflow.json` no seu ambiente N8N:

   * Acesse o painel do N8N
   * Clique em **Workflows > Import from File**
   * Selecione o arquivo `.json` do laboratório

5. Configure as **credenciais necessárias** (Telegram API, OpenAI, etc.)

---

## 🛠️ Requisitos Gerais

* Instância do [n8n](https://n8n.io) (self-hosted ou cloud)
* Conta no [Telegram](https://t.me/BotFather) para criar bots
* API Key da [OpenAI](https://platform.openai.com) (para GPT, Whisper e Vision)

---

## 🤝 Contribuições

Contribuições são bem-vindas! Você pode:

* Criar seu próprio laboratório seguindo o mesmo padrão de pastas
* Abrir issues com dúvidas ou sugestões
* Criar PRs para corrigir erros ou melhorar a documentação

---

## 👨‍💻 Autor

**Raphael de Carvalho Florencio**
[🔗 LinkedIn](https://linkedin.com/in/raphaelflorencio) · [📬 Telegram](https://t.me/rapha_dunha)

---

> “O melhor jeito de aprender é ensinando. Compartilhar seus experimentos pode ajudar alguém do outro lado do mundo.” 🚀
