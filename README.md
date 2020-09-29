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
      "documento":"60677546068",
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
         "ImageBase64",
         "ImageBase642"
      ]
   },
   "proprietarios":[
      {
         "perfil_id":"1",
         "doc_proprietario":"25231510068",
         "nome":"PROPRIETARIO 01",
         "sexo":"M",
         "uf":"MT",
         "filiacao_materno":"Mae",
         "filiacao_paterno":"Pai",
         "contato_email":"email@motorista.com.br",
         "contato_celular":"066 9 9695-4545",
         "contato_telefone":"066 3421-5485",
         "documento_proprietario_anexo":"ImageBase64",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"CCC1234",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CAVALO",
               "anexo":"ImageBase64"
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"VVV8888",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CARRETA",
               "anexo":"ImageBase64"
            }
         ]
      },
      {
         "perfil_id":"1",
         "doc_proprietario":"60677546068",
         "nome":"PROPRIETARIO 02",
         "sexo":"M",
         "uf":"MT",
         "filiacao_materno":"Mae",
         "filiacao_paterno":"Pai",
         "contato_email":"email@motorista.com.br",
         "contato_celular":"066 9 9695-4545",
         "contato_telefone":"066 3421-5485",
         "documento_proprietario_anexo":"ImageBase64",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"YYY8989",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CAVALO",
               "anexo":"ImageBase64"
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"YYY9090",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CARRETA",
               "anexo":"ImageBase64"
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
      "id":"259",
      "protocolo":"2909.1601403938/2020",
      "status":"HOMOLOGADO",
      "pesquisa_avancada":"N",
      "validade":"2020-09-30",
      "categoria":"COMBO",
      "motorista":{
         "status":"HOMOLOGADO",
         "documento":"60677546068",
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
            "https://localhost/files/analise_perfil/api/combo/5-5f737adb304c5.png"
         ]
      },
      "proprietario":[
         {
            "perfil_id":"1",
            "doc_proprietario":"25231510068",
            "nome":"PROPRIETARIO 01",
            "sexo":"M",
            "uf":"MT",
            "filiacao_materno":"Mae",
            "filiacao_paterno":"Pai",
            "contato_email":"email@motorista.com.br",
            "contato_celular":"066 9 9695-4545",
            "contato_telefone":"066 3421-5485",
            "anexo":"https://localhost/files/analise_perfil/api/combo/5-5f737adb32e9c.png",
            "veiculos":[
               {
                  "perfil_id":"1",
                  "renavam":"999999999",
                  "placa":"CCC1234",
                  "chassi":"2222222222",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://localhost/files/analise_perfil/api/combo/592-5f737adb36f2d.png"
               },
               {
                  "perfil_id":"1",
                  "renavam":"8888888888",
                  "placa":"VVV8888",
                  "chassi":"333333",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://localhost/files/analise_perfil/api/combo/593-5f737adb39ec7.png"
               }
            ]
         },
         {
            "perfil_id":"1",
            "doc_proprietario":"60677546068",
            "nome":"PROPRIETARIO 02",
            "sexo":"M",
            "uf":"MT",
            "filiacao_materno":"Mae",
            "filiacao_paterno":"Pai",
            "contato_email":"email@motorista.com.br",
            "contato_celular":"066 9 9695-4545",
            "contato_telefone":"066 3421-5485",
            "anexo":"https://localhost/files/analise_perfil/api/combo/5-5f737adb3c37e.png",
            "veiculos":[
               {
                  "perfil_id":"1",
                  "renavam":"999999999",
                  "placa":"YYY8989",
                  "chassi":"2222222222",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://localhost/files/analise_perfil/api/combo/595-5f737adb3ee13.png"
               },
               {
                  "perfil_id":"1",
                  "renavam":"8888888888",
                  "placa":"YYY9090",
                  "chassi":"333333",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://localhost/files/analise_perfil/api/combo/596-5f737adb4193e.png"
               }
            ]
         }
      ]
   }
}
```
# Parâmetros

#### Parâmetros Perfil_id
| Descrição     | Valor   |
| ------------- |--------------:|
| FROTA         | 1|
| AGREGADO      | 2|
| TERCEIRO      | 3|
| AJUDANTE      | 4|




