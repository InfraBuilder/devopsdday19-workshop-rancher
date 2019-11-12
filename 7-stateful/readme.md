# Déploiement d'application stateful

Objectif : Déployer une application stateful et l'exposer

## 1: Déployer wordpress via les App

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue projet "Default" de votre cluster user**X**, navigation `App`, cliquez sur `Launch`
* Séléctionnez `Wordpress`
* Dans la section `WORDPRESS SETTINGS`, à la question `WordPress Persistent Volume Enabled` sélectionnez "true"
* Dans la section `DATABASE SETTINGS`, à la question `MariaDB Persistent Volume Enabled` sélectionnez "true"
* Dans la section `SERVICES AND LOAD BALANCING`, pour le champs `Hostname` choisissez `Specify a hostname to use` et rensignez  "blog.user**X**.dday.ibd.sh" (**NB :** Pensez à remplacer **userX**)
* Puis cliquez sur `Launch` en bas de la page.

