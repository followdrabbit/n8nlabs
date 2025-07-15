# 🎵 LiryAnaBot – Telegram AI Music Assistant via n8n

Este projeto é um fluxo do **n8n** que conecta um bot no **Telegram** a uma automação de inteligência artificial capaz de receber mensagens com **nomes de músicas**, **cantores** ou **links**, e retornar:

* A **letra original** da música (em qualquer idioma)
* A **tradução**
* Uma **interpretação textual** da letra com apoio de IA

---

## ⚙️ Componentes Principais

### 📲 Recepção e Validação de Mensagens

* Webhook ativo em `https://n8n.parus.seg.br/webhook-test/musicinfo`
* Aceita mensagens de **texto**, **áudio (voz)** e **imagem**
* Validação do remetente antes de processar mensagens

### 🧠 Processamento com IA

* 🎤 **Mensagens de voz** são transcritas com o modelo **Whisper** (via OpenAI)
* 🖼️ **Imagens** são analisadas via **GPT-4o Vision**
* 💬 **Textos** são classificados e interpretados com **GPT-4 Turbo**

### 🧪 Roteamento por Tipo de Conteúdo

O fluxo utiliza um nó `Switch` chamado **Message Router** que divide as mensagens recebidas conforme o tipo:

* `"text"` → nome de música, cantor ou link
* `"voice"` → transcrição e interpretação
* `"photo"` → interpretação visual

---

## 🔐 Credenciais Necessárias

> Ao importar este projeto no seu ambiente n8n, você deverá configurar manualmente as credenciais:

### 1. **Telegram API**

* Criar via: `Credenciais → Telegram API`
* Inserir o token fornecido pelo [BotFather](https://t.me/BotFather)

### 2. **OpenAI API**

* Criar via: `Credenciais → OpenAI`
* Inserir sua `API Key` válida (modelos usados: `gpt-4`, `gpt-4-vision-preview`, `whisper-1`)

---

## 📌 Observações e Créditos

* Este projeto foi baseado no workflow oficial da comunidade n8n:
  🔗 [Telegram Messaging Agent for Text/Audio/Images](https://n8n.io/workflows/2751-telegram-messaging-agent-for-textaudioimages/),
  criado por **Joseph LePage** ([n8n.io][1], [n8n.io][2])
* Todas as melhorias feitas por **Raphael de Carvalho Florencio**, personalizando para letras, tradução e interpretação musical
* O projeto não armazena arquivos ou transcrições após o uso
* Pode ser adaptado para ambientes de produção alterando apenas a URL do webhook
* Testado com `n8n v1.100.1 (Self-hosted)`

---

## 👨‍💻 Desenvolvedor

> Desenvolvido por Raphael de Carvalho Florencio – [@rapha\_dunha](https://t.me/rapha_dunha)
> Foco em soluções com IA + Automação com n8n