``` d
healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9200/_cluster/health?wait_for_status=yellow"]
      interval: 1m30s
      timeout: 30s
      start_period: 30s
      retries: 3
```

permet de vérifier qu'un service est toujours en cours d'exécution

dans le service qui dépend du service qui est vérifié
```d
depends_on:  
  elasticsearch:  
    condition: service_healthy
```

possibilité d'ajouter des profiles pour décider quels services on veut executer
```
podman compose --profile application up
```
