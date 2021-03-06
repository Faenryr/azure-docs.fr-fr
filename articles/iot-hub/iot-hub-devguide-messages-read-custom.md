---
title: "Présentation des points de terminaison Azure IoT Hub personnalisés | Microsoft Docs"
description: "Guide du développeur : utilisation de règles de routage pour router les messages appareil-à-cloud vers des points de terminaison."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.translationtype: Human Translation
ms.sourcegitcommit: 5edc47e03ca9319ba2e3285600703d759963e1f3
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.contentlocale: fr-fr
ms.lasthandoff: 05/31/2017


---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Utiliser des itinéraires de messages et des points de terminaison personnalisés pour les messages appareil-à-cloud

IoT Hub vous permet d’acheminer les [messages appareil-à-cloud][lnk-device-to-cloud] vers des points de terminaison exposés au service IoT Hub en fonction de leurs propriétés. Les règles d’acheminement vous offrent la souplesse nécessaire pour envoyer des messages au bon endroit sans avoir besoin de services supplémentaires pour les traiter ou pour écrire du code supplémentaire. Chaque règle d’acheminement que vous configurez a les propriétés suivantes :

| Propriété      | Description |
| ------------- | ----------- |
| **Nom**      | Nom unique qui identifie la règle. |
| **Source**    | Origine du flux de données qui fait l’objet du traitement. Par exemple, télémétrie des appareils. |
| **Condition** | Expression de requête de la règle d’acheminement exécutée sur les en-têtes et le corps du message et utilisée pour déterminer s’il existe une correspondance pour le point de terminaison. Pour plus d’informations sur la construction d’une condition d’acheminement, consultez la [Référence : langage de requête pour jumeaux d’appareils et travaux][lnk-devguide-query-language]. |
| **Point de terminaison**  | Nom du point de terminaison auquel IoT Hub envoie des messages qui correspondent à la condition. Les points de terminaison doivent être dans la même région que l’IoT Hub, sinon des écritures inter-régions peuvent vous être facturées. |

Un seul message peut correspondre à la condition de plusieurs règles d’acheminement, auquel cas IoT Hub remet le message au point de terminaison associé à chaque règle ayant affiché une correspondance. Par ailleurs, IoT Hub déduplique automatiquement la remise des messages ; par conséquent, si un message correspond à plusieurs règles qui ont toutes la même destination, il n’est écrit qu’une seule fois dans cette destination.

Un hub IoT a par défaut un [point de terminaison intégré][lnk-built-in]. Vous pouvez créer des points de terminaison personnalisés pour y acheminer les messages en liant d’autres services de votre abonnement au hub. IoT Hub prend actuellement en charge les points de terminaison personnalisés Event Hubs, les files d’attente Service Bus et les rubriques Service Bus.

> [!WARNING]
> Les files d’attente et rubriques Service Bus dont les options **Sessions** ou **Détection des doublons** sont activées ne sont pas prises en charge comme points de terminaison personnalisés.

Pour plus d’informations sur la création de points de terminaison personnalisés dans IoT Hub, consultez la page [Points de terminaison IoT Hub][lnk-devguide-endpoints].

Pour plus d’informations sur la lecture à partir de points de terminaison personnalisés, consultez :

* Lecture à partir [d’Event Hubs][lnk-getstarted-eh].
* Lecture à partir de [files d’attente Service Bus][lnk-getstarted-queue].
* Lecture à partir de [rubriques Service Bus][lnk-getstarted-topic].

### <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les points de terminaison IoT Hub, consultez [Points de terminaison IoT Hub][lnk-devguide-endpoints].

Pour plus d’informations sur le langage de requête que vous utilisez pour définir des règles de routage, consultez [Langage de requête d’IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-devguide-query-language].

Le didacticiel [Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires][lnk-d2c-tutorial] vous montre comment utiliser des règles de routage et des points de terminaison personnalisés.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md

