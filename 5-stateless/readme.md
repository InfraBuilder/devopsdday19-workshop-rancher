# Déploiement d'application stateless

Objectif : Déployer une application stateless et l'exposer

## 1: Déployer un workload avec une image publique

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue projet "Default" de votre cluster user**X**, sur l'onglet `Workloads`, cliquez sur `Deploy`
* Renseignez les champs suivants :
  * Name : "web"
  * Docker Image : "nginx"
* Puis cliquez sur `Launch` en bas de la page.

## 2: Exposer ce premier workload avec une Ingress

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue projet "Default" de votre cluster user**X**, sur l'onglet `Load Balancing`, cliquez sur `Add Ingress`
* Renseignez le nom de l'ingress avec la valeur "web"
* Dans la section `Rules`, séléctionnez `Specify a hostname to use` et renseignez le champs `Request Host` avec la valeur "web.user**X**.dday.ibd.sh" (**NB :** Pensez à remplacer **userX**)
* Dans la liste déroulante `Target`, sélectionnez le workload "web"
* Dans le champs `Port` indiquez le port "80"
* Puis cliquez sur `Save` en bas de la page.

Vous pouvez maintenant vous rendre sur l'url : `http://web.userX.dday.ibd.sh` (**NB :** Pensez à remplacer **userX**)

## 3: Déployer une image depuis un registry privée

* Sur l'interface de Rancher (https://rancher.dday.ibd.sh), sur la vue projet "Default" de votre cluster user**X**, dans la navigation `Resources`=> `Secrets`,  sur l'onglet `Registry Credentials`, cliquez sur `Add Registry`
* Dans le champs `Name`, renseignez le nom de la registry : "demo"
* Dans le champs `Adress`, sélectionnez "Custom" et renseignez l'URL de la registry : "registry.gitlab.com"
* Dans le champs `Username`, renseignez l'utilisateur de la registry : "ibddemo"
* Dans le champs `Password`, renseignez le mot de passe de la registry : "1oMv_gnVpHVA5zF5n3NJ"
* Puis cliquez sur `Save` en bas de la page.

La registry privée est à présent configurée pour notre projet. 

Déployez à présent un nouveau workload utilisant l'image `registry.gitlab.com/ibddemo/demo`, et exposez-là sur l'URL `http://demo.userX.dday.ibd.sh` (**NB :** Pensez à remplacer **userX**). Aidez-vous des points 1 et 2 si nécessaire.