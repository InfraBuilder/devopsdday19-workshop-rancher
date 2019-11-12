# Rancher haute dispo

Objectif : Déployer un serveur Rancher 2 en haute dispo

## 1: Créer le fichier cluster.yml de RKE

Sur le serveur bastion (bastion.dday.ibd.sh), créez un dossier `rancher` et déplacez vous dans ce dossier :

```bash
cd ~
mkdir rancher
cd rancher
```

Puis créez fichier `cluster.yml` contenant (**NB :** Pensez à remplacer tous les **userX**) : 

```yaml
ssh_key_path: ~/.ssh/id_rsa
nodes:
  - address: rancher01.userX.dday.ibd.sh
    user: userX
    role:
      - controlplane
      - etcd
      - worker
  - address: rancher02.userX.dday.ibd.sh
    user: userX
    role:
      - controlplane
      - etcd
      - worker
  - address: rancher03.userX.dday.ibd.sh
    user: userX
    role:
      - controlplane
      - etcd
      - worker
```

Et on déploie le cluster :

```bash
rke up
```

## 2: Vérification de l'accès à Kubernetes

Toujours sur le bastion, lancez la commande suivante :

```bash
export KUBECONFIG=~/rancher/kube_config_cluster.yml
kubectl get node
```

Vous devriez obtenir un résultat similaire à ce qui suit :

```
NAME                          STATUS   ROLES                      AGE   VERSION
rancher01.userX.dday.ibd.sh   Ready    controlplane,etcd,worker   65s   v1.15.5
rancher02.userX.dday.ibd.sh   Ready    controlplane,etcd,worker   65s   v1.15.5
rancher03.userX.dday.ibd.sh   Ready    controlplane,etcd,worker   65s   v1.15.5
```

## 3: Installation de Helm

```bash
kubectl -n kube-system create sa tiller
kubectl create clusterrolebinding tiller \
    --clusterrole cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller
```

## 4 : Installation de cert-manager

```bash
kubectl apply -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.9/deploy/manifests/00-crds.yaml
kubectl create namespace cert-manager
kubectl label namespace cert-manager certmanager.k8s.io/disable-validation=true
helm repo add jetstack https://charts.jetstack.io
helm repo update

helm install \
  --name cert-manager \
  --namespace cert-manager \
  --version v0.9.1 \
  jetstack/cert-manager
```

A ce stade vous devriez pouvoir lister les release Helm :

```bash
helm list
```

Vous devriez avoir le résultat suivant :

```
NAME        	REVISION	UPDATED                 	STATUS  	CHART              	APP VERSION	NAMESPACE
cert-manager	1       	Mon Nov XX 19:07:44 2019	DEPLOYED	cert-manager-v0.9.1	v0.9.1     	cert-manager
```

## 5 : Installation de rancher

On commence par ajouter le repository helm Rancher :

```bash
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
helm repo update
```

Et enfin on installe Rancher (**NB :** Pensez à remplacer **userX**) :

```bash
helm install rancher-stable/rancher \
  --name rancher \
  --namespace cattle-system \
  --set ingress.tls.source=letsEncrypt \
  --set letsEncrypt.email=dday@ibd.sh \
  --set hostname=rancher.userX.dday.ibd.sh
```

Après quelques instants, le temps que Rancher effectue le challenge HTTP de Letsencrypt, vous devriez pouvoir accéder à l'URL suivante avec un certificat SSL valide (**NB :** Pensez à remplacer **userX**) :

​	https://rancher.userX.dday.ibd.sh/