Installation de podman pour pouvoir lancer elastic et kibana
Executer le script bash pour redéfinir le découpage de la mémoire

**docker-compose.yml dans File**

podman compose up

localhost:5601 pour la visualisation des données avec kibana
localhost:9200 pour l'api elastic

créer un index
PUT -> http://localhost:9200/logs

ajouter des données
POST -> http://localhost:9200/logs/_doc
dans le body mettre les données

récupérer des données
```
GET -> http://localhost:9200/_search
POST -> http://localhost:9200/_search
rajouter des conditions
{
    "query": {
        "query_string": {
            "query": "fou"
        }
    }
}
```

```
services:
  elasticsearch:
    image: elasticsearch:8.12.2
    ports:
      - 9200:9200/tcp
      - 9300:9300/tcp
    volumes:
      - ./data:/usr/share/elasticsearch/data:rw
    environment:
      - xpack.security.enabled=false
      - discovery.type=single-node
      - http.cors.enabled=true
      - http.cors.allow-origin="*"
      - http.cors.allow-methods=OPTIONS,HEAD,GET,POST,PUT,DELETE
      - http.cors.allow-headers=X-Requested-With,X-Auth-Token,Content-Type,Content-Length
      - http.cors.allow-credentials=true
  kibana:
    image: kibana:8.12.2
    ports:
      - 5601:5601/tcp
    depends_on:
      - elasticsearch
```

### Création de template  pour les index
ca parmet d'avoir des index avec toujours la meme structure que l'on peut créer selon un paterne
**ne pas oublier de cocher auto-create** sinon c'est trop chiant sa mère

exemple:
```
PUT _index_template/my-log-template  

{  
  "version": 1,  
  "template": {  
    "settings": {  
      "index": {  
        "lifecycle": {  
          "name": "my-aux-log"  
        }      }    },    "mappings": {  
      "properties": {  
        "accessDate": {  
          "type": "date"  
        },        "accessType": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "appAccess": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "comment": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "entityKey": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "entityType": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "userEmail": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "userId": {  
          "type": "long"  
        },        "userName": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "userToken": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "index_options": "docs",  
          "split_queries_on_whitespace": false,  
          "doc_values": true  
        },        "userType": {  
          "eager_global_ordinals": false,  
          "norms": false,  
          "index": true,  
          "store": false,  
          "type": "keyword",  
          "split_queries_on_whitespace": false,  
          "index_options": "docs",  
          "doc_values": true  
        }      }    },    "aliases": {  
      "aux-log": {}  
    }  },  "index_patterns": [  
    "aux-log-*"  ],  "composed_of": [],  
  "allow_auto_create": true  
}


```

`indices.lifecycle.poll_interval` ce champs permet de modifier l'intervalle de temps pour check les life cycle des index (passer de hot à warm à cold …)

**Si on veut faire de la data visualisation avec kibana sur des champs text il faut les passer en keyword**


```http
PUT /_data_stream/aux-log-stream

POST /_reindex?wait_for_completion=false
{
  "source": {
    "index": ".ds-aux-log-data-stream-2024.09.06-000001"
  },
  "dest": {
    "index": "aux-log-stream",
    "op_type": "create"
  }
}

GET /_tasks/wNpW8VHsQgyP3b19F2jQCw:51400609
```

