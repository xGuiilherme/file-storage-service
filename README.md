# Serviço para envios de arquivos para S3 AWS


Neste projeto demonstro um exemplo de implementação para fazer **envio** e **download** de arquivos para o S3 na AWS.

```java
@Configuration
public class StorageConfig {

    @Value("${cloud.aws.credentials.access-key}")
    protected String accessKey;

    @Value("${cloud.aws.credentials.secret-key}")
    protected String accessSecret;

    @Value("${cloud.aws.region.static}")
    protected String region;

    /* Método: Retorna um AWSCredentials para autorizar uma solicitação da AWS.
       Em: Uma implementação pode carregar credenciais de um sistema existente ou carregar novas credenciais
    */
    @Bean
    public AmazonS3 s3Client() {
        AWSCredentials credentials = new BasicAWSCredentials(accessKey, accessSecret);
        return AmazonS3ClientBuilder.standard()
                .withCredentials(new AWSStaticCredentialsProvider(credentials))
                .withRegion(region).build();
    }
}
```
