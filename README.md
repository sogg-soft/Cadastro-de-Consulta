# API REST - CADASTRO DE CONSULTA

### Autenticação

API baseada na arquitetura REST.
Todas as requisições devem ser enviadas com um token de autenticação no header da requisição HTTP. (Entre em contato com a SOGG SOFT). Ex:

```php 
$request->setHeaders(array(
          'content-type' => 'application/json',
          'Authorization' => {token}
        ));
```

                  
## Enviar Pesquisa

EndPoint: https://homologacao.soggsoft.com.br/ws/combo

Objeto Motorista
| Parâmetro     | Obrigatorio   |
| ------------- |--------------:|
| pesquisa_avancada      | SIM|
| perfil_id      | SIM|
| documento      | SIM|
| nome      | SIM|
| sexo      | SIM|
| nascimento| SIM|
| naturalidade| SIM|
| rg| SIM|
| rg_uf| SIM|
| rg_emissao| NÃO|
| cnh| SIM|
| cnh_uf| SIM|
| cnh_emissao| NÃO|
| cnh_validade| SIM|
| cnh_seguranca| SIM|
| cnh_categoria_id| SIM|
| cnh_prontuario| NÃO|
| filiacao_materno| SIM|
| filiacao_paterno| NÃO|
| contato_telefone| NÃO|
| contato_celular| NÃO|
| contato_email| NÃO|
| anexos| NÃO| 

Request:

Tipo de requisição: `POST`

```json
{
   "motorista":{
      "pesquisa_avancada":"N",
      "perfil_id":"1",
      "documento":"606.775.460-68",
      "nome":"MOTORISTA TESTE",
      "sexo":"M",
      "nascimento":"1992-06-17",
      "naturalidade":"Campo Grande",
      "rg":"21445591",
      "rg_uf":"MT",
      "rg_emissao":"2010-01-01",
      "cnh":"22222222",
      "cnh_uf":"MT",
      "cnh_emissao":"2010-01-01",
      "cnh_validade":"2010-10-01",
      "cnh_seguranca":"33333333",
      "cnh_categoria_id":"4",
      "cnh_prontuario":"2",
      "filiacao_materno":"MAE",
      "filiacao_paterno":"PAI",
      "contato_telefone":"66999999999",
      "contato_celular":"66999999999",
      "contato_email":"CONTATO@SOGGSOFT.COM.BR",
      "anexos":[
         "Imagem em base64"
      ]
   },
   "proprietarios":[
      {
         "perfil_id":"1",
         "doc_proprietario":"606.775.460-68",
         "nome":"RAZÃO SOCIAL",
         "sexo":"M",
         "uf":"MT",
         "filiacao_materna":"Mae",
         "filiacao_paterna":"Pai",
         "email":"email@motorista.com.br",
         "celular":"066 9 9695-4545",
         "telefone":"066 3421-5485",
         "documento_proprietario_anexo":"Imagem em base64",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"YYY8989",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CAVALO",
               "anexo":"Imagem em base64"
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"YYY9090",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CARRETA",
               "anexo":"Imagem em base64"
            }
         ]
      }
   ]
}
```

Response:
Será retornado o código da nova pesquisa gerada, é necessário armarzena-lo para pesquisar o status da consulta posteriormente.

HTTP CODE `201` 
```json
{
  "codigo": "204",
  "message": "success"
}
```

## Consultar Pesquisa

EndPoint: https://homologacao.soggsoft.com.br/ws/combo/{{idPesquisa}}

Request:

Tipo de requisição: `GET`

Response:
```json
{
   "pesquisa":{
      "id":"222",
      "protocolo":"2809.1601307182\/2020",
      "status":"HOMOLOGADO",
      "pesquisa_avancada":"N",
      "validade":"2020-09-29",
      "categoria":"COMBO",
      "motorista":{
         "status":"HOMOLOGADO",
         "documento":"606.775.460-68",
         "nome":"MOTORISTA TESTE",
         "sexo":"M",
         "nascimento":"1992-06-17",
         "naturalidade":"Campo Grande",
         "rg":"21445591",
         "rg_uf":"MT",
         "rg_emissao":"2010-01-01",
         "cnh":"22222222",
         "cnh_uf":"MT",
         "cnh_validade":"2010-10-01",
         "cnh_seguranca":"33333333",
         "cnh_categoria_id":"4",
         "cnh_prontuario":"2",
         "filiacao_materno":"MAE",
         "filiacao_paterno":"PAI",
         "contato_telefone":"66999999999",
         "contato_celular":"66999999999",
         "contato_email":"CONTATO@SOGGSOFT.COM.BR",
         "anexos":[
            "localhost.\/files\/analise_perfil\/api\/combo\/5-5f7200d7e2740.png"
         ]
      },
      "proprietario":{
         "perfil_id":"1",
         "doc_proprietario":"60677546068",
         "nome":"RAZÃO SOCIAL",
         "sexo":"M",
         "uf":"MT",
         "filiacao_materna":"Mae",
         "filiacao_paterna":"Pai",
         "contato_email":"email@motorista.com.br",
         "contato_celular":"066 9 9695-4545",
         "contato_telefone":"066 3421-5485",
         "anexo":"localhost.\/files\/analise_perfil\/api\/combo\/5-5f7200d7e50e3.png",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"YYY8989",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"COMBO",
               "anexo":"localhost.\/files\/analise_perfil\/api\/combo\/375-5f7200d7e7d97.png"
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"YYY9090",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"COMBO",
               "anexo":"localhost.\/files\/analise_perfil\/api\/combo\/376-5f7200d7ea46b.png"
            }
         ]
      }
   }
}
```


