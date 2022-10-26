![alt text](https://miro.medium.com/max/700/1*cmfoGi3FnVIBCwvmVLYgjg.png)
# dio-dynamodb
Repositório para o desafio de código do Bootcamp Geração Tech Unimed-BH - Ciência de Dados da DIO sobre o Amazon DynamoDB.

<br>
<h2>Serviço utilizado</h2>

<li>Amazon DynamoDB</li>
<li>Amazon CLI para execução em linha de comando</li>

<br>
<h2>Comandos para execução do experimento:</h2>
<li>Criar uma tabela</li>

```
aws dynamodb create-table \
    --table-name Music \
    --attribute-definitions \
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongTitle,AttributeType=S \
    --key-schema \
        AttributeName=Artist,KeyType=HASH \
        AttributeName=SongTitle,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=10,WriteCapacityUnits=5
```


<li>Inserir um item</li>

```
aws dynamodb put-item \
    --table-name Music \
    --item file://itemmusic.json \
```

<li>Inserir múltiplos itens</li>

```
aws dynamodb batch-write-item \
    --request-items file://batchmusic.json
```

<li>Criar um index global secundário baeado no título do álbum</li>

```
aws dynamodb update-table \
    --table-name Music \
    --attribute-definitions AttributeName=AlbumTitle,AttributeType=S \
    --global-secondary-index-updates \
        "[{\"Create\":{\"IndexName\": \"AlbumTitle-index\",\"KeySchema\":[{\"AttributeName\":\"AlbumTitle\",\"KeyType\":\"HASH\"}], \
        \"ProvisionedThroughput\": {\"ReadCapacityUnits\": 10, \"WriteCapacityUnits\": 5      },\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"
```

<li>Pesquisar item por artista</li>

```
aws dynamodb query \
    --table-name Music \
    --key-condition-expression "Artist = :artist" \
    --expression-attribute-values  '{":artist":{"S":"Iron Maiden"}}'
```

<li>Pesquisar item por artista e título da música</li>

```
aws dynamodb query \
    --table-name Music \
    --key-condition-expression "Artist = :artist and SongTitle = :title" \
    --expression-attribute-values file://keyconditions.json
```
