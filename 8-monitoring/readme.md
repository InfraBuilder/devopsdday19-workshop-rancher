# Déploiement d'application stateless

Objectif : Déployer une application stateful et l'exposer

## 1: Déployer wordpress via les App

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue "cluster" de votre cluster user**X**, navigation `Cluster`, cliquez sur `Enable Monitoring to see live metrics`
* Pour `Enable Persistent Storage for Prometheus`, choisissez "true"
* Pour `Enable Persistent Storage for Grafana`, choisissez "true"
* Puis cliquez sur `Enable` en bas de la page.
* Retournez sur l'onglet de navigation `Cluster`
* Attendez quelques minutes pour voir apparaitre le monitoring intégré

