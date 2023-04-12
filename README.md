# 📚  Escola de Cursos(DB)
Este repositório foi criado como parte de um desafio proposto pela DIO no curso de Banco de Dados SQL e NoSQL. Nesse desafio, foi proposto criar uma tabela no DynamoDB e adicionar índices a ela, utilizando os exemplos fornecidos no curso. Porém, optei por utilizar um projeto pessoal, de outro desafio, para realizar o desafio atual, que consiste em um sistema de gerenciamento de cursos online, cujo código está disponível no seguinte link do Github: [https://github.com/JulianWelter/desafio-poo-dio](https://github.com/JulianWelter/desafio-poo-dio).

## Criando a tabela 🚀

`aws dynamodb create-table --table-name Course --attribute-definitions AttributeName=name,AttributeType=S AttributeName=duration,AttributeType=S --key-schema AttributeName=name,KeyType=HASH AttributeName=duration,KeyType=RANGE`

## Valor inserido 📝

`{ "name": { "S": "Teste" }, "duration": { "S": "1h30" }, "description": { "S": "Curso Teste" }, "price": { "N": "30" } }`

## Adicionando índice 🔎

`aws dynamodb update-table --table-name Course --attribute-definitions AttributeName=CourseName,AttributeType=S --global-secondary-index-updates "[{\"Create\":{\"IndexName\": \"CourseName-index\",\"KeySchema\":[{\"AttributeName\":\"CourseName\",\"KeyType\":\"HASH\"}],\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"`

## Criando índice com descrição e preço 🔍💰

`aws dynamodb update-table --table-name Course --attribute-definitions AttributeName=CourseDescription,AttributeType=S AttributeName=CoursePrice,AttributeType=N --global-secondary-index-updates "[{\"Create\":{\"IndexName\":\"CoursePriceDescription-index\",\"KeySchema\":[{\"AttributeName\":\"CourseDescription\",\"KeyType\":\"HASH\"},{\"AttributeName\":\"CoursePrice\",\"KeyType\":\"RANGE\"}],\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"`
