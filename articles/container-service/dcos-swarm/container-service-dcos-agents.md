---
title: groepen met aaaDC/OS-agent voor Azure Container Service | Microsoft Docs
description: Hoe Hallo openbare en persoonlijke agent pools werken met een Azure Container Service DC/OS-cluster
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Groepen met DC/OS-agent voor Azure Container Service
DC/OS-clusters in Azure Container Service bevatten agent knooppunten in twee groepen, een openbare toepassingen en een persoonlijke toepassingen. Een toepassing kan worden geïmplementeerd tooeither groep, toegankelijkheid tussen computers in uw containerservice beïnvloeden. Hallo machines kunnen worden blootgesteld toohello internet (openbaar) of interne (particuliere) wilt bewaren. Dit artikel bevat een kort overzicht van waarom er groepen van openbare en persoonlijke zijn.


* **Persoonlijke agents**: persoonlijke agent knooppunten uitvoeren via een niet-routeerbaar netwerk. Dit netwerk is alleen toegankelijk vanuit Hallo beheerder zone of via Hallo openbare zone edge router. Standaard start DC/OS-apps op persoonlijke agent knooppunten. 

* **Openbare agents**: openbare agent knooppunten uitvoeren DC/OS-apps en services via een openbaar toegankelijk netwerk. 

Zie voor meer informatie over netwerkbeveiliging DC/OS Hallo [DC/OS-documentatie](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Agent-groepen implementeren

Hallo DC/OS-agent van toepassingen In Azure Container Service gemaakt als volgt:

* Hallo **persoonlijke groep** bevat Hallo-nummer van de agent-knooppunten opgeven wanneer u [Hallo DC/OS-cluster implementeren](container-service-deployment.md). 

* Hallo **openbare groep** in eerste instantie bevat een vooraf vastgesteld aantal knooppunten van de agent. Deze groep wordt automatisch toegevoegd wanneer Hallo DC/OS-cluster is ingericht.

Hallo persoonlijke pool en Hallo van openbare toepassingen worden virtuele Azure-machine-schaalsets. U kunt deze groepen wijzigen na de implementatie.

## <a name="use-agent-pools"></a>Agent pools gebruiken
Standaard **Marathon** implementeert een nieuwe toepassing toohello *persoonlijke* agent knooppunten. U hebt tooexplicitly Hallo toepassing toohello implementeren *openbare* knooppunten tijdens het maken van de toepassing hello Hallo. Selecteer Hallo **optioneel** tabblad en voer **slave_public** voor Hallo **geaccepteerde resourcerollen** waarde. Dit proces wordt beschreven [hier](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) en in Hallo [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentatie.

## <a name="next-steps"></a>Volgende stappen
* Lees meer over [beheer van uw DC/OS-containers](container-service-mesos-marathon-ui.md).

* Meer informatie over hoe te[Hallo firewall openen](container-service-enable-public-access.md) verstrekt door Azure tooallow openbare toegang tooyour DC/OS containers.

