# 📱 App do Cliente

Aplicativo do cliente desenvolvido em FlutterFlow, contemplando o fluxo completo de autenticação, navegação pelo cardápio, carrinho e finalização de pedido, integrado ao backend via API.

## Conteúdo

- **Fluxograma de telas** — mapa completo de navegação do app, construído no FlutterFlow, cobrindo desde o cadastro/login até o acompanhamento do pedido.

## Lógica do App (FlutterFlow)

O aplicativo não foi montado apenas no nível visual: toda a lógica de funcionamento foi estruturada utilizando os principais recursos do FlutterFlow para conectar telas, dados e backend de forma consistente.

- **API Calls** — todas as integrações com o backend (Xano) foram configuradas como chamadas de API dentro do próprio FlutterFlow. Isso inclui autenticação de usuário (cadastro, login e verificação de código por e-mail), busca e listagem do cardápio, criação e atualização de pedidos, gerenciamento de endereços e processamento de pagamento via Pix e cartão. Cada chamada foi mapeada com seus parâmetros de entrada, headers de autenticação e tratamento da resposta retornada pela API.

- **Custom Actions** — utilizadas para lógicas que precisavam rodar diretamente no app, sem depender de uma chamada ao backend. Isso inclui validações de formulário (e-mail, senha, campos obrigatórios), formatação de dados (valores monetários, máscaras de campo), cálculos auxiliares (como total do carrinho antes de enviar o pedido) e pequenas regras de negócio aplicadas no momento da interação do usuário.

- **App State** — variáveis de estado global que mantêm informações entre as diferentes telas do app, evitando que o usuário perca dados ao navegar. Inclui o estado do usuário autenticado, os itens adicionados ao carrinho, o endereço selecionado para entrega e o status do pedido em andamento.

- **Data Schema** — estrutura de tipos de dados (data types) criada no FlutterFlow para representar de forma padronizada as entidades do sistema, como produto, pedido, endereço, forma de pagamento e usuário. Esses schemas garantem que os dados recebidos das API Calls sejam consumidos de forma consistente em todas as telas do app.

## Telas principais

Cadastro, login, recuperação de senha, verificação de código por e-mail, listagem de cardápio, carrinho, cadastro de endereço, checkout, pagamento via Pix (com QR Code) e cartão, confirmação e acompanhamento de pedido.

## Observação

As imagens desta pasta foram produzidas em conjunto com o grupo do projeto.
