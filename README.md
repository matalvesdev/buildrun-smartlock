# Conhecendo o projeto Smart Stock

Neste projeto, apresento o **Smart Stock**, uma solução que desenvolvi para automatizar o processo de recompra de itens em uma empresa de e-commerce. Antes da automação, eu precisava realizar o processo de recompra manualmente: sempre que a quantidade de um item no estoque caía abaixo do nível mínimo, era necessário negociar diretamente com o setor de compras.

Com o **Smart Stock**, construí uma aplicação Spring Boot para automatizar todo esse fluxo. Agora, o sistema executa as seguintes etapas:

- Leio um arquivo CSV gerado por um sistema legado, contendo os dados de estoque;
- Aplico regras de negócio para identificar automaticamente os itens que precisam ser repostos;
- Integro com a API do setor de compras, utilizando um token de autenticação para garantir a segurança da comunicação;
- Persisto os dados no MongoDB para acompanhamento e auditoria.

Ao final deste processo, compreendo claramente o problema, os objetivos do projeto e as principais tecnologias aplicadas durante o desenvolvimento do Smart Stock.

## Regras de Negócio

- Consumo diariamente o arquivo em formato CSV, que contém os seguintes campos:
  - `item_id` (uuid)
  - `item_name`
  - `quantity`
  - `reorder_threshold`
  - `supplier_name`
  - `supplier_email`
  - `last_stock_update_time`
- Sempre que um item fica abaixo da quantidade mínima em estoque, solicito a recompra com a quantidade mínima acrescida de 20% de margem de segurança.
- Para interagir com a API do Setor de Compras, faço:
  - Autenticação na API;
  - Realizo a chamada utilizando o token obtido na etapa de autenticação.
- Mantenho registrado todos os itens para os quais solicitei recompra, armazenando:
  - Identificação do Item
  - Nome do Item
  - Quantidade em estoque
  - Quantidade mínima de itens no estoque
  - Nome do Fornecedor
  - E-mail do Fornecedor
  - Última atualização do item no estoque
  - Quantidade de recompra solicitada
  - Indicativo se a recompra foi enviada com sucesso ou falha
  - Data e hora do envio da solicitação de recompra

---

Com o **Smart Stock**, consegui automatizar e tornar muito mais eficiente o controle de estoque e o processo de recompra, reduzindo falhas humanas e otimizando o tempo do processo.
