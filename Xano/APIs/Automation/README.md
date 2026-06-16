# 🤖 API do Chatbot (N8N + Telegram)

Documentação da API consumida pelo chatbot de atendimento do SLFood, integrada via n8n ao bot do Telegram. Permite que o agente de IA consulte o cardápio, crie pedidos e acompanhe o status de pagamento diretamente pela conversa.

## Endpoints

### `GET /cardapio`

Retorna os produtos do cardápio filtrados por categoria, usado pelo chatbot para responder perguntas sobre os itens disponíveis.

**Autenticação:** não requerida

**Parâmetros:** `categoria_id` (query, obrigatório)

**Resposta de sucesso (200):**
```json
[
  {
    "id": 0,
    "nome": "string",
    "descricao": "string",
    "qtd_disp": 0,
    "url_imagem": "string",
    "preco": 0,
    "precisa_produzir": true,
    "categoria_id": 0
  }
]
```

<img width="960" height="724" alt="image" src="https://github.com/user-attachments/assets/7a823c3b-3d88-44ca-9b2f-0f28c8280fac" />


---

### `GET /produto`

Retorna os dados de um produto específico pelo ID, usado pelo chatbot para detalhar um item perguntado pelo cliente.

**Autenticação:** não requerida

**Parâmetros:** `produto_id` (query, obrigatório)


<img width="953" height="706" alt="image" src="https://github.com/user-attachments/assets/d51581a0-a2e5-4f4c-923a-41fb38f7b4a8" />


---

### `POST /pedido_criar`

Cria um pedido com base nos itens enviados durante a conversa no chatbot, validando produtos e valores diretamente no banco de dados.

**Autenticação:** não requerida

**Request body:**
```json
{
  "cliente_id": 0,
  "itens": {}
}
```

<img width="957" height="748" alt="image" src="https://github.com/user-attachments/assets/ba7db9a7-a1b3-4147-8ca7-ede728b5c4a9" />


---

### `GET /pedido_status`

Consulta o status atual de um pedido, incluindo seus itens e o status individual de cada um — usado pelo chatbot para responder "onde está meu pedido".

**Autenticação:** não requerida

**Parâmetros:** `pedido_id` (query, obrigatório)

**Resposta de sucesso (200):**
```json
{
  "sucesso": "string",
  "pedido_id": "string",
  "cliente_id": "string",
  "total": "string",
  "status_pedido_id": "string",
  "status": "string",
  "itens": [
    {
      "id": 0,
      "qtd": 0,
      "valor_unit": 0,
      "subtotal": 0,
      "produto_id": 0,
      "status_item_id": 0
    }
  ]
}
```

<img width="960" height="795" alt="image" src="https://github.com/user-attachments/assets/fd4d202d-7689-4bc1-a648-ec2db9a1ac98" />


---

### `POST /pix_solicitar`

Solicita a geração da cobrança Pix referente a um pedido feito via chatbot.

**Autenticação:** não requerida

**Request body:**
```json
{
  "pedido_id": 0
}
```

<img width="955" height="892" alt="image" src="https://github.com/user-attachments/assets/f426f9c3-cb69-4917-86b8-eee0f9d0d44a" />

---

### `POST /pix_enviar_codigo`

Envia o código/QR Code Pix para o cliente finalizar o pagamento pelo Telegram.

**Autenticação:** não requerida

**Request body:**
```json
{
  "pedido_id": 0
}
```

<img width="957" height="885" alt="image" src="https://github.com/user-attachments/assets/47697017-1b9b-4cd0-b367-b68bc1e756da" />


---

### `POST /pix_confirmar`

Confirma o pagamento Pix e atualiza o status do pedido e da transação correspondente.

**Autenticação:** não requerida

**Request body:**
```json
{
  "pedido_id": 0
}
```

<img width="957" height="893" alt="image" src="https://github.com/user-attachments/assets/d7812a0f-ac2e-412f-9f6c-20db8a1e9729" />


---

## Sobre essa API

Diferente da API de Produção (consumida pelo app), esta é a versão consumida pelos fluxos do **n8n**, que orquestram a conversa do chatbot no Telegram com um agente de IA. O fluxo típico é: o cliente conversa com o bot → o agente de IA interpreta a intenção → o n8n chama o endpoint correspondente nesta API → a resposta é formatada e enviada de volta ao Telegram.

## Tratamento de erros

| Código | Significado |
|---|---|
| 400 | Erro de validação no payload da requisição |
| 401 | Não autorizado |
| 403 | Acesso negado — privilégios insuficientes |
| 404 | Recurso não encontrado |
| 429 | Limite de requisições excedido |
| 500 | Erro inesperado no servidor |
