# Serviço para envios de arquivos para o S3 AWS:

⚙️ **Tecnologias**
- Java 11
- Framework Spring Boot

# Projeto

Está aplicação tem como objetivo demonstrar um exemplo de implementação para fazer um **envio** e **download** de arquivos para o bucket no S3 da AWS.

# Exemplo
**Configurando credenciais e região para autorizar uma solicitação na AWS:**

**Obs: Método implementado pode carregar credenciais de um sistema existente ou carregar novas credenciais.**
```java
@Configuration
public class StorageConfig {

    @Value("${cloud.aws.credentials.access-key}")
    protected String accessKey;

    @Value("${cloud.aws.credentials.secret-key}")
    protected String accessSecret;

    @Value("${cloud.aws.region.static}")
    protected String region;

    @Bean
    public AmazonS3 s3Client() {
        AWSCredentials credentials = new BasicAWSCredentials(accessKey, accessSecret);
        return AmazonS3ClientBuilder.standard()
                .withCredentials(new AWSStaticCredentialsProvider(credentials))
                .withRegion(region).build();
    }
}
```
#
**Métodos para envio, download e exclusão dos arquivos no S3 via Postman:**

**Obs: O conteúdo do arquivo é armazenado na memória ou temporariamente no disco. Em ambos os casos, o usuário é responsável por copiar o conteúdo do arquivo para um nível de sessão ou armazenamento persistente. O armazenamento temporário será limpo no final do processamento da solicitação.**
```java
@RestController
@RequestMapping("/file")
public class StorageController {

    @Autowired
    protected StorageService service;

    @PostMapping("/upload")
    public ResponseEntity<String> uploadFile(@RequestParam(value = "file") MultipartFile file) {
        return new ResponseEntity<>(service.uploadFile(file), HttpStatus.OK);
    }

    @GetMapping("/download/{fileName}")
    public ResponseEntity<ByteArrayResource> downloadFile(String fileName) {
        byte[] data = service.downloadFile(fileName);
        ByteArrayResource resource = new ByteArrayResource(data);
        return ResponseEntity
                .ok()
                .contentLength(data.length)
                .header("Content-type", "application/octet-stream")
                .header("Content-disposition", "attachment; fileName=\"" + fileName + "\"")
                .body(resource);
    }

    @DeleteMapping("/delete/{fileName}")
    public ResponseEntity<String> deleteFile(@PathVariable String fileName) {
        return new ResponseEntity<>(service.deleteFile(fileName), HttpStatus.OK);
    }
}
```
# 
**Nesta aplicação foi utilizado o application.yml para definir o acesso da aws, porta, nome do bucket e tamanho do arquivo:**
```java
cloud:
  aws:
    credentials:
      access-key:
      secret-key:
    region:
      static: us-east-2
    stack:
      auto: false

application:
  bucket:
    name:


spring:
  servlet:
    multipart:
      enabled: true
      file-size-threshold: 2MB
      max-file-size: 5MB
      max-request-size: 10MB

server:
  port: 9090
```
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
