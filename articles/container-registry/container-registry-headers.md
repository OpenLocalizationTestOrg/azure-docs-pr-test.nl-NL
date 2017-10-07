---
title: aaaAzure container register opslagplaatsen | Microsoft Docs
description: "Hoe toouse Azure Container register opslagplaatsen voor Docker-installatiekopieën"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Register-opslagplaatsen voor Azure-container

Azure Container registers zijn compatibel met een groot aantal services en orchestrators. toomake deze eenvoudiger tootrack Hallo bron services en agents waaruit ACR wordt gebruikt, we hebt gestart met behulp van Docker-kopveld Hallo in Hallo Docker.config bestand.



## <a name="viewing-repositories-in-hello-portal"></a>Opslagplaatsen in Hallo Portal weergeven

Hallo ACR headers volgt Hallo indeling:
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Cloud: Azure, Azure-Stack of andere government of land-specifieke Azure-clouds. Hoewel Azure Stack en government clouds worden momenteel niet ondersteund, schakelt u deze parameter toekomstige ondersteuning.
* Service: de naam van van Hallo-service.
* Optionalservicename: een optionele parameter voor services met subservices of toospecify een SKU (ex: web-apps overeenkomen met de Azure/app-service/web-apps).

Partnerservices en orchestrators zijn aangemoedigd toouse specifieke koptekst waarden toohelp met onze telemetrie. Gebruikers kunnen ook Hallo-waarde doorgegeven toohello header desgewenst wijzigen.

we willen ACR partners toouse toopopulate Hallo 'X-Meta-bron-Client' veld Hallo-waarden zijn hieronder:

| Naam service              | Koptekst                                |
| ------------------------- | ------------------------------------- |
| Azure Container Service   | Azure/compute/azure-container-service |
| App Service - Web-Apps    | Azure /-/ web-apps van app service            |
| App Service - Logic Apps  | Azure /-/ logic-apps van app service          |
| Batch                     | compute-Azure/batch                   |
| Cloud-Console             | Azure-cloud-console                   |
| Functies                 | compute-Azure-functies               |
| Internet der dingen - Hub  | iot-Azure-hub                         |
| HDInsight                 | data-Azure/hdinsight                  |
| Jenkins                   | Azure/jenkins                         |
| Machine Learning          | Azure/data/machile-learning           |
| Service Fabric            | Azure/compute/service-infrastructuur          |
| VSTS                      | Azure/vsts                            |


## <a name="next-steps"></a>Volgende stappen
[Meer informatie over registers en Hallo ondersteund services en orchestrators](container-registry-intro.md)
