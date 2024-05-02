Utilisation de stream
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