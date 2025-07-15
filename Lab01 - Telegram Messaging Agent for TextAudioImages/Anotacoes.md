# 📩 Como Configurar o WebHook de um Bot do Telegram (com Integração ao N8N)

⚠️ **Importante:** Este fluxo **não é indicado para canais do Telegram**, pois o payload recebido de canais possui uma estrutura JSON diferente da tratada neste fluxo. Ele foi desenvolvido para interações com **usuários individuais ou grupos**.

---

## 🧠 Conceito Básico

O **WebHook** permite que seu bot do Telegram receba mensagens de forma automática, sem precisar consultar a API com frequência (polling). Ao configurar um webhook, o Telegram envia as atualizações diretamente para o **endpoint HTTPS que você informar**.

---

## 🤖 Como Criar o Bot

1. No Telegram, converse com o [`@BotFather`](https://t.me/BotFather)
2. Use o comando `/newbot`
3. Escolha um nome e um nome de usuário exclusivo
4. Ao final, o BotFather fornecerá um **token** de acesso, que será usado nas chamadas à API:

```
Exemplo de token: 123456789:ABCdEfGhIjKlMnOpQrStUvWxYz
```

---

## ⚙️ Como Configurar o WebHook do Telegram

A configuração do WebHook é feita via **chamada GET ou POST para a API do Telegram**, e **não pode ser feita via aplicativo Telegram**.

### ✅ Endereço (endpoint) a ser configurado

O endpoint deve ser a **URL do webhook configurado no N8N**, que pode ser:

* **Ambiente de Teste**:

  ```http
  https://n8n.seusite.com/webhook-test/<nome_do_webhook>
  ```

* **Ambiente de Produção**:

  ```http
  https://n8n.seusite.com/webhook/<nome_do_webhook>
  ```

Exemplo de chamada:

```http
https://api.telegram.org/bot<SEU_BOT_TOKEN>/setWebhook?url=https://n8n.seusite.com/webhook/telegram
```

---

## 🎛️ Personalizando o tipo de atualização recebida: `allowed_updates`

Você pode configurar quais tipos de eventos seu bot deve receber usando o parâmetro `allowed_updates` (apenas se fizer uma **chamada POST** com `Content-Type: application/json`).

### Exemplo usando apenas mensagens (o mais comum):

```json
{
  "url": "https://n8n.seusite.com/webhook/telegram",
  "allowed_updates": ["message"]
}
```

Outros tipos possíveis de atualizações:

| Tipo de atualização   | Descrição                              |
| --------------------- | -------------------------------------- |
| `message`             | Mensagens comuns enviadas por usuários |
| `edited_message`      | Mensagens que foram editadas           |
| `channel_post`        | Postagens feitas em canais             |
| `edited_channel_post` | Edição de postagens em canais          |
| `callback_query`      | Clique em botões inline                |
| `inline_query`        | Consultas feitas em modo inline        |
| `poll`                | Envio de enquetes                      |
| `chat_member`         | Mudanças no status de membros do chat  |

> ⚠️ Se não informar o `allowed_updates`, o Telegram enviará **todos os tipos de atualização**.

### Exemplo de requisição POST para definir o WebHook com tipo `"message"`:

```bash
curl -X POST https://api.telegram.org/bot<SEU_BOT_TOKEN>/setWebhook \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://n8n.seusite.com/webhook/telegram",
    "allowed_updates": ["message"]
  }'
```

---

## 🔍 Verificando o Status do WebHook

Use o seguinte endpoint para verificar o webhook configurado:

```http
https://api.telegram.org/bot<SEU_BOT_TOKEN>/getWebhookInfo
```

Exemplo de resposta:

```json
{
  "ok": true,
  "result": {
    "url": "https://n8n.seusite.com/webhook/telegram",
    "has_custom_certificate": false,
    "pending_update_count": 0,
    "max_connections": 40
  }
}
```

---

## 🧹 Como remover o WebHook (ex: para usar `getUpdates`)

Se quiser desativar o webhook (por exemplo, para testar o `getUpdates`), use:

```http
https://api.telegram.org/bot<SEU_BOT_TOKEN>/deleteWebhook
```

---

## 📥 Como testar com `getUpdates` (modo polling)

Este método **somente funciona se o webhook estiver removido**.

```http
https://api.telegram.org/bot<SEU_BOT_TOKEN>/getUpdates
```

---

## 🔐 Configurando o Token no N8N

Ao usar o nó de Telegram no N8N:

1. Crie uma nova **credencial de bot Telegram**
2. Cole o **token fornecido pelo BotFather**
3. Salve e selecione a credencial no seu workflow

---

## ✅ Resumo de Endpoints Úteis

| Objetivo                                  | URL de exemplo                                                      |
| ----------------------------------------- | ------------------------------------------------------------------- |
| Definir WebHook (GET simples)             | `https://api.telegram.org/bot<SEU_TOKEN>/setWebhook?url=<ENDPOINT>` |
| Definir WebHook com tipo de evento (POST) | `curl -X POST ...` com `"allowed_updates": ["message"]`             |
| Verificar WebHook ativo                   | `https://api.telegram.org/bot<SEU_TOKEN>/getWebhookInfo`            |
| Remover WebHook                           | `https://api.telegram.org/bot<SEU_TOKEN>/deleteWebhook`             |
| Ver mensagens recebidas (`polling`)       | `https://api.telegram.org/bot<SEU_TOKEN>/getUpdates`                |
