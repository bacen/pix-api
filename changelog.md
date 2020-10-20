# Changelog

Mudanças relevantes na API Pix serão documentadas aqui.

## [2.1.0-rc.0] 

### Novidades

- Endpoint para criação de "Locations"; os locations, denotados por `fdqnPSPRecebedor/pixEndpoint/pixUrlAccessToken`, podem ser utilizados para exibir cobranças, de acordo com a vontade do usuário recebedor, mas apenas uma por vez. O location em `PUT /cob/{txid}` é um objeto que pode ser atribuído pelo usuário recebedor.
- A cobrança agora suporta o conceito de "Vencimento", juntamente com as funcionalidades correlatas: juros, multa, descontos, abatimentos e afins.
- O formato do txid foi revisado: o tamanho do txid do estático é diferente do tamanho do txid dinâmico.

### Correções

- Endpoints que criam recursos deveriam retornar 201 created. [#85](https://github.com/bacen/pix-api/issues/85)
- Removidas menções ao o endpoint /refresh. [#48](https://github.com/bacen/pix-api/issues/48)
- API começa em v2 e acompanha a major version [#3](https://github.com/bacen/pix-api/issues/3)
- revisados exemplos inconsistentes.

## [2.0.0] 

### Adicionado
- Endpoint para criação de Cobranças
- Endpoint para gerenciamento de Cobranças
- Endpoint para consulta parametrizada de Cobranças
- Endpoint para gerenciamento de Pix
- Endpoint para consulta parametrizada de Pix
- Endpoint para solicitar devolução de Pix
- Endpoint para consultar devolução de Pix
- Endpoint para configurar Webhooks
- Endpoint para exibir informações de Webhooks
- Endpoint para cancelar Webhooks
- Endpoint para acesso ao Payload JSON de Cobrança
- Autenticação e Autorização baseada em OAuth2

### Removido
- Recursos para gerenciamento de Documentos
- Configuração de vencimento em calendário
- Configuração de juros, multa e desconto em valor
