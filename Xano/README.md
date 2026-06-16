# 🗄️ Xano — Backend e Banco de Dados

Esta pasta documenta toda a estrutura de backend do SLFood, desenvolvida na plataforma Xano: banco de dados relacional, lógica de negócio e as APIs consumidas pelo app do cliente, pelo painel administrativo e pelo chatbot via n8n.

## Sobre a implementação

O backend foi inteiramente desenvolvido na plataforma Xano, utilizando seu motor de banco de dados relacional (PostgreSQL) para estruturar as entidades do sistema — clientes, produtos, pedidos, transações, funcionários e permissões — com integridade referencial entre elas.

A lógica de negócio foi separada por workspace/grupo de API conforme o consumidor final:

- **Autenticação** — cadastro, login e verificação de identidade do cliente.
- **Produção** — cardápio, criação de pedidos e fluxo completo de pagamento via Pix, consumida pelo app do cliente.
- **Chatbot (N8N)** — versão da API consumida pelos fluxos de automação do n8n, que conectam o agente de IA ao bot do Telegram.
- **Painel** — gestão de cardápio, funcionários e login de acesso administrativo.

Essa separação permitiu manter responsabilidades isoladas por contexto de uso, facilitando o controle de permissões e a manutenção de cada grupo de endpoints de forma independente.

## Documentação detalhada

Cada API possui seu próprio README dentro da pasta `APIs/`, com a lista completa de endpoints, exemplos de request/response e espaço para prints da documentação interativa do Xano.

## Modelagem do banco de dados

*(Espaço reservado para o diagrama de entidade-relacionamento — DER)*

<img width="1071" height="787" alt="image" src="https://github.com/user-attachments/assets/6400a59e-19c0-4cef-b9b3-3c3b1ea49818" />
<img width="1099" height="792" alt="image" src="https://github.com/user-attachments/assets/951bf77a-fa3a-4bd8-a99b-ff9de16c621f" />


## Observação de segurança

As URLs reais das instâncias do Xano foram removidas/mascaradas de toda a documentação publicada neste repositório. Endpoints de uso interno ou desenvolvimento (como rotinas de seed de dados) não foram incluídos na documentação pública. Os arquivos de especificação completos (OpenAPI/XanoScript) disponibilizados aqui passaram por revisão antes da publicação.
