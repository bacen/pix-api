# Changelog

Mudanças relevantes na API Pix serão documentadas aqui neste documento.

## [2.1.2]

- Readme: corrige informações sobre os Manuais
- [#172](https://github.com/bacen/pix-api/issues/172): corrige campos de cobv.devedor na exibição do Payload JSON que não estavam aderentes com o Manual de Iniciação
- [#171](https://github.com/bacen/pix-api/issues/171): corrige descrição do campo cobsv[n].criacao

## [2.1.1]

### Corrigido:

- Readme: adiciona menção ao Manual de Padrões para iniciação do Pix.
- [#168](https://github.com/bacen/pix-api/issues/168): corrige descrição do endpoint webhook.

## [2.1.0-rc.5, 2.1.1]

### Adicionado

- A API agora apresenta Endpoints para gerenciamento de _Cobranças com Vencimento_
- Cobranças com vencimento dispõem de seu próprio endpoint
- A API agora apresenta Endpoints para gerenciamento de Lotes de _Cobranças com Vencimento_
- Adicionado um endpoint para criação de cobrança imediata com txid criado pelo PSP recebedor
- Adicionados Endpoints para o gerenciamento de _Locations_, habilitando o caso de uso "Reuso de Locations".
- Adicionado campo para descrição complementar do status da devolucão [#148](https://github.com/bacen/pix-api/issues/148)

### Correções

- removido o objeto __opcional__ pix.pagador [#153](https://github.com/bacen/pix-api/issues/153)
- os webhooks agora são associados a uma chave pix [#120](https://github.com/bacen/pix-api/issues/120)
- os endereços dos endpoints agora apresentam corretamente o fragmento `v2` [#3](https://github.com/bacen/pix-api/issues/3)

## [2.1.0-rc.4]

### Correções

- removido endpoint `DELETE /cob/{txid}/loc`, uma vez que o endpoint PATCH cobre a situação. [#108](https://github.com/bacen/pix-api/issues/108)

## [2.1.0-rc.3]

### Correções

- removido txid opcional no response do endpoint `POST /loc` [#104](https://github.com/bacen/pix-api/issues/104),[#106](https://github.com/bacen/pix-api/issues/106)

## [2.1.0-rc.2]

### Correções

- corrigido array _required_ de CobSolicitada [#100](https://github.com/bacen/pix-api/issues/100)

## [2.1.0-rc.1]

### Correções

- corrigido exemplo JWS da tag cobPayload

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
