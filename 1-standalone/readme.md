# Rancher standalone (poc)

Objectif : Déployer un serveur Rancher 2 via Docker pour faire des tests

## 1: Déployer un conteneur Rancher 2

Sur le serveur rancher01 (rancher01.**userX**.dday.ibd.sh) : 

```bash
sudo docker run -d \
  -v /srv/rancher:/var/lib/rancher \
  -p 80:80 -p 443:443 \
  --name rancher \
  rancher/rancher:stable
```

## 2: Vérification

Pour accéder à l'interface de rancher, rendez-vous sur (**NB :** Pensez à remplacer **userX**) :

	https://rancher01.userX.dday.ibd.sh

## 3: Arrêt du conteneur

```bash
sudo docker stop rancher
sudo docker rm rancher
```

## 4 : [Optionnel] Suppression des données

```bash
sudo rm -rf /srv/rancher
```

