---
title: "Utiliser l’extension de machine virtuelle Azure Docker | Microsoft Docs"
description: "Découvrez comment utiliser l’extension de machine virtuelle Docker sur Azure pour déployer un environnement Docker rapidement et en toute sécurité dans Azure en utilisant des modèles Resource Manager et Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.translationtype: HT
ms.sourcegitcommit: bfd49ea68c597b109a2c6823b7a8115608fa26c3
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.contentlocale: fr-fr
ms.lasthandoff: 07/25/2017

---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a>Création d’un environnement Docker dans Azure à l’aide de l’extension Docker VM
Docker est une solution courante de gestion de conteneurs et une plateforme de création d’images qui permet de travailler rapidement avec des conteneurs sous Linux. Dans Azure, il existe différentes méthodes pour déployer Docker selon vos besoins. Cet article se concentre sur l’utilisation de l’extension de machine virtuelle Docker et des modèles Azure Resource Manager avec Azure CLI 2.0. Vous pouvez également suivre ces étapes avec [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Présentation de l’extension Azure Docket VM
L’extension de machine virtuelle Docker Azure installe et configure le démon Docker, le client Docker et Docker Compose dans votre machine virtuelle (VM) Linux. L’extension Azure Docker VM vous offre plus de contrôle et de fonctionnalités que la simple utilisation de Docker Machine ou la création de votre propre hôte Docker. Ces fonctionnalités supplémentaires, telles que [Docker Compose](https://docs.docker.com/compose/overview/), permettent d’adapter l’extension Azure Docker VM à des environnements de développement ou de production plus robustes.

Pour plus d’informations sur les différentes méthodes de déploiement, y compris l’utilisation des services Docker Machine et Azure Container, consultez les articles suivants :

* Pour créer rapidement un prototype d’application, vous pouvez créer un hôte Docker unique en utilisant [Docker Machine](docker-machine.md).
* Pour créer des environnements prêts pour la production et évolutifs qui exploitent d’autres outils de planification et de gestion, vous pouvez déployer [un cluster Docker Swarm sur les services Azure Container](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a>Déployer un modèle avec l’extension de machine virtuelle Azure Docker
Nous allons utiliser un modèle de démarrage rapide existant pour créer une machine virtuelle Ubuntu qui utilise l’extension Azure Docker VM pour installer et configurer l’hôte Docker. Vous pouvez voir le modèle ici : [Simple deployment of an Ubuntu VM with Docker (Déploiement simple d’une machine virtuelle Ubuntu avec Docker)](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Vous devez disposer de la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et vous connecter à un compte Azure avec la commande [az login](/cli/azure/#login).

Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *westus* :

```azurecli
az group create --name myResourceGroup --location westus
```

Ensuite, déployez une machine virtuelle avec la commande [az group deployment create](/cli/azure/group/deployment#create) qui inclut l’extension de machine virtuelle Azure Docker de [ce modèle Azure Resource Manager sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Fournissez vos propres valeurs pour *newStorageAccountName*, *adminUsername*, *adminPassword* et *dnsNameForPublicIP* comme suit :

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Le déploiement prend quelques minutes. Une fois le déploiement terminé, [passez à l’étape suivante](#deploy-your-first-nginx-container) pour procéder à la connexion SSH à votre machine virtuelle. 

Sinon, si vous souhaitez retourner le contrôle à l’invite et permettre au déploiement de continuer en arrière-plan, ajoutez l’indicateur `--no-wait` à la commande précédente. Ce processus vous permet d’effectuer d’autres tâches dans l’interface CLI pendant que le déploiement se poursuit pendant quelques minutes. 

Vous pouvez ensuite afficher des détails sur l’état de l’hôte Docker avec la commande [az vm show](/cli/azure/vm#show). L’exemple suivant vérifie l’état de la machine virtuelle nommée *myDockerVM* (nom par défaut extrait du gabarit - ne pas modifier ce nom) dans le groupe de ressources nommé *myResourceGroup* :

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Lorsque cette commande renvoie *Succeeded* (Opération réussie), le déploiement est terminé et vous pouvez procéder à la connexion SSH à la machine virtuelle à l’étape suivante.

## <a name="deploy-your-first-nginx-container"></a>Déployer votre premier conteneur nginx
Pour afficher les détails de votre machine virtuelle, y compris le nom DNS, utilisez `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. Connectez-vous par SSH à votre nouvel hôte Docker à partir de votre ordinateur local, de la façon suivante :

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Une fois connecté à l’hôte Docker, nous allons exécuter un conteneur nginx :

```bash
sudo docker run -d -p 80:80 nginx
```

La sortie est similaire à l’exemple suivant lorsque l’image nginx est téléchargée et qu’un conteneur est démarré :

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Vérifiez l’état des conteneurs s’exécutant sur l’hôte Docker comme suit :

```bash
sudo docker ps
```

Le résultat est similaire à l’exemple suivant, indiquant que le conteneur nginx est en cours d’exécution et que les ports TCP 80 et 443 sont transférés :

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

Pour voir votre conteneur en action, ouvrez un navigateur web et entrez le nom DNS de votre hôte Docker :

![Exécution d’un conteneur ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Référence de modèle pour l’extension Azure Docker VM
L’exemple précédent utilise un modèle de démarrage rapide existant. Vous pouvez également déployer l’extension Azure Docker VM avec vos propres modèles Resource Manager. Pour cela, ajoutez ce qui suit à vos modèles Resource Manager, en définissant la valeur `vmName` de votre machine virtuelle en conséquence :

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Pour découvrir la procédure pas à pas d’utilisation de modèles Resource Manager, voir la [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez [configurer le port TCP du démon Docker](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), examiner la [sécurité Docker](https://docs.docker.com/engine/security/security/), ou déployer des conteneurs à l’aide de [Docker Compose](https://docs.docker.com/compose/overview/). Pour plus d’informations sur l’extension Azure Docker VM elle-même, consultez le [projet GitHub](https://github.com/Azure/azure-docker-extension/).

En savoir plus sur les options de déploiement supplémentaires Docker dans Azure :

* [Utiliser Docker Machine avec le pilote Azure](docker-machine.md)  
* [Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples sur une machine virtuelle Azure](docker-compose-quickstart.md).
* [Déploiement d’un cluster Azure Container Service](../../container-service/dcos-swarm/container-service-deployment.md)


