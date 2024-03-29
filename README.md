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


<details>
<summary>Detalhes objeto Motorista</summary>

| Parâmetro     | Obrigatorio   | Tipo | Valor |
| ------------- |--------------|--------------|--------------:|
| pesquisa_avancada      | SIM| String | ('Y' ou'N') |
| perfil_id      | SIM| int | [Parâmetros](https://github.com/sogg-soft/Cadastro-de-Consulta#par%C3%A2metros-perfil_id)  |
| documento      | SIM| String |
| nome      | SIM| String | 
| sexo      | SIM| String(1) | 'F' ou'M' |
| nascimento| SIM| Date | 'yyyy-mm-dd' |
| naturalidade| SIM| String |
| rg| SIM| String(11) |
| rg_uf| SIM| String(2) |
| rg_emissao| NÃO| Date | 'yyyy-mm-dd' |
| cnh| SIM| String |
| cnh_uf| SIM| String(2) |
| cnh_emissao| NÃO| Date | 'yyyy-mm-dd' |
| cnh_validade| SIM| Date | 'yyyy-mm-dd' |
| cnh_seguranca| SIM| String | [Obter Cód Segurança](https://youtu.be/9kgIFn4vPVk?t=45)  |
| cnh_categoria_id| SIM| int | [Parâmetros Categoria](https://github.com/sogg-soft/Cadastro-de-Consulta#par%C3%A2metros-cnh_categoria_id)  |
| cnh_prontuario| NÃO| String |
| filiacao_materno| SIM| String | 
| filiacao_paterno| NÃO| String |
| contato_telefone| NÃO| String | xx xxxx-xxxx|
| contato_celular| NÃO| String | xx x xxxx-xxxx|
| contato_email| NÃO| String | email@dominio.com.br |
| anexos| NÃO| String | Base64 |

</details>

<details>
<summary>Detalhes objeto Proprietário</summary>

| Parâmetro     | Obrigatorio   | Tipo | Valor |
| ------------- |--------------|--------------|--------------:|
| perfil_id      | SIM| int | [Parâmetros](https://github.com/sogg-soft/Cadastro-de-Consulta#par%C3%A2metros-perfil_id)  | 
| doc_proprietario      | SIM| String | CPF ou CNPJ |
| nome | SIM | String |  
| sexo | NÃO | String(1) | 
| uf | NÃO | String(2) |
| filiacao_materno| NÃO| String |
| filiacao_paterno| NÃO| String |
| razao_social| SIM | String |  
| inscricao_municipal| NÃO | String | 
| inscricao_estadual| NÃO | String | 
| contato_email| NÃO| String | email@dominio.com.br |
| contato_telefone| NÃO| String | xx xxxx-xxxx|
| contato_celular| NÃO| String | xx x xxxx-xxxx|
| anexos| NÃO| String | Base64 |

</details>

<details>
<summary>Detalhes objeto Veículo</summary>

| Parâmetro     | Obrigatorio   | Tipo | Valor |
| ------------- |--------------|--------------|--------------:|
| perfil_id | SIM | int | [Parâmetros](https://github.com/sogg-soft/Cadastro-de-Consulta#par%C3%A2metros-perfil_id)  | 
| renavam | SIM | String |
| placa | SIM | String |
| chassi | SIM | String |
| antt | SIM | String |
| uf | SIM | String (2) |
| categoria | SIM | String | [Parâmetros](https://github.com/sogg-soft/Cadastro-de-Consulta#par%C3%A2metros-categoria)  |
| anexo | NÃO | String | Base64 |

</details>

`solicitante: Campo para informar quem foi o solicitante consulta. Não é obrigatório`

``` 
anexos: enviar no formato base64, informando o tipo de arquivo 
ex: data:application/pdf;base64,JVBERi0xLjQNCiXi48/TDQoxIDAgb2J... 
```

##### Request:

Tipo de requisição: `POST`

```json
{
   "solicitante":"Nome do solicitante",
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
         "data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ==",
         "data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ=="
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
         "documento_proprietario_anexo":"data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ==",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"CCC1234",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CAVALO",
               "anexo":"data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ=="
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"VVV8888",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CARRETA",
               "anexo":"data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ=="
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
         "documento_proprietario_anexo":"data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ==",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"YYY8989",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CAVALO",
               "anexo":"data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ=="
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"YYY9090",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CARRETA",
               "anexo":"data:image/png;base64,YmFzZTY0IGRhIGltYWdlbQ=="
            }
         ]
      }
   ]
}
```

##### Response:

Será retornado o código da nova pesquisa gerada, é necessário armarzena-lo para pesquisar o status da consulta posteriormente.
Caso o documento do motorista enviado na pesquisa não esteja cadastrado no sistema, o mesmo será realizado e vinculado a empresa, nesta caso, será adicionado o atributo motoristaID.

Nota: Caso o documento do motorista já esteja cadastrado para empresa, o atributo motoristaID não será retornado

HTTP CODE `201` 
```json
{
  "codigo": "cb5d2100-62c5-4ca0-a7d3-3dae3df7876f",
  "message": "success",
  "motoristaID": "9128"
}
```

## Consultar Pesquisa

É possível consultar uma pesquisa em específico passando o id da mesma, exemplo: `https://homologacao.soggsoft.com.br/ws/combo/?id=cb5d2100-62c5-4ca0-a7d3-3dae3df7876f`, ou passando o documento de um motorista, caso exista pesquisa para o motorista em questão, será retornado a última pesquisa realizada para o mesmo, exemplo: `https://homologacao.soggsoft.com.br/ws/combo/?documento=36375073073`

EndPoint: https://homologacao.soggsoft.com.br/ws/combo/?{paramêtro}={valor}

Request:

Tipo de requisição: `GET`

Response:
```json
{
   "pesquisa":{
      "id":"cb5d2100-62c5-4ca0-a7d3-3dae3df7876f",
      "protocolo":"2909.1601403938/2020",
      "status":"HOMOLOGADO",
      "pesquisa_avancada":"N",
      "validade": "2021-05-05",
      "revalidacao": true,
      "validade_revalidacao": "2021-10-27",
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
      ],
      "ocorrencias": []
   }
}
```
 Caso a pesquisa retorne status PENDENCIA_CLIENTE sera adicionado um ou mais objetos (1 para cada ocorrencia), dentro do array ocorrencias.
Exemplo:
```JSON
{
  "pesquisa": {
    "informacoes referente a pesquisa":  "...",
    "motorista": [
      "...."
    ],
    "proprietarios": [
      "...."
    ],
    "ocorrencias": [
      {
        "objeto": "Motorista",
        "ocorrencia": "CNH VENCIDA",
        "observacao": "CNH DO MOTORISTA VENCIDA"
      },
      {
        "objeto": "Veículo",
        "ocorrencia": "PLACA NÃO CONFERE",
        "observacao": "PLACA NÃO ENCONTRADA"
      },
      {
        "objeto": "Proprietário",
        "ocorrencia": "NOME DIGITADO ERRADO",
        "observacao": "NOME NÃO CONFERE COM DOCUMENTO"
      }
    ]
  }
}

```

## Alterar Pesquisa
Obs: O método PUT está disponível apenas caso o status da pesquisa seja igual à PENDENCIA_CLIENTE
EndPoint: https://homologacao.soggsoft.com.br/ws/combo/{{idPesquisa}}
Tipo de requisição: `PUT`
Request:
Utilizar o mesmo body do método POST, porém é necessário enviar apenas os atributos que deseja alterar.
Exemplo de request para alterar o nome do motorista:

```json
{
  "motorista": {
    "nome": "Henrique da Silva"
  }
}
```

Response
HTTP CODE `200`
```json
{
  "codigo": "cb5d2100-62c5-4ca0-a7d3-3dae3df7876f",
  "message": "success"
}
```


## Revalidar Pesquisa
Obs: Funcionalidade disponóvel quando a consulta anterior retornar o atributo revalidacao como true. 
É possível realizar a revalidação passando dois parâmetros, o código da pesquisa ou o documento do motorista. Ambas os métodos irão retornar o mesmo response.

Revalidação enviando o código da pesquisa:

EndPoint: https://homologacao.soggsoft.com.br/ws/combo/revalidacao/{{idPesquisa}}

Tipo de requisição: `POST`

`solicitante: Campo para informar quem foi o solicitante consulta. Não é obrigatório`

Request:
```json
{
  "solicitante": "solicitante"
}
```

Response
HTTP CODE `200`
```json
{
   "codigo": "123456",
   "status": "AGUARDANDO",
   "message": "success"
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

#### Parâmetros categoria
| Descrição     | Valor   |
| ------------- |--------------:|
| CAVALO         | 'CAVALO'|
| CARRETA      | 'CARRETA'|

#### Parâmetros cnh_categoria_id
| ID     | Categoria   |
| ------------- |--------------:|
| 1 |A|
| 2 |B|
| 3 |C|
| 4 |D|
| 5 |E|
| 6 |AB|
| 7 |AC|
| 8 |AD|
| 9 |AE|



