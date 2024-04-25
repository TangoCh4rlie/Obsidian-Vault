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


### Création de template  pour les index
ca parmet d'avoir des index avec toujours la meme structure que l'on peut créer selon un paterne
**ne pas oublier de cocher auto-create** sinon c'est trop chiant sa mère

exemple:
```
PUT _index_template/my-log-template
{
  "template": {
	"settings": {
      "index": {
        "lifecycle": {
          "name": "my-aux-log"
        }
      }
    },
    "mappings": {
      "properties": {
        "accessType": {
          "type": "text"
        },
        "userToken": {
          "type": "text"
        },
        "accessDate": {
          "type": "date"
        },
        "entityType": {
          "type": "text"
        },
        "entityKey": {
          "type": "text"
        },
        "comment": {
          "type": "text"
        },
        "userEmail": {
          "type": "text"
        },
        "userType": {
          "type": "text"
        },
        "appSource": {
          "eager_global_ordinals": false,
          "index_phrases": false,
          "fielddata": false,
          "norms": true,
          "index": true,
          "store": false,
          "type": "text",
          "index_options": "positions"
        },
        "userName": {
          "type": "text"
        },
        "appAccess": {
          "type": "text"
        },
        "userId": {
          "type": "long"
        }
      }
    },
    "aliases": {
      "aux-log": {}
    }
  },
  "index_patterns": [
    "aux-log-*"
  ],
  "composed_of": [],
  "allow_auto_create": true
}
```
`indices.lifecycle.poll_interval` ce champs permet de modifier l'intervalle de temps pour check les life cycle des index (passer de hot à warm à cold …)