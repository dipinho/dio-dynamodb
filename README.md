# dio-dynamodb
Repositório para o desafio de código do Bootcamp Ciencias de Dados da DIO sobre o Amazon DynamoDB.

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
