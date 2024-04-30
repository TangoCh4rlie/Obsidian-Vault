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