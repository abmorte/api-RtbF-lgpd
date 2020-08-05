# Api RtbF LGPD
> 1. Descrição da Business network (BNt);
> 2. Descrição da api com a assinatura dos métodos para provimento do Direito ao Esquecimento e Retificação da LGPD - Lei Geral de Proteção de Dados Pessoais.


**1. Business Network (BNt)**

> BNt formada pelo Titular, Controlador e Operador.
> referência 1: https://cloud.ibm.com/docs/blockchain?topic=blockchain-swagger-network
> referência 2: https://cloud.ibm.com/docs/blockchain?topic=blockchain-ibp-swagger#ibp-swagger

Definição da BNt:

**Participantes**
`Titular` `Controlador` `Operador`
<<TODO> inserir figura do livro HandsOn Hyperledger>>
![Logo do R](http://developer.r-project.org/Logo/Rlogo-5.png)

**Ativos**
`Dados Pessoais (PII, PPII e NPII)` `Termos do Contrato` `Compartilhamento`


**Transações Rede**
`1. formar-rede` `2. aderir-rede`  `2.3 aceitar-termos-contrato` `2.3.4 consentir-tratamento` `obter-dados-pessoais` `compartilhar-dados-pessoais` `notificar-tratamento-dados-pessoais` `excluir-dados-pessoais` `notificar-exclusao-ddaos-pessoais` `retificar-dados-pessoais` `notificar-retificacao-dados-pessoais`

**Regras de negócio**
`formar-rede (genesis)`
1.1 - A rede deve permitir/controlar a adesão de 1 Titular.      Exemplo: Motorista Uber. Cada instância desse Órgão Motorista é um motorista em particular (peer).
1.1.1 - A rede deve habilitar interface para adesão de 1 Titular
1.2 - A rede deve permitir/controlar a adesão de 1 Controlador.  Exemplo: Uber. Cada servidor da Uber é um peer.
1.2.1 - A rede deve habilitar interface para adesão de 1 Controlador
1.3 - A rede deve permitir/controlar a adesão de 1 Operador.     Exemplo: Serpro. Cada servidor do Serpro é um peer.
1.3.1 - A rede deve habilitar interface para adesão de 1 Operador
1.4 - A aceitação dos termos do contrato deve ser um pré-requisito para adesão da organização à rede.
call formar-rede()

`aderir-rede`
2.1 - A organização deve identificar-se como Titular, Controlador ou Operador
2.2 - A organização deve estar em território brasileiro [Art. 3º, inciso I] - a operaçao de tratamento seja realizada em territorio nacional. inciso II - os dados pessoais objeto do tratamento tenham sido coletados em territorio nacional

call aderir-rede(TipoOrg tipoOrg [Titular, Controlador, Operador])

2.3 - A organização deve aceitar os termos do contrato
 subcall `aceitar-termos-contrato`()
 ps. Vide exemplo adaptado de ONIK:
  1. Apague dados ao término do tratamento (Art.16) 
  2. Apague os dados mediante solicitação do titular (Art. 18)
  2. Tratamento de Dados deve ser realizado em território brasileiro (Escopo de dados no Brasil)
  3. Notificar violação de dados dentro de 72 horas 
  - (Art. 9º - O titular tem o direito ao acesso facilitado às informações sobre o tratamento de seus dados de forma clara [...])
  4. Cada tratamento (distribuição inclusive) de dados de notificação ao Titular, e precisa do consentimento deste (Art. 18)
  5. O tratamento de dados será cessado quando da revogação do consentimento ou a pedido da ANPR? (art. 15)
  ps. Mapear a ANPR também como uma organização da rede?
 
  
 


Exemplos:

Criar `Titular`, `Controlador`, `Operador`:

```
{
  "$class": "cidadaobr.brasil.bnt.Titular",
  "email": "andersonA@brasil.cidadaobr",
  "firstName": "Billy",
  "lastName": "Thompson"
  "cpf": "858.978.646-90"
}

```
```
{
  "$class": "rfb.brasil.bnt.Controlador",
  "email": "rfb@brasil.rfb",
  "Name": "Receita Federal do Brasil",
  "shortName": "RFB"
  "cnpj": "867.986.0001-90" 
}
```
```
{
  "$class": "dataprev.brasil.bnt.Operador",
  "email": "dataprevB@brasil.dataprev",
  "Name": "Dataprev",
  "shortName": "DTP"
  "cnpj": "755.986.0001-90" 
}
```


Submit  `Compartilhar` transaction:

```
{
  "$class": "org.acme.pii.AuthorizeAccess",
  "memberId": "org.acme.pii.Member#memberA@acme.org"
}
```
O Titular consente o tratameto e compartilha os seus dados pessoais (PII, PPII e NPII) com o Controlador
| Artigo LGPD |                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                         |
|:-----------:|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| 7º          | O tratamento de dados pessoais somente pode ser realizado nas seguintes hipóteses:  I - mediante o fornecimeno de consentimento pelo titular; § 4º - é dispensada a exigência de consentimento [...] para dados tornados manifestamente públicos pelo Titular  [...] mais informações sobre tratamento de dados de crianças no texto no Google Docs | call compartilhar (Dados dados-pessoais*, Destino operador\|controlador*, Boolean consentimento, Boolean publicos)                                                      |
| 9º          | O titular tem o direito ao acesso facilitado às informaçõe sobre o tratamento de seus dados [...]                                                                                                                                                                                                                                                   | consultar-dadospessoais(Titular identificacao-titular)                                                                                                                  |
| 11º         | O tratamento de dados pessoais sensíveis somente poderá ocorrer nas seguintes hipóteses:  I - quando o titular ou seu responsável consentir, de forma destacada e específica para finalidades específicas [..]                                                                                                                                      |                                              call compartilhar (Dados dados-pessoais-sensiveis, Destino operador\|controlador, Boolean consentimento, Boolean publicos) |
| 11º         | § 4º É vedada a comunicação ou o uso compartilhado entre controladores de dados pessoais sensíveis **referentes à saúde** [...] e para permitir:  I - a **portabilidade** de dados quando solicitada pelo Titular                                                                                                                                   |                                                                                                    call transferir(Dados dados-pessoais-sensiveis, Destino controlador) |
| 15          | O término do tratamento de dados pessoais ocorrerá nas seguintes hipóteses: III - [...] inclusive no exercício de seu direito de revogação                                                                                                                                                                                                          |                                                                             call revogar-consentimento (ANPD anpd, Titular ident-titular, Destino operador/controlador) |
| 16          | Os dados pessoais serão eliminados após o término de seu tratamento, no âmbito e nos limites técnicos das atividades, autorizada a conservação para as seguintes finalidades:  I -  cumprimento de obrigação legal [...]  II - estudo por órgão de pesquisa                                                                                         | eliminar-dados-pessoais (Titular titular)  Atores:  - Titular - Controlador: o próprio controlador pode comandar a eliminação dos dados após a realização do tratamento |
## License <a name="license"></a>
http://creativecommons.org/licenses/by/4.0/

.
