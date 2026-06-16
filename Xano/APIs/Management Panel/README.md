# 🛠️ API do Painel de Gestão

Documentação da API do painel administrativo do SLFood, desenvolvida no Xano. Responsável pela gestão de cardápio e funcionários, além do login de acesso ao painel.

## Endpoints

### `POST /login`

Realiza o login de um funcionário/administrador no painel de gestão, retornando token de autenticação e dados do usuário, incluindo seu papel no sistema.

**Autenticação:** não requerida

**Request body:**
```json
{
  "email": "user@example.com",
  "password": "string"
}
```

**Resposta de sucesso (200):**
```json
{
  "authToken": "string",
  "user_id": "string",
  "name": "string",
  "email": "string",
  "papel_id": "string",
  "papel": "string"
}
```

<img width="958" height="739" alt="image" src="https://github.com/user-attachments/assets/13c5730b-5d99-47ce-9fd2-8df643ad8bd2" />

---

### `GET /cardapio_listar`

Lista todos os produtos cadastrados no cardápio, usado pelo painel para exibir a gestão de itens.

**Autenticação:** não requerida

**Resposta de sucesso (200):**
```json
{
  "produtos": [
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
}
```

<img width="954" height="672" alt="image" src="https://github.com/user-attachments/assets/d6784a1e-49db-4352-b6c3-2bdcf5367a5d" />

---

### `POST /cardapio_criar`

Cria um novo item no cardápio do restaurante.

**Autenticação:** não requerida

**Request body:**
```json
{
  "nome": "string",
  "descricao": "string",
  "preco": 0,
  "url_imagem": "string"
}
```

<img width="955" height="772" alt="image" src="https://github.com/user-attachments/assets/f2d0a05b-9eec-4349-aa4a-fae0bf1e105a" />


---

### `GET /funcionarios_listar`

Lista todos os funcionários cadastrados, incluindo papel/permissão e status de verificação.

**Autenticação:** não requerida

**Resposta de sucesso (200):**
```json
{
  "resumo": "string",
  "funcionarios": [
    {
      "id": 0,
      "name": "string",
      "email": "string",
      "papel_id": 0,
      "is_verified": false
    }
  ]
}
```

<img width="958" height="661" alt="image" src="https://github.com/user-attachments/assets/5d369d83-07a5-44b4-8454-77c612f48bb2" />

---

### `POST /funcionario_criar`

Cadastra um novo funcionário no sistema, definindo seu papel/permissão de acesso.

**Autenticação:** não requerida

**Request body:**
```json
{
  "name": "string",
  "email": "user@example.com",
  "password": "string",
  "papel_id": 0
}
```

<img width="960" height="744" alt="image" src="https://github.com/user-attachments/assets/8ff8ff5a-fdfa-494f-83e7-875ae8fe23e1" />

---

## Controle de permissões

O campo `papel_id` define o nível de acesso de cada funcionário dentro do painel (ex: administrador, atendente, cozinha), permitindo restringir quais telas e ações cada perfil pode executar.

## Tratamento de erros

| Código | Significado |
|---|---|
| 400 | Erro de validação no payload da requisição |
| 401 | Não autorizado |
| 403 | Acesso negado — privilégios insuficientes |
| 404 | Recurso não encontrado |
| 429 | Limite de requisições excedido |
| 500 | Erro inesperado no servidor |
