---
title: "Haute disponibilité Azure Analysis Services | Microsoft Docs"
description: "Garantissez la haute disponibilité Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.translationtype: Human Translation
ms.sourcegitcommit: 43aab8d52e854636f7ea2ff3aae50d7827735cc7
ms.openlocfilehash: 0a9bdf3afba87ba1e7a1047907ab9eeb0ef8a842
ms.contentlocale: fr-fr
ms.lasthandoff: 06/03/2017

---

# <a name="analysis-services-high-availability"></a>Haute disponibilité Analysis Services
Cet article décrit la garantie d’une haute disponibilité pour les serveurs Azure Analysis Services. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Garantissez une haute disponibilité au cours d’une interruption de service
Bien que le fait soit rare, un centre de données Azure peut subir une panne. En cas de panne, il entraîne une interruption de service qui peut durer de quelques minutes à plusieurs heures. La haute disponibilité est souvent obtenue grâce à la redondance des serveurs. Avec Azure Analysis Services, vous pouvez obtenir une redondance en créant des serveurs secondaires supplémentaires dans une ou plusieurs régions. Lorsque vous créez des serveurs redondants pour garantir la synchronisation des données et des métadonnées sur ces serveurs avec le serveur d’une région hors connexion, vous pouvez :

* Déployer des modèles sur des serveurs redondants dans d’autres régions. Cette méthode requiert le traitement des données sur votre serveur principal et sur les serveurs redondants en parallèle, garantissant ainsi la synchronisation de tous les serveurs.

* Sauvegardez les bases de données à partir de votre serveur principal et restaurez-les sur des serveurs redondants. Par exemple, vous pouvez automatiser les sauvegardes nocturnes vers le stockage Azure et procéder à la restauration vers d’autres serveurs redondants dans d’autres régions. 

Dans les deux cas, si votre serveur principal subit une panne, vous devez modifier les chaînes de connexion des clients de rapport afin de vous connecter au serveur dans un autre centre de données régional. Cette modification doit être envisagée en dernier recours et uniquement en cas de panne très grave du centre de données régional. Il est plus probable qu’une panne du centre de données hébergeant votre serveur principal réapparaisse en ligne avant que vous ne puissiez mettre à jour les connexions sur tous les clients. 



## <a name="related-information"></a>Informations connexes
[Sauvegarde et restauration](analysis-services-backup.md)   
[Gérer Azure Analysis Services](analysis-services-manage.md) 


