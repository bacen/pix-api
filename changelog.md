# Changelog

Mudanças relevantes na API Pix serão documentadas aqui neste documento.

## [2.9.0]

- Atualização do padrão de campos com domínio `CNPJ` para aceitar valores alfanuméricos, conforme Instrução Normativa RFB nº 2229, de 15 de outubro de 2024.
- Atualização dos padrões dos campos `ispbParticipante` e `prestadorDoServicoDeSaque` para permitir valores alfanuméricos, considerando que o `ISPB` pode ser derivado do respectivo `CNPJ`.
- Atualização dos padrões dos campos `idRec` e `idSolicRec` para permitir valores alfanuméricos nos componentes `xxxxxxxx` (ISPBs) das suas regras de formação.
- Correção na descrição do campo `idRec`.
- Correção nos campos `cob.devedor` e `cobv.devedor` removendo campos duplicados.
- Correção nas violações de `CobVOperacaoInvalida` removendo informações duplicadas.


## [2.8.2]
- Ajuste na descrição do `PUT /webhookrec`.
- Correção nas informações do parâmetro `status` em `GET /cobr` que se refere ao status da cobrança recorrente.
- Ajuste das propriedades `encerramento.rejeicao.descricao` e `encerramento.cancelamento.descricao` nas recorrências e cobranças recorrentes para o tamanho máximo de `400` caracteres.
- Ajuste da propriedade `tentativas.rejeicao.descricao` das cobranças recorrentes para o tamanho máximo de `400` caracteres.
- Nas tags `RecPayload` e `Rec` substituímos a expressão `encerrada` por `expirada, cancelada ou rejeitada`.

## [2.8.1]

- Inclusão do campo não obrigatório `rec.recebedor.convenio` no request do `POST /rec` e response do `GET /rec`, `GET /rec/{idRec}` e `POST /rec`.
- Inclusão do parâmetro de busca não obrigatório `convenio` no `GET /rec`, `GET /cobr` e `GET /locrec`.
- Inclusão de exemplo de uso do campo `convenio` no response do `GET /rec/{idRec}`. 
- Inclusão da obrigatoriedade do campo `rec.recebedor` no response do GET `/rec` e GET `/rec/{idRec}` .
- Inclusão do campo não obrigatório `cobr.tentativas.rejeicao` no response do `GET /cobr`, `GET /cobr/{txid}` e `POST /cobr/{txid}/retentativa/{data}`.
- Ajuste na descrição dos campos `cobr.ajusteDiaUtil` e `cobr.calendario.dataDeVencimento`.
- Pequenos ajustes de texto na seção `Tratamento de Erros`.
- Inclusão de violações para o endpoint `GET /rec/{idRec}`.
- Ajuste nas violações do endpoint `PATCH /solicrec/{idSolicRec}`.
- Remoção do campo `tipoCob` do response do DELETE `/locrec/{id}/idrec`.
- Ajuste no exemplo do response do DELETE `/locrec/{id}/idrec`.

## [2.8.0]

- Correção do campo `destinatario` de opcional para obrigatório no schema da `Solicitação de Recorrência` do `POST /solicRec`.
- Remoção do campo `recebedor`, desnecessário, do exemplo em `POST /rec`.
- Incluída a obrigatoriedade dos campos `parametros` e `cobrs` no `GET /cobr` para seguir o comportamento similar ao existente para as demais consultas de outras entidades.
- Incluída a obrigatoriedade dos campos `parametros` e `recs` no `GET /rec` para seguir o comportamento similar ao existente para as demais consultas de outras entidades.
- Pequenos ajustes de texto na seção `Tratamento de Erros`.
- Ajuste do exemplo na retentativa quando a política não permite, lançando erro 400.
- Ajuste nas descrições dos identificadores de recorrência e solicitação de recorrência.

## [2.7.0]

