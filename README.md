# Desafio4AWSCloudFormation
Repositório do Bootcamp AWS da DIO parceria Santander
README.md — Laboratório: AWS CloudFormation
Sumário
Visão geral

Objetivos do laboratório

Arquitetura

Descrição do template CloudFormation

Passo a passo — deploy

Como validar que deu certo

Limpeza e custos

1. Visão geral
Este laboratório mostra como projetar, criar e operar uma stack AWS usando CloudFormation. O objetivo é aprender a criar uma stack utilizando um template.

Cenário prático: Criar um template YAML onde terá a criação de Lambda e um S3, irá baixar arquivo csv do github. O Lambda será chamado e o mesmo irá baixar o arquivo do GitHub e salvar no S3

2. Objetivos do laboratório
Ao final teremos a seguinte capacidade:

Entender a estrutura de um template CloudFormation
Criar stacks via Console
Validar recursos criados (S3, Lambda)
3. Arquitetura
Descrição sequencial:

Será criado template na extensão YAML.
Esse template irá criar um Bucket S3 e um Lambda. O Lambda será invocado e irá realizar o download do arquivo e salvar no bucket criado.
CustomLambdaInvoker aciona uma função Lambda
Lambda faz o download do CSV pela url e salva no S3.
Diagrama (simplificado):

[template.yaml --> [S3 Bucket] --> (CustomLambdaInvoker) --> [Lambda] --> {download e grava no S3}
4. Descrição do template CloudFormation
O template.yaml inclui as seções tipicamente usadas:

Parameters — variáveis passadas no deploy (ex.: Nome do stack, ambiente, prefixo de nomes).
Mappings — mapeamentos (ex.: AMI por região, caso use EC2).
Resources — definição dos recursos (S3 Bucket, Lambda Function, DynamoDB Table, IAM Roles/Policies, Event Notification, CloudWatch Log Group, SNS Topic opcional).
Outputs — informações úteis (ex.: ARN do bucket, nome da tabela DynamoDB, URL do console).
Recursos (exemplo mínimo)
LambdaExecutionRole: Role com políticas mínimas — s3:GetObject, dynamodb:PutItem, logs:CreateLogStream, logs:PutLogEvents.
ProcessorLambda: Função Lambda (Python 3.13).
5. Passo a passo — deploy
Opção A — Console
Acesse o Console AWS → CloudFormation.
Clique em Create stack → With new resources (standard).
Selecione Template file (envie templateDesafio4CloudFormation3.yaml).
Clique em Create stack e aguarde.
6. Como validar que deu certo
Verifique status da stack: Status esperado: CREATE_COMPLETE.
Verifique o bucket S3 criado (nome no output):
Verifique se o arquivo csv esta no Bucket S3
7. Limpeza e custos
Para não pagar por recursos após o laboratório, remova a stack:

Verifique se todos os recursos foram removidos (às vezes, buckets não são apagados automaticamente se não estiverem vazios). Se um bucket restante impedir a remoção, esvazie-o manualmente:
