# 🤖 N8N — Automação do Chatbot Telegram

Esta pasta documenta a automação do chatbot de atendimento do SLFood, construída no n8n e integrada ao Telegram. O chatbot permite que o cliente faça pedidos, gere pagamento via Pix, consulte status do pedido e tire dúvidas com suporte automatizado por IA — tudo diretamente pela conversa no Telegram.

## Visão geral

O backend oficial do sistema permanece no Xano, responsável por armazenar e controlar pedidos, itens, transações e status. O n8n atua como camada de automação, orquestrando a comunicação entre Telegram, Xano, Asaas (gateway de pagamento Pix) e o agente de IA.

A automação foi dividida em quatro fluxos independentes, separados por responsabilidade, o que facilita manutenção, testes e evolução do sistema.

## Fluxos

### 01 — Gerenciador Telegram

Porta de entrada do chatbot. Recebe todas as interações enviadas pelo cliente — mensagens digitadas e cliques em botões — identifica o tipo de entrada e direciona para o fluxo correto: pedido ou suporte. Não executa regras de negócio diretamente, apenas roteia a conversa.

<img width="1398" height="746" alt="image" src="https://github.com/user-attachments/assets/1f58ce35-2b6a-40da-881c-65b6b11348be" />

---

### 02 — Fluxo de Pedido

Conduz o cliente durante todo o processo de compra: escolha de categoria e produto, definição de quantidade, montagem do carrinho e finalização do pedido. O cardápio é consultado diretamente no Xano, e o carrinho temporário é armazenado em Data Tables do próprio n8n, evitando misturar dados de conversa com o banco principal antes da finalização.

Ao finalizar o pedido, o fluxo cria o registro oficial no Xano e, ao optar por pagamento via Pix, gera a cobrança e envia o código Pix copia-e-cola ao cliente. A sessão do pedido é então marcada como `aguardando_pagamento`.

<img width="1560" height="790" alt="image" src="https://github.com/user-attachments/assets/853a8ce7-c57c-4372-9950-e4ecd68702c2" />

---

### 03 — Suporte com IA

Responsável pelo atendimento automatizado de dúvidas gerais: cardápio, endereço, telefone, horário de funcionamento, formas de pagamento e status de pedido.

O fluxo primeiro classifica a intenção da mensagem. Se o cliente pergunta sobre o status de um pedido informando o número, a consulta é feita diretamente no Xano. Para dúvidas gerais sobre o restaurante, o agente de IA consulta uma base de conhecimento estruturada em Google Sheets antes de responder — reduzindo o risco de respostas genéricas ou inventadas.

<img width="1101" height="761" alt="image" src="https://github.com/user-attachments/assets/ca132606-9041-4462-ad7b-d458f0922f7e" />

---

### 04 — Confirmação de Pagamento Pix

Fluxo dedicado à confirmação do pagamento Pix. Recebe o número do pedido e o chat do Telegram, atualiza os status oficiais no Xano (pedido e transação), envia a confirmação ao cliente e finaliza a sessão temporária no n8n — encerrando corretamente o ciclo daquele pedido.

<img width="1815" height="302" alt="image" src="https://github.com/user-attachments/assets/91e9967d-7bce-4b86-8a75-f2f3cb66b519" />

---

## Integrações utilizadas

| Serviço | Função |
|---|---|
| **Telegram** | Canal de atendimento e interação com o cliente |
| **n8n** | Orquestração dos fluxos, controle de sessões e chamadas de API |
| **Xano** | Backend principal — pedidos, itens, transações e status |
| **Asaas (Sandbox)** | Geração de cobranças Pix para simulação de pagamento |
| **Google Sheets** | Base de conhecimento consultada pelo agente de IA |
| **Gemini** | Modelo de IA utilizado no atendimento automatizado |

## Organização dos dados

O sistema separa os dados conforme sua finalidade, evitando misturar informações temporárias de conversa com dados oficiais:

- **Xano** — dados oficiais: pedidos, itens, clientes, transações, status e produtos.
- **n8n Data Tables** — dados temporários: sessão do pedido, carrinho temporário e sessão de suporte.
- **Google Sheets** — informações consultáveis pela IA: dados do restaurante, cardápio e FAQ.

## Resumo do fluxo completo

O cliente inicia a conversa no Telegram, e o Gerenciador identifica se a intenção é pedido ou suporte. No fluxo de pedido, o cliente navega pelo cardápio, monta o carrinho, finaliza a compra, gera o Pix e aguarda a confirmação de pagamento — que atualiza o status no Xano e encerra a sessão. No fluxo de suporte, a IA consulta o status do pedido (quando solicitado) ou a base de conhecimento do restaurante para responder dúvidas com informações reais, evitando respostas genéricas.

## Situação atual

O fluxo de pedido foi validado com sucesso de ponta a ponta: criação de pedido, geração de Pix via Asaas, envio do código ao cliente e confirmação de pagamento. O fluxo de suporte também foi validado, consultando status real no Xano e utilizando o Google Sheets como base de conhecimento da IA.

## Demonstração

Vídeo completo demonstrando o funcionamento dos fluxos em ação: **https://www.youtube.com/watch?v=CUaZDK-gNWA**
