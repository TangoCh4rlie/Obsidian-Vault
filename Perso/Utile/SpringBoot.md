[Java](java)
@Bean : Permet de faire de "l'injection de dépendance" pour par exemple créer une connexion avec une bd :

``` java
@Configuration  
public class QueueClientConfig {  
    @Value("${storage.connectStr}")  
    private String connectStr;  
  
    @Value("${storage.containerName}")  
    private String containerName;  
  
    @Bean  
    public QueueClient queueClientBuilder() {  
        if (connectStr == null || connectStr.isEmpty()) {  
            throw new IllegalStateException("connectStr is null or empty");  
        }  
        if (containerName == null || containerName.isEmpty()) {  
            throw new IllegalStateException("containerName is null or empty");  
        }  
        return new QueueClientBuilder()  
                .connectionString(connectStr)  
                .queueName(containerName)  
                .buildClient();  
    }  
}
```

``` java
/**  
 * Constructeur qui récupère une connection 
 * @param queueClient Bean de QueueClientConfig  
 */
 public StorageQueueClientService(QueueClient queueClient) {  
    this.queueClient = queueClient;  
    queueClient.create();  
    objectMapper = new ObjectMapper();  
    queue = new ArrayList<>();  
}
```
Le queue client est injecté directement dans les paramètres du constructeur de la classe

### Intercepter des requêtes avant qu'elles soient retournées
implémenter l'interface ``HandleInterceptor`` 
### Récupérer un objet avant qu'il soit retourné
implémenter l'interface ``ResponseBodyAdvice``
permet de manipuler l'objet avant de le retourner 