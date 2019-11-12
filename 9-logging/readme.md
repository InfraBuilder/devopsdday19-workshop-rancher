# Gestion des logs

Objectif : Déployer une centralisation des logs

## 1: Déployer une stack EFK via les App

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue projet "System" de votre cluster user**X**, navigation `App`, cliquez sur `Launch`
* Séléctionnez `efk`

* Dans la section `KIBANA CONFIG`, à la question  `Kibana Service Type`, choisissez "ClusterIP"
* Dans la section `ELASTICSEARCH CONFIG`, à la question  `Enable Elasticsearch Persistent Volume`, choisissez "true"
* Puis cliquez sur `Launch` en bas de la page.

