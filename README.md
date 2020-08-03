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

| Artigo LGPD |                                                                                                                                                                                                                                                               |                                                                                                                    |
|:-----------:|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------:|
| 7º          | O tratamento de dados pessoais somente pode ser realizado nas seguintes hipóteses:  I - mediante o fornecimeno de consentimento pelo titular; § 4º - é dispensada a exigência de consentimento [...] para dados tornados manifestamente públicos pelo Titular | call compartilhar (Dados dados-pessoais*, Destino operador\|controlador*, Boolean consentimento, Boolean publicos) |
| Gnat        | per gram                                                                                                                                                                                                                                                      |                                                                                                              13.65 |
|             | each                                                                                                                                                                                                                                                          |                                                                                                               0.01 |
| Gnu         | stuffed                                                                                                                                                                                                                                                       |                                                                                                              92.50 |
| Emu         | stuffed                                                                                                                                                                                                                                                       |                                                                                                              33.33 |
| Armadillo   | frozen                                                                                                                                                                                                                                                        |                                                                                                               8.99 |


## License <a name="license"></a>
http://creativecommons.org/licenses/by/4.0/

.