- Inclusão do campo `rec.dadosQR` contendo os campos `pixCopiaECola` e `jornada` referentes ao response do GET `/rec/{idRec}?txid={txid}` fornecendo informações complementares relacionadas a respectiva jornada e QRCode com exemplos.
- Remoção do campo `rec.pagador` no response do POST `/rec` e PATCH `/rec/{idRec}`.
- Remoção do campo `rec.cobr` no response do GET `/rec` e GET `/rec/{idRec}` e inserido `idRec` como parâmetro de busca em GET `/cobr`.
- Ajuste no campo `cobr.dadosDevedor` substituído por `cobr.devedor`.
- Ajuste no campo `cobr.contaRecebedor` substituido por `cobr.recebedor`.
- Ajuste no campo `cobr.valor` substituido por `cobr.valor.original`.
- Ajuste no campo `cobr.ajusteDiaUtil` para valor default `true`.
- Inclusão do campo `cobr.vinculo.devedor.nome` no request do PATCH `/cobr/{txid}`.


## [2.7.0-RC1]

- Inclusão das tags relacionadas ao Pix Automático:
  -	`RecPayload`: que reúne os endpoints (locations) utilizados pelo software do PSP pagador para recuperar o payload JSON que representa uma recorrência;
  - `Rec`: que reúne os endpoints destinados a lidar com o gerenciamento de recorrências;
  - `SolicRec`: que reúne os endpoints destinados a lidar com o gerenciamento de solicitações de confirmação de recorrências;
  - `CobR`: que reúne os endpoints destinados a lidar com o gerenciamento de cobranças associadas a uma recorrência;
  - `PayloadLocationRec`: que reúne os endpoints destinados a lidar com a configuração e a remoção de locations para uso dos payloads de recorrências;
  - `WebhookRec`: que reúne os endpoints para o gerenciamento de notificações de recorrências por parte do PSP recebedor ao usuário recebedor; e
  - `WebhookCobR`: que reúne os endpoints para o gerenciamento de notificações de cobranças recorrentes por parte do PSP recebedor ao usuário recebedor.

## [2.6.3]

