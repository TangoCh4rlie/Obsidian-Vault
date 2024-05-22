[springboot](SpringBoot)
### Utilisation de stream
``` java
List<? extends Serializable> notNullValues = Stream.of(  
        logBuilder.getAppAccess(),  
        logBuilder.getEntityType(),  
        logBuilder.getEntityKey(),  
        logBuilder.getAccessType(),  
        logBuilder.getAccessDate(),  
        logBuilder.getUserToken()  
).filter(Objects::isNull).toList();
```

```Java
List<ClientLDTO> clientsAndCourtiersLDTO = Arrays.stream(arrayOfClientCrmDTO).sorted(Comparator.comparing(ClientCrmDTO::getNom)).map(clientLightCrmMapper::toDTO).collect(Collectors.toList());  
  
String[] clients = clientsAndCourtiersLDTO.stream().filter(c -> c.getNumeroCourtier() == null).map(ClientLDTO::getId).map(Object::toString).toArray(String[]::new);  
String[] courtiers = clientsAndCourtiersLDTO.stream().map(ClientLDTO::getNumeroCourtier).filter(Objects::nonNull).toArray(String[]::new);
```

### Middleware et fonctions
```java
private final List<Function<Object, Object>> middlewares;
```
Le premier paramètre de la fonction est le type l'objet qui serra passé en paramètre de la fonction et le deuxième sera le type de  l'objet qui sera retourné.
```java
/**  
 * Methode qui sera appelé dans l'application spring pour définir la fonction qui sera appelée pour set les valeurs propres à l'application
 * Exemple : userName, userToken...
 * @param middleware la fonction à exécuter  
 */
 public void registerMiddleware(Function<LogBuilder, LogBuilder> middleware) {  
    this.middlewares.add(middleware);  
}

private LogBuilder callMiddlewares(LogBuilder initialLogBuilder) {  
    LogBuilder logBuilder = initialLogBuilder;  
    for (Function<LogBuilder, LogBuilder> middleware : middlewares) {  
        logBuilder = middleware.apply(logBuilder);  
    }  
    return logBuilder;  
}

//pour créer la fonction à exécuter
this.logBuilderService.registerMiddleware((lb) -> {  
	// traitement a faire 
    return lb;  
});
```
Faire un .apply() sur l'objet fonction avec en paramètre les paramètres de la fonction à exécuter
## Jackson (serialiser des objet en json)
Créer un serialiser custom pour pouvoir retourner vraiment le format de valeur qu'on veux
```java
class StringArraySerializer extends JsonSerializer<String[]> {  
    @Override  
    public void serialize(String[] strings, JsonGenerator jsonGenerator, SerializerProvider serializerProvider) throws IOException {  
        String serialized = String.join(",", strings);  
        jsonGenerator.writeString(serialized);  
    }  
}

@JsonSerialize(using = StringArraySerializer.class)  
private String[] entityKey = null;

```

### Callable
Permet de chercher si une valeur va pas lever une NPE 
```java
private <T> T safeGetExternalValue(Callable<T> getter) {  
    try {  
        return getter.call();  
    } catch (Exception e) {  
        return null;  
    }  
}
this.safeGetExternalValue(entity::getEntiteMetier)
```