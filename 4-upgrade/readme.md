# Mise à jour de Kubernetes

Objectif : Mettre à jour un cluster Kubernetes géré par Rancher 2

## 1: Mettre à jour le cluster

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue globale, navigation `Clusters` cliquez sur le menu à droite de votre cluster, puis cliquez sur  `Edit`
* Dans le panneau `Cluster Options` => `Kubernetes Options` , séléctionnez `v1.17.6-rancher2-1`
* Validez en cliquant sur `Save`en bas de la page

Vous devriez avoir un message `This cluster is currently Updating.` sur la vue Cluster.