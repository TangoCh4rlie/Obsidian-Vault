Installation de podman pour pouvoir lancer elastic et kibana
Executer le script bash pour redéfinir le découpage de la mémoire

podman compose up

localhost:5601 pour la visualisation des données avec kibana
localhost:9200 pour l'api elastic

créer un index
PUT -> http://localhost:9200/logs

ajouter des données
POST -> http://localhost:9200/logs/_doc
dans le body mettre les données

récupérer des données
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
