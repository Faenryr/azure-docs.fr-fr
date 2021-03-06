---
title: "Créez un registre de conteneur Docker privé dans Azure CLI | Microsoft Docs"
description: "Prise en main de la création et de la gestion de registres de conteneurs Docker privés avec Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.translationtype: HT
ms.sourcegitcommit: 83f19cfdff37ce4bb03eae4d8d69ba3cbcdc42f3
ms.openlocfilehash: 2875f4089231ed12a0312b2c2e077938440365c6
ms.contentlocale: fr-fr
ms.lasthandoff: 08/21/2017

---
# <a name="create-a-private-docker-container-registry-using-the-azure-cli-20"></a>Créez un registre de conteneur Docker privé à l’aide d’Azure CLI 2.0
Utilisez les commandes [d’Azure CLI 2.0](https://github.com/Azure/azure-cli) pour créer un registre de conteneur et gérer ses paramètres à partir de votre ordinateur Linux, Mac ou Windows. Vous pouvez également créer et gérer des registres de conteneur à l’aide du [portail Azure](container-registry-get-started-portal.md) ou par programme avec [l’API REST](https://go.microsoft.com/fwlink/p/?linkid=834376) de Container Registry.


* Pour plus d’informations, notamment sur les concepts, voir la [page de présentation](container-registry-intro.md)
* Pour obtenir de l’aide concernant les commandes CLI de Container Registry (commandes `az acr`), transmettez le paramètre `-h` à toutes les commandes.


## <a name="prerequisites"></a>Composants requis
* **Azure CLI 2.0** : pour installer et découvrir la CLI 2.0, consultez les [instructions d’installation](/cli/azure/install-azure-cli). Connectez-vous à votre abonnement Azure en exécutant `az login`. Pour plus d’informations, consultez [Prise en main CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Groupe de ressources** : créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) avant de créer un registre de conteneur, ou utilisez un groupe de ressources existant. Assurez-vous que le groupe de ressources est dans un emplacement où le service Container Registry est [disponible](https://azure.microsoft.com/regions/services/). Pour créer un groupe de ressources à l’aide de la CLI 2.0, consultez la [référence de l’interface CLI 2.0](/cli/azure/group).
* **Compte de stockage** (facultatif) : créez un [compte de stockage](../storage/common/storage-introduction.md) Azure standard pour prendre en charge le registre de conteneur dans le même emplacement. Si vous ne spécifiez pas de compte de stockage lors de la création d’un registre avec `az acr create`, la commande en crée un pour vous. Pour créer un compte de stockage à l’aide de la CLI 2.0, consultez la [référence de l’interface CLI 2.0](/cli/azure/storage/account). Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.
* **Principal de service** (facultatif) : lorsque vous créez un registre avec la CLI, par défaut son accès n’est pas configuré. Selon vos besoins, vous pouvez affecter un principal de service Azure Active Directory existant à un registre (ou en créer et en affecter un nouveau), ou activer le compte d’utilisateur Admin du registre. Consultez les sections disponibles plus loin dans cet article. Pour plus d’informations sur l’accès au registre, consultez la section relative à [l’authentification auprès d’un conteneur](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Créer un registre de conteneur
Exécutez la commande `az acr create` pour créer un registre de conteneur.

> [!TIP]
> Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres. Dans cet exemple, le nom de registre est `myRegistry1`, mais vous pouvez le remplacer par un nom unique de votre choix.
>
>

La commande ci-après utilise les paramètres minimaux pour créer le registre de conteneurs `myRegistry1` dans le groupe de ressources `myResourceGroup`, et en utilisant la référence SKU *De base* :

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` est facultatif. S’il n’est pas spécifié, un compte de stockage est créé avec un nom comprenant le nom de Registre et un horodatage dans le groupe de ressources spécifié.

Une fois le registre créé, la sortie ressemble à ce qui suit :

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Notez les poins suivants :

* `id` : identificateur du registre dans votre abonnement, dont vous avez besoin si vous souhaitez affecter un principal de service.
* `loginServer` : le nom complet à utiliser pour [se connecter au registre](container-registry-authentication.md). Dans cet exemple, le nom est `myregistry1.exp.azurecr.io` (en minuscules).

## <a name="assign-a-service-principal"></a>Affecter un principal de service
Utilisez les commandes CLI 2.0 pour affecter un principal de service Azure Active Directory à un registre. Le principal du service dans ces exemples est affecté au rôle de propriétaire, mais vous pouvez attribuer [d’autres rôles](../active-directory/role-based-access-control-configure.md) si vous le souhaitez.

### <a name="create-a-service-principal-and-assign-access-to-the-registry"></a>Créer un principal de service et attribuer l’accès au registre
Dans la commande suivante, un nouveau principal de service dispose de l’accès du rôle de propriétaire dans l’identificateur de registre transmis avec le paramètre `--scopes`. Spécifiez un mot de passe fort avec le paramètre `--password`.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Affecter un principal de service existant
Si vous avez déjà un principal de service et que vous souhaitez lui attribuer l’accès du rôle de propriétaire au registre, exécutez une commande similaire à l’exemple suivant. Vous transmettez l’ID d’application du principal de service à l’aide du paramètre `--assignee` :

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Gérer les informations d’identification de l’administrateur
Un compte d’administrateur est automatiquement créé pour chaque registre de conteneur et est désactivé par défaut. Les exemples suivants montrent des commandes CLI `az acr` permettant de gérer les informations d’identification d’administrateur pour votre registre de conteneur.

### <a name="obtain-admin-user-credentials"></a>Obtenir les informations d’identification de l’utilisateur Admin
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Activer l’utilisateur Admin pour un registre existant
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Désactiver l’utilisateur Admin pour un registre existant
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Répertorier les images et les balises
Utilisez les commandes CLI `az acr` pour interroger les images et les balises dans un référentiel.

> [!NOTE]
> Actuellement, Container Registry ne prend pas en charge la commande `docker search` permettant d’effectuer une requête sur les images et les balises.


### <a name="list-repositories"></a>Répertorier les référentiels
L’exemple suivant répertorie les référentiels dans un registre, au format JSON (JavaScript Object Notation) :

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Répertorier les balises
L’exemple suivant répertorie les balises sur le référentiel **exemples/nginx**, au format JSON :

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Étapes suivantes
* [Effectuer un push de votre première image à l’aide de l’interface CLI Docker](container-registry-get-started-docker-cli.md)

