---
title: een Azure-Kubernetes aaaMonitor cluster met CoScale | Microsoft Docs
description: Een cluster Kubernetes in Azure Container Service met behulp van CoScale bewaken
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Een Azure Container Service Kubernetes-cluster met CoScale bewaken

In dit artikel wordt uitgelegd hoe u dat toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor alle knooppunten en containers in uw Kubernetes-cluster in Azure Container Service. U moet een account met CoScale voor deze configuratie. 


## <a name="about-coscale"></a>Over CoScale 

CoScale is een controle platform waarmee metrische gegevens en gebeurtenissen verzameld uit alle containers in verschillende orchestration-platforms. CoScale biedt volledige stack bewaking voor Kubernetes omgevingen. Biedt visualisaties en analytics voor alle lagen in Hallo-stack: Hallo OS, Kubernetes, Docker en toepassingen die worden uitgevoerd binnen uw containers. CoScale biedt diverse ingebouwde bewaking dashboards en hieraan de ingebouwde afwijkingsdetectie detectie tooallow operators en ontwikkelaars toofind infrastructuur- en problemen snel.

![CoScale gebruikersinterface](./media/container-service-kubernetes-coscale/coscale.png)

Zoals u in dit artikel, kunt u agents installeren op een Kubernetes cluster toorun CoScale als een SaaS-oplossing. Als u tookeep uw gegevens op de locatie wilt, is CoScale ook beschikbaar voor lokale installatie.


## <a name="prerequisites"></a>Vereisten

U moet eerst te[maken van een account CoScale](https://www.coscale.com/free-trial).

In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).

Ook wordt ervan uitgegaan dat u Hallo hebt `az` Azure CLI en `kubectl` hulpprogramma's geïnstalleerd.

U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:

```azurecli
az --version
```

Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](/cli/azure/install-azure-cli).

U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:

```bash
kubectl version
```

Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>Hallo CoScale agent installeren met een DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) worden gebruikt door Kubernetes toorun één exemplaar van een container op elke host in Hallo-cluster.
Ze zijn ideaal voor bewaking agenten zoals Hallo CoScale agent uit te voeren.

Nadat u zich aanmeldt tooCoScale, gaat u toohello [agent pagina](https://app.coscale.com/) tooinstall CoScale agents op uw cluster met behulp van een DaemonSet. Hallo CoScale gebruikersinterface biedt begeleide configuratie stappen toocreate een agent en de controle van uw volledige Kubernetes cluster starten.

![De agentconfiguratie coScale](./media/container-service-kubernetes-coscale/installation.png)

toostart Hallo-agent op Hallo cluster Hallo opgegeven opdracht uitvoeren:

![Hallo CoScale agent starten](./media/container-service-kubernetes-coscale/agent_script.png)

Dat is alles. Zodra Hallo agents actief en werkend zijn, moet u gegevens in de console Hallo zien over een paar minuten. Ga naar Hallo [agent pagina](https://app.coscale.com/) toosee een samenvatting van uw cluster aanvullende configuratiestappen uitvoeren en dashboards zoals Hallo Zie **Kubernetes cluster overzicht**.

![Overzicht van de cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

Hallo CoScale agent wordt automatisch geïmplementeerd op nieuwe computers in het Hallo-cluster. Hallo-agent wordt automatisch bijgewerkt wanneer een nieuwe versie wordt uitgebracht.


## <a name="next-steps"></a>Volgende stappen

Zie Hallo [CoScale documentatie](http://docs.coscale.com/) en [blog](https://www.coscale.com/blog) voor meer informatie over CoScale bewakingsoplossingen. 