- Inclusão de esclarecimento referente ao domínio `AGPSS` do campo `modalidadeAgente` para Pix Saque e Pix Troco, dispondo que ele deve ser convertido para `AGFSS` na elaboração da mensagem `pacs.008`. Optou-se pela não alteração desse domínio (para `AGFSS`) na API Pix neste momento, ficando a uniformização com o Catálogo de Mensagens do SPI reservada para a próxima *major version* da API Pix.
- Descontos em cobranças com vencimento agora podem ser aplicados para datas **menores ou iguais** à data de vencimento.
- Correção dos exemplos `F` e `G` conforme apontado na issue [[#485](https://github.com/bacen/pix-api/issues/485)].
- Uniformização das descrições dos campos `/lotecobv/{id}` do request e `id` no response do GET `/lotecobv/{id}` que semânticamente são o mesmo valor.
- Remoção do 'pagador' como campo obrigatório do 'Pix' no *seu respectivo schema*.

## [2.6.2]

- Inclusão do valor `AGTOT` no domínio do campo `valor.retirada.troco.modalidadeAgente`.
- Ajuste da descrição do valor domínio `AGTOT` de 'Agente Outra Espécie de Pessoa Jurídica' para 'Agente Outra Espécie de Pessoa Jurídica ou Correspondente no País'.
- Exclusão do valor `AGPSS` dos domínios dos campos `PixValorTroco.troco.modalidadeAgente` e `CobPayload.valor.retirada.troco.modalidadeAgente`.
- Substituição da expressão 'Prestador de Serviços de Saque' por 'Facilitador de Serviço de Saque' em linha com a nova instrução normativa.
- Correção do exemplo '*cobrança com troco alterável*' para inclusão da estrutura `retirada`.
- Correção do exemplo '*troco com valor.original alterável*', estrutura `retirada.troco` com `AGTOT`.

## [2.6.1]

- Restrição da `modalidadeAgente` do Pix Troco para aceitar somente `AGTEC`.
- Ajustes nos endpoints de Devolução para os diferentes tipos de natureza relacionados aos códigos `BE08` e `FR01`.
- Indicação tamanho máximo do campo `pixCopiaECola` [[#457](https://github.com/bacen/pix-api/issues/457)].

## [2.6.0]

- Inclusão e referenciamento de "Status do registro de cobrança" onde lia-se "Status da Cobrança" com a descrição da semântica de cada estado.
- Inclusão do campo `pixCopiaECola` (opcional) correspondente às cobranças.
- Na listagem `componentesValor` do objeto `Pix` foram incluídas as informações relativas aos juros, multas, descontos e abatimentos quando o Pix se refere a um pagamento de cobrança com vencimento. Tendo assim o detalhamento em caso de antecipações ou atrasos no pagamento.
- Inclusão do campo `descricao` nos objetos que tratam de Devoluções.
- Ajuste na descrição do campo `natureza` nas Devoluções.

## [2.5.0]

- Inclusão do atributo `retirada` como campo opcional do objeto `valor` nos endpoints de consulta, criação e revisão da cobrança imediata. O campo pode ser preenchido com os atributos `saque` ou `troco` exclusivamente, detalhados pelos atributos `valor` e `modalidadeAlteracao`. Se apresentarem o campo `modalidadeAlteracao` como valor 1, significa que o usuário pagador pode alterar o valor do saque ou troco.
  Em sua ausência, assume-se o valor 0, que significa que o valor do saque ou troco não pode ser alterado.
- Inclusão do atributo `componentesValor` como campo opcional nos endpoints de consulta Pix para informações da composição do valor final do Pix, este será detalhado por um array de objetos compostos por `tipo` e `valor`.
- Formatações gerais de referências a campos, objetos e schemas.
- Inclusão do domínio `natureza` nas devoluções para diferenciamento de devoluções de Pix comuns, ou oriundos de Saque/Troco.
- Referências a https://www.bcb.gov.br/estabilidadefinanceira/pagamentosinstantaneos trocadas por https://www.bcb.gov.br/estabilidadefinanceira/pix.

## [2.4.0]

- Não houve mudança. Versão seguiu para 2.5.0 para acompanhar o Manual de Iniciação.

## [2.3.0]

- `modalidadeAlteracao` agora é um campo opcional do objeto `valor`
  no payload da cobrança imediata e nos endpoints de criação e revisão da cobrança imediata.
  Se apresentado como valor 1, significa que o usuário pagador pode alterar o valor da cobrança.
  Em sua ausência, assume-se o valor 0, que significa que a cobrança não pode ser alterada.
- Não é mais obrigatório que o fragmento de versão v2 esteja presente na _location_.
  Não há problema em manter o fragmento; este será considerado como parte integrante da _location_.
- [[#348](https://github.com/bacen/pix-api/issues/348)]: corrige case do padrão de datas de `yyyy-mm-dd` -> `YYYY-MM-DD`.
- [[#354](https://github.com/bacen/pix-api/issues/354)]: Aprimora a descrição do webhook detalhando
  a ativação em caso de devolução de um pix. O callback deve ser ativado, também, no caso de serem atingidos
  os status finais da devolução: "devolvido" e "não realizado".
- [[#356](https://github.com/bacen/pix-api/issues/356)]: Adiciona dois cenários de erro para o endpoint
  `PUT /pix/{e2eid}/devolucao/{id}` na seção de tratamentos de erros.
- [[#357](https://github.com/bacen/pix-api/issues/357)]: aprimora a descrição do campo "motivo" no retorno do endpoint
  `​/pix​/{e2eid}​/devolucao​/{id}`.

## [2.2.2]

- [[#331](https://github.com/bacen/pix-api/issues/331)]: O campo `validadeAposVencimento` estava constando como `opcional`, na resposta da criação da cobrança, um efeito colateral da correção correlata ocorrida na release 2.2.1.
- [[#334](https://github.com/bacen/pix-api/issues/334)]: adicionados detalhes a respeito da manipulação da revisão da cobrança em cenário de alteração do _location_.
- [[#342](https://github.com/bacen/pix-api/issues/342)]: removidos trechos duplicados na seção de tratamento de erros.

## [2.2.1]

### Corrigido:

- Os campos no objeto "devedor" no request do endpoint `PUT /cobv/{txid}` passam a ser opcionais.
  Nem sempre o usuário recebedor tem a posse de todas as informações que constavam como obrigatórias.
- [[#307](https://github.com/bacen/pix-api/issues/307)]: Detalhada a semântica do campo `validadeAposVencimento`. Passa a apresentar redação
  detalhando o que ocorre em casos de exceção em que o vencimento da cobrança seja um final de semana
  ou um feriado juntamente com a atribuição de um valor pequeno para `validadeAposVencimento`.
- O campo `validadeAposVencimento` estava constando como `required`, o que estava incorreto.
  Quando não preenchido, o PSP recebedor assume o valor deste campo como 30, então não há motivos para
  o campo ser obrigatório.
- [[#269](https://github.com/bacen/pix-api/issues/269)]. A regex do txid, na parte concernente ao tamanho, nos endpoints /pix e no callback webhook,
  estava errada. Corrigida de `{26,35}` para `{1,35}` porque pode haver a presença de pagamentos de QRs
  estáticos nesses locais.
- [[#270](https://github.com/bacen/pix-api/issues/270)]: O id do objeto `location` estava especificado como `int32`. De fato, apenas cerca de 2 bilhões
  de possibilidades pode acabar muito rápido para grandes emissores de cobranças. Entendemos que o identificador do objeto `lotecobv`
  se encaixa na mesma situação. Nesse sentido, alteramos de `int32` para `int64`,
  o que não deve causar maiores problemas no momento.
- [[#249](github.com/bacen/pix-api/issues/249)], [[#250](github.com/bacen/pix-api/issues/250)]: Com a entrada do campo "chave" como identificador do webhook, toda a parte referente à paginação
  em GET /webhook perde a razão de existir. Nesse sentido, os parâmetros de busca "inicio" e "fim" passam
  a ser opcionais. O objeto de paginação "parametros", também torna-se opcional.
- [[#239](github.com/bacen/pix-api/issues/239)]: Conforme relatado nesta discussão, entendemos que
  seria interessante, tanto sob o aspecto de segurança quanto sob o aspecto de funcionalidade, que o
  objeto pix agregue o atributo "chave", opcional.
- [[#241](https://github.com/bacen/pix-api/issues/241)]: Acrescentamos detalhes em relação à questão do acionamento do webhook por parte do PSP recebedor.
- [[#294](https://github.com/bacen/pix-api/issues/294)]: Erro de ortografia. Na documentação, onde se lê `pixUrlAcessToken` deveria estar escrito `pixUrlAccessToken`.
- [[#273](https://github.com/bacen/pix-api/issues/273)]: O texto do response 202 do endpoint `PATCH lotecobv/{id}` estava erroneamente induzindo o
  leitor a pensar que o lote já estava revisado quando, na verdade, estaria apenas em processamento
- [[#273](https://github.com/bacen/pix-api/issues/273)]: Na lista de violações em lotecobv, havia indicações do endpoint `/lotecobv/{txid}`, o que inexiste. O correto é `/lotecobv/{id}`.
- [[#316](https://github.com/bacen/pix-api/issues/316)]: Duas violações específicas foram removidas por questões de performance.

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

- removido o objeto **opcional** pix.pagador [#153](https://github.com/bacen/pix-api/issues/153)
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
