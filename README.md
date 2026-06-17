# 🍛 Sabor Local / SLFood

Plataforma própria de delivery desenvolvida para reduzir a dependência de marketplaces terceiros, com aplicativo do cliente, painel administrativo, backend relacional, automações e chatbot com IA. Projeto acadêmico — **2º lugar** na entrega final.

![Status](https://img.shields.io/badge/status-concluído-success)
![Tipo](https://img.shields.io/badge/tipo-projeto%20acadêmico-blue)
![Resultado](https://img.shields.io/badge/resultado-2º%20lugar-yellow)

---

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Arquitetura](#-arquitetura)
- [Funcionalidades](#-funcionalidades)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Demonstração](#-demonstração)
- [Melhorias Futuras](#-melhorias-futuras)
- [Aprendizados](#-aprendizados)
- [Estrutura do Repositório](#-estrutura-do-repositório)

---

## 📌 Sobre o Projeto

O Sabor Local é um projeto acadêmico que propõe uma solução de delivery própria para restaurantes de culinária regional mineira. O problema central abordado foi a dependência excessiva de plataformas de delivery de terceiros, que cobram taxas elevadas sobre cada pedido, reduzem a margem de lucro do restaurante, limitam o controle sobre a experiência do cliente e restringem o acesso a dados estratégicos do próprio negócio.

O ponto de partida foi um escopo completo de projeto, com solicitações detalhadas, modelagem de dados, regras de negócio e requisitos já definidos. O trabalho da equipe foi transformar esse escopo em uma solução real, integrada e funcional: o **SLFood**.

A solução foi pensada para devolver ao restaurante o controle sobre sua operação digital — desde o relacionamento direto com o cliente até a gestão interna de pedidos, cardápio e equipe, passando por automações de atendimento via inteligência artificial.

O projeto contemplou todo o ciclo de desenvolvimento de produto: levantamento de requisitos, definição de regras de negócio, modelagem de dados, arquitetura de integrações, prototipação em Figma, desenvolvimento em FlutterFlow, backend em Xano e automações em n8n.

**Minha responsabilidade no time** foi a estruturação do banco de dados relacional, a criação das APIs no Xano e a montagem da automação no n8n — a camada que conecta o app, o backend e o chatbot.

---

## 🏗️ Arquitetura

A arquitetura do SLFood foi estruturada em camadas integradas por API, combinando ferramentas low-code/no-code com automações orientadas a eventos:

- **Frontend (App do Cliente e Painel de Gestão):** desenvolvidos em FlutterFlow, consumindo a API do backend para autenticação, listagem de cardápio, carrinho, criação de pedidos, pagamento, gestão de cardápio, funcionários e permissões.
- **Backend/API:** construído no Xano, responsável pela lógica de negócio, autenticação e exposição dos endpoints consumidos pelo app, pelo painel e pelo chatbot.
- **Banco de Dados:** modelo relacional no próprio Xano, estruturado para suportar clientes, pedidos, itens de cardápio, funcionários, permissões e transações.
- **Automação e Atendimento:** fluxos no n8n conectando o bot do Telegram a um agente de IA, capaz de consultar informações do cardápio e do restaurante para responder o cliente.
- **Pagamentos:** integração de fluxo de pagamento via Pix e cartão, conectada ao processo de finalização de pedido.

Essa combinação permitiu validar, em escala acadêmica, uma arquitetura orientada a eventos e integrações via API entre ferramentas distintas — sem a necessidade de desenvolver cada camada do zero em código tradicional.

---

## ✅ Funcionalidades

### App do Cliente
- Cadastro de cliente
- Login
- Listagem de cardápio com imagem, descrição e preço
- Carrinho de compras
- Geração de pedido
- Pagamento via Pix
- Pagamento via cartão

### Painel Administrativo
- Cadastro de funcionários
- Controle de permissões por papel
- Gestão de cardápio
- Painel de acompanhamento de pedidos

### Automação e Suporte
- Chatbot de atendimento via Telegram
- Agente de IA com consulta a informações do restaurante e do cardápio

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Uso no projeto |
|---|---|
| **FlutterFlow** | Desenvolvimento do app do cliente e painel administrativo |
| **Xano** | Backend, banco de dados relacional e APIs |
| **n8n** | Automação de fluxos e orquestração de integrações |
| **Telegram Bot** | Canal de atendimento ao cliente |
| **Agente de IA** | Suporte automatizado com consulta a dados do restaurante |
| **Figma** | Prototipação e design das telas |
| **GitHub** | Versionamento e documentação do projeto |

---

## 🎥 Demonstração

Vídeo demonstrando o funcionamento completo dos fluxos do chatbot via Telegram disponível na pasta `N8N/`.

Imagens das telas, fluxos e documentação técnica de cada módulo estão organizadas nas pastas `Design/`, `FlutterFlow/`, `Xano/` e `N8N/`.

---

## 🚧 Melhorias Futuras

> As funcionalidades abaixo **não foram implementadas** nesta entrega. Estão listadas como evoluções previstas para versões futuras do projeto.

- **Rastreamento em tempo real / logística com Google Maps:** não implementado nesta versão devido a limitações de custo e complexidade de integração.
- Expansão das opções e integrações de pagamento.
- Refinamento de relatórios e indicadores estratégicos no painel administrativo.

---

## 🎓 Aprendizados

- Integração entre ferramentas low-code/no-code (FlutterFlow, Xano, n8n) e como elas se comunicam via API.
- Modelagem de banco de dados relacional aplicada a um cenário real de negócio (delivery).
- Construção de fluxos orientados a eventos para automação de atendimento.
- Integração de um agente de IA a um canal de comunicação (Telegram) com consulta a dados específicos do negócio.
- Importância da documentação de requisitos e regras de negócio para guiar decisões técnicas.
- Arquitetura bem pensada em ambientes low-code exige o mesmo rigor de raciocínio que em desenvolvimento tradicional — a complexidade só se desloca de lugar, não desaparece.

---

## 📁 Estrutura do Repositório

```
sabor-local-impacta/
├── Design/         # Telas, fluxos e design system criados no Figma
├── FlutterFlow/    # App do cliente e painel administrativo
├── Xano/           # Backend, banco de dados e documentação das APIs
├── N8N/            # Automação do chatbot via Telegram (fluxos JSON e vídeo demonstrativo)
├── .gitignore
└── README.md
```

---

## 📄 Licença

Este é um projeto acadêmico desenvolvido para fins de aprendizado.
