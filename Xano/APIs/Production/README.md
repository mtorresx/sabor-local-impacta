# 🍽️ API de Produção (Cardápio, Pedidos e Pagamento Pix)

Documentação da API de produção do SLFood, desenvolvida no Xano. Responsável pela listagem e detalhe de produtos do cardápio, criação de pedidos e todo o fluxo de pagamento via Pix.

## Endpoints

### `GET /produto_listar`

Retorna a lista completa de produtos disponíveis no cardápio, com nome, descrição, preço, imagem, quantidade disponível e categoria.

**Autenticação:** não requerida

**Resposta de sucesso (200):**
```json
[
  {
    "id": 0,
    "created_at": "now",
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

<img width="1152" height="798" alt="image" src="https://github.com/user-attachments/assets/86b2718c-9163-457c-9911-1f3ce485ceea" />


---

### `GET /produto_buscar`

Permite buscar produtos do cardápio a partir de um termo de busca textual.

**Autenticação:** não requerida

**Parâmetros:** `busca` (query, opcional)

<img width="1151" height="779" alt="image" src="https://github.com/user-attachments/assets/090000aa-dd3e-4da6-b34f-0edb82738751" />


---

### `GET /produto_detalhe`

Retorna os dados detalhados de um produto específico pelo ID, incluindo seus itens adicionais disponíveis — usado na tela de detalhe do produto no app do cliente.

**Autenticação:** não requerida

**Parâmetros:** `produto_id` (query)

**Resposta de sucesso (200):**
```json
{
  "produto": {
    "id": 0,
    "nome": "string",
    "descricao": "string",
    "qtd_disp": 0,
    "url_imagem": "string",
    "preco": 0,
    "precisa_produzir": true,
    "categoria_id": 0
  },
  "adicionais": [
    {
      "id": 0,
      "nome": "string",
      "preco": 0
    }
  ]
}
```

<img width="1073" height="949" alt="image" src="https://github.com/user-attachments/assets/3b4b25a7-c45b-45d1-a588-b31c2e86fb23" />


---

### `POST /pedido_criar`

Cria um novo pedido a partir do carrinho do cliente, calculando subtotal, taxa de entrega e total.

**Autenticação:** não requerida

**Request body:**
```json
{
  "cliente_id": 0,
  "itens": {}
}
```

**Resposta de sucesso (200):**
```json
{
  "pedido": {
    "id": 0,
    "total": 0,
    "cliente_id": 0,
    "status_pedido_id": 0
  },
  "subtotal": "string",
  "taxa_entrega": "string",
  "total": "string"
}
```

<img width="1086" height="900" alt="image" src="https://github.com/user-attachments/assets/6f82a725-57ad-43a6-9d99-dd1259f47e87" />


---

### `POST /pix_solicitar`

Solicita a geração da cobrança Pix referente a um pedido, retornando os dados da transação e o código de cobrança.

**Autenticação:** não requerida

**Request body:**
```json
{
  "pedido_id": 0
}
```

<img width="957" height="890" alt="image" src="https://github.com/user-attachments/assets/8c07ba19-1a93-4ed8-ba96-40cc8e7d2649" />


---

### `POST /pix_enviar_codigo`

Envia o código/QR Code Pix gerado para o cliente finalizar o pagamento.

**Autenticação:** não requerida

**Request body:**
```json
{
  "pedido_id": 0
}
```

<img width="955" height="886" alt="image" src="https://github.com/user-attachments/assets/7253f259-a3f0-44aa-b119-af0b3af3eeb6" />


---

### `POST /pix_confirmar`

Confirma o pagamento Pix realizado, atualizando o status do pedido e da transação correspondente.

**Autenticação:** não requerida

**Request body:**
```json
{
  "pedido_id": 0
}
```

**Resposta de sucesso (200):**
```json
{
  "sucesso": "string",
  "mensagem": "string",
  "pedido_id": "string",
  "status_pedido_id": "string",
  "transacao_id": "string",
  "status_transacao_id": "string"
}
```

<img width="959" height="928" alt="image" src="https://github.com/user-attachments/assets/03e5c4af-947e-4b21-bc5d-9c003d2b22ad" />


---

## Fluxo de pagamento Pix

A confirmação do Pix segue três etapas sequenciais: solicitação da cobrança (`pix_solicitar`), envio do código/QR Code ao cliente (`pix_enviar_codigo`) e confirmação do pagamento (`pix_confirmar`), que atualiza o status do pedido e da transação no banco de dados.

## Tratamento de erros

| Código | Significado |
|---|---|
| 400 | Erro de validação no payload da requisição |
| 401 | Não autorizado |
| 403 | Acesso negado — privilégios insuficientes |
| 404 | Recurso não encontrado |
| 429 | Limite de requisições excedido |
| 500 | Erro inesperado no servidor |
