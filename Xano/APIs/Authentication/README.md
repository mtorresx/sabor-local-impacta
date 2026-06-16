# 🔐 API de Autenticação

Documentação da API de autenticação do SLFood, desenvolvida no Xano. Responsável por todo o fluxo de cadastro, login e verificação de identidade do usuário antes do acesso ao restante do sistema.

## Endpoints

### `POST /auth/login`

Realiza o login do usuário com e-mail e senha, retornando um token de autenticação (JWT) utilizado nas demais requisições autenticadas.

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
  "authToken": "string"
}
```

<img width="1154" height="850" alt="image" src="https://github.com/user-attachments/assets/c46923a2-e164-4179-966d-9b93b6da111d" />


---

### `GET /auth/me`

Retorna os dados do usuário autenticado a partir do token enviado no header da requisição.

**Autenticação:** requerida (Bearer Token)

**Resposta de sucesso (200):**
```json
{
  "id": 0,
  "created_at": "now",
  "name": "string",
  "email": "user@example.com",
  "papel_id": 0
}
```

O campo `papel_id` referencia o papel/permissão do usuário no sistema (cliente, funcionário ou administrador), utilizado no controle de acesso do painel de gestão.

<img width="1147" height="722" alt="image" src="https://github.com/user-attachments/assets/cb182ffe-3764-4b5d-a970-52c800b4011c" />


---

### `POST /auth/signup`

Realiza o cadastro de um novo usuário no sistema.

**Autenticação:** não requerida

**Request body:**
```json
{
  "name": "string",
  "email": "user@example.com",
  "password": "string",
  "celular": "string",
  "cpf": "string"
}
```

**Resposta de sucesso (200):**
```json
{
  "user_id": "string"
}
```

Após o cadastro, o usuário recebe um código de verificação por e-mail, validado pelo endpoint `/verify_code` antes da liberação total do acesso.

<img width="1147" height="880" alt="image" src="https://github.com/user-attachments/assets/7b760c3e-f317-4920-a1bb-71e90db0ef0b" />


---

### `POST /verify_code`

Valida o código de verificação enviado por e-mail durante o cadastro, confirmando a identidade do usuário.

**Autenticação:** não requerida

**Request body:**
```json
{
  "user_id": 0,
  "codigo_digitado": 0
}
```

**Resposta de sucesso (200):**
```json
{
  "message": "string"
}
```

<img width="1144" height="847" alt="image" src="https://github.com/user-attachments/assets/557e36d9-8d88-4be3-8cc5-be198d23297d" />


---

## Tratamento de erros

Todos os endpoints seguem o padrão de respostas de erro do Xano:

| Código | Significado |
|---|---|
| 400 | Erro de validação no payload da requisição |
| 401 | Não autorizado |
| 403 | Acesso negado — privilégios insuficientes |
| 404 | Recurso não encontrado |
| 429 | Limite de requisições excedido |
| 500 | Erro inesperado no servidor |
