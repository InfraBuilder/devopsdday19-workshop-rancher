# Déploiement de Kubernetes

Objectif : Déployer un cluster Kubernetes géré par Rancher 2

## 1: Créer le cluster sur l'interface de Rancher

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue globale cliquez sur `Add cluster`
* Séléctionnez `From existing nodes (Custom)`
* Renseignez le nom du cluster : "**userX**"  (**NB :** Pensez à remplacer **userX**), puis cliquez sur `next`en bas de la page

Vous êtes à présent sur la page `Add Cluster - Custom`, cette page est un générateur de commande docker, qui va nous permettre d'ajouter les noeuds au cluster

## 2: Ajouter les noeuds master

* Dans le panneau `Node Options` , cochez **uniquement** les cases :
  * `etcd`
  * `controlplane`
* Copier la commande docker générée
* Lancez cette commande sur les serveurs Master01, Master02 et Master03 (master**0Y**.user**X**.dday.ibd.sh)

## 3: Ajouter les noeuds worker

* Dans le panneau `Node Options` , cochez **uniquement** les cases :
  * `worker`
* Copier la commande docker générée
* Lancez cette commande sur les serveurs Worker01, Worker02 et Worker03 (worker**0Y**.user**X**.dday.ibd.sh)

## 4: Terminer la création du cluster

* Vous pouvez maintenant cliquer sur `done`