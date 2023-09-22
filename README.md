## Envio de Arquivos para o Amazon S3:

Este é um serviço em Java 11 baseado no Framework Spring Boot que permite o envio de arquivos para um Bucket no Amazon AWS S3. Com esta aplicação, você pode enviar, deletar e baixar arquivos de forma fácil e eficiente no S3 da AWS.

## **Tecnologias Utilizadas**
- Java 11
- Framework Spring Boot
- Amazon AWS - S3 SDK

## Projeto

Esta aplicação tem como objetivo demonstrar um exemplo de implementação para fazer o envio e download de arquivos para um Bucket no S3 da AWS. Nesta implementação, utilizamos alguns dos exemplos abaixo para manipular os arquivos e o Bucket que foram criados:

- Enviar um arquivo para o Bucket que está criado no S3 da AWS.
- Deletar um arquivo específico do Bucket.
- Baixar um arquivo específico do Bucket.

#
**Dependencia necessaria para conectar ao aws**
```xml
<dependency>
    <groupId>com.amazonaws</groupId>
	<artifactId>aws-java-sdk</artifactId>
	<version>1.12.239</version>
</dependency>
```
#
**Para mais informações sobre SDK AWS para Java**
**[clique aqui](https://docs.aws.amazon.com/pt_br/sdk-for-java/latest/developer-guide/using.html)**
