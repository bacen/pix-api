# Changelog

Mudanças relevantes na API Pix serão documentadas aqui neste documento.

## [2.2.1]

### Corrigido:

* Os campos no objeto "devedor" no request do endpoint `PUT /cobv/{txid}` passam a ser opcionais.
Nem sempre o usuário recebedor tem a posse de todas as informações que constavam como obrigatórias.
* [[#307](https://github.com/bacen/pix-api/issues/307)]: Detalhada a semântica do campo `validadeAposVencimento`. Passa a apresentar redação 
detalhando o que ocorre em casos de exceção em que o vencimento da cobrança seja um final de semana 
ou um feriado juntamente com a atribuição de um valor pequeno para `validadeAposVencimento`. 
* [[#269](https://github.com/bacen/pix-api/issues/269)]. A regex do txid, na parte concernente ao tamanho, nos endpoints /pix e no callback webhook, 
estava errada. Corrigida de `{26,35}` para `{1,35}` porque pode haver a presença de pagamentos de QRs
estáticos nesses locais. 
* [[#270](https://github.com/bacen/pix-api/issues/270)]: O id do objeto `location` estava especificado como `int32`. De fato, apenas cerca de 2 bilhões
de possibilidades pode acabar muito rápido para grandes emissores de cobranças. Entendemos que o identificador do objeto `lotecobv`
se encaixa na mesma situação. Nesse sentido, alteramos de `int32` para `int64`, 
o que não deve causar maiores problemas no momento. 
* [[#249](github.com/bacen/pix-api/issues/249)], [[#250](github.com/bacen/pix-api/issues/250)]: Com a entrada do campo "chave" como identificador do webhook, toda a parte referente à paginação 
em GET /webhook perde a razão de existir. Nesse sentido, os parâmetros de busca "inicio" e "fim" passam 
a ser opcionais. O objeto de paginação "parametros", também torna-se opcional. 
* [[#239](github.com/bacen/pix-api/issues/239)]: Conforme relatado nesta discussão, entendemos que 
seria interessante, tanto sob o aspecto de segurança quanto sob o aspecto de funcionalidade, que o 
objeto pix agregue o atributo "chave", opcional.
* [[#241](https://github.com/bacen/pix-api/issues/241)]: Acrescentamos detalhes em relação à questão do acionamento do webhook por parte do PSP recebedor. 
* [[#294](https://github.com/bacen/pix-api/issues/294)]: Erro de ortografia. Na documentação, onde se lê `pixUrlAcessToken` deveria estar escrito `pixUrlAccessToken`. 
* [[#273](https://github.com/bacen/pix-api/issues/273)]: O texto do response 202 do endpoint `PATCH lotecobv/{id}` estava erroneamente induzindo o 
leitor a pensar que o lote já estava revisado quando, na verdade, estaria apenas em processamento 
* [[#273](https://github.com/bacen/pix-api/issues/273)]: Na lista de violações em lotecobv, havia indicações do endpoint `/lotecobv/{txid}`, o que inexiste. O correto é `/lotecobv/{id}`. 
* [[#316](https://github.com/bacen/pix-api/issues/316)]: Duas violações específicas foram removidas por questões de performance. 

## [2.2.0-rc.0]

### Adicionado:

- A API Pix agora estabelece uma série de erros padronizados seguindo a [RFC 7807](https://tools.ietf.org/html/rfc7807) reunidos na seção 
"Tratamento de erros". Procuramos ser exaustivos com relação aos possíveis erros semânticos.
- Adicionado o endpoint `PATCH /lotecobv/{id}`. Este endpoint pode ser utilizado quando a intenção do 
usuário recebedor for alterar cobranças específicas dentro do conjunto de cobranças criadas no lote em 
questão. O endpoint `PUT /lotecobv/{id}` também pode ser utilizado para alterar cobranças, mas deve
ser atribuído na requisição o array exatamente como especificado na requisição originária, o que torna 
este endpoint ineficiente no caso em que quer se alterar uma cobrança específica ou poucas dentro de um 
array com grande quantidade de cobranças.

- Incorporadas melhorias de redação em alguns endpoints específicos.

### Corrigido:

- adiciona o atributo `problema` no array `cobsv` no response do endpoint `GET /lotecobv/{id}`
- corrige os status `REMOVIDA_*`, que erroneamente vieram como `REMOVIDO_*` no branch 2.1.X. [#222](https://github.com/bacen/pix-api/issues/222)

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
