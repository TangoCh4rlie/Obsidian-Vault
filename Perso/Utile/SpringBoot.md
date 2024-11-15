## Configurer un projet SpringBoot
[https://start.spring.io](https://start.spring.io) pour inititaliser un projet avec des dépendances
Mettre flyway avec la bonne configuration
```groovy
plugins {  
    id 'org.flywaydb.flyway' version '8.2.0'  
}  
  
flyway {  
    url = 'jdbc:mysql://localhost/saera3?createDatabaseIfNotExist=true&useSSL=false'  
    user = 'root'  
    password = 'root'  
}
```
`id 'org.flywaydb.flyway' version '8.2.0'` la 10.0.0 marchait pas la dernière fois que j'ai essayé. **Repasser en 8.2.0**

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

### Projection
Si l'utilisation de DTO n'est pas possible par ce que la query ne retourne pas une table a proprement parlé mais des éléments de plusieurs table, on peut faire un **projection

```java
public interface UtilisateurHabilitationProjection {  
    String getPrenom();  
    String getNom();  
    String getCodeVisa();  
    Boolean getActif();  
    String getGroupeLibelle();  
    String getSousGroupeLibelle();  
    Integer getMontantHabilitationProvision();  
    Integer getMontantHabilitationReglement();  
}
```

cette interface peut être retourné comme un DTO dans une ResponseEntity
```java
@GetMapping("habilitations")  
@Operation(summary = "Permet de récupérer la liste des utilisateur qui ont une habilitation dans un des trois groupe")  
public ResponseEntity<List<UtilisateurHabilitationProjection>> getHabilitations(  
        CurrentAuth currentAuth,  
        @RequestParam(name = "rolesBan", required = false) List<String> rolesBan  
) {  
    return ResponseEntity.ok().body(utilisateurService.findAllHabilitation(currentAuth, rolesBan));  
}
```
## Test avec une bd h2
```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)  
@ActiveProfiles("test")  
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)  
class AuthControllerTest {  
    @LocalServerPort  
    private int port;  
  
    private String PATH;  
  
    @BeforeEach  
    public void setUp() {  
        PATH = "http://localhost:" + port;  
    }  
  
    @Test  
    @Order(2)  
    void createToken() {  
        RestTemplate restTemplate = new RestTemplate();  
        AuthenticationRequestDTO authen = new AuthenticationRequestDTO();  
        authen.setUsername("toto");  
        authen.setPassword("titi");  
        HttpHeaders headers = new HttpHeaders();  
        headers.set("Content-type", "application/json;charset=UTF-8");  
        HttpEntity<AuthenticationRequestDTO> request = new HttpEntity<>(authen, headers);  
        AuthResponseDTO authenticationResponse =  
                restTemplate.postForObject(PATH + "/authenticate", request, AuthResponseDTO.class);  
        assertNotNull(authenticationResponse);  
        String token = authenticationResponse.getAuthenticationResponseDTO().getJwtToken();  
        assertNotNull(token);  
    }  
  
    @Test  
    @Order(1)  
    void register() {  
        RestTemplate restTemplate = new RestTemplate();  
        RegisterRequestDTO registerRequestDTO = new RegisterRequestDTO();  
        registerRequestDTO.setUsername("toto");  
        registerRequestDTO.setPassword("titi");  
        registerRequestDTO.setPasswordConfirm("titi");  
        registerRequestDTO.setUserType("PARRAIN");  
  
        HttpHeaders headers = new HttpHeaders();  
        headers.set("Content-type", "application/json;charset=UTF-8");  
        HttpEntity<RegisterRequestDTO> request = new HttpEntity<>(registerRequestDTO, headers);  
        AuthResponseDTO registerResponse = restTemplate.postForObject(PATH + "/register", request, AuthResponseDTO.class);  
        assertNotNull(registerResponse);  
        assertNotNull(registerResponse.getAuthenticationResponseDTO().getJwtToken());  
    }  
}
```