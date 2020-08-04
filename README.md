# Api RtbF LGPD
> 1. Descrição da Business network (BNt);
> 2. Descrição da api com a assinatura dos métodos para provimento do Direito ao Esquecimento e Retificação da LGPD - Lei Geral de Proteção de Dados Pessoais.


** Business Network**

> BNt formada pelo Titular, Controlador e Operador.

Definição da BNt:

**Participantes**
`Titular` `Controlador` `Operador`

**Ativos**
`PII` `PPII` `NPII` `Termos do Contrato` `Compartilhamento`


**Transações**
`Autenticar` `Compartilhar` `Esquecer` `Retificar`


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
