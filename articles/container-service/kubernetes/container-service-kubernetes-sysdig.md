---
title: aaaMonitor Azure Kubernetes cluster - Sysdig | Microsoft Docs
description: Bewaking van Kubernetes cluster in Azure Container Service met behulp van Sysdig
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Een Azure Container Service Kubernetes-cluster met behulp van Sysdig bewaken

## <a name="prerequisites"></a>Vereisten
In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).

Ook wordt ervan uitgegaan dat u hello azure cli en kubectl hulpprogramma's geïnstalleerd hebt.

U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:

```console
$ az --version
```

Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).

U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:

```console
$ kubectl version
```

Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a>Sysdig
Sysdig is een externe controle als een servicebedrijf die containers in uw Kubernetes cluster worden uitgevoerd in Azure kunt bewaken. Sysdig, moet een actieve Sysdig-account.
U kunt aanmelden voor een account op hun [site](https://app.sysdigcloud.com).

Nadat u bent aangemeld op toohello Sysdig cloud website, klikt u op uw gebruikersnaam en op de pagina Hallo ziet u uw 'toegangssleutel'. 

![Sysdig API-sleutel](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>Hallo Sysdig agents tooKubernetes installeren
uw containers, Sysdig wordt uitgevoerd een proces op elke computer met behulp van een Kubernetes toomonitor `DaemonSet`.
DaemonSets zijn Kubernetes API-objecten die één exemplaar van een container per computer worden uitgevoerd.
Ze zijn ideaal voor het installeren van hulpprogramma's als Hallo van Sysdig-bewakingsagent.

tooinstall hello Sysdig daemonset, moet u eerst downloaden [Hallo sjabloon](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) van sysdig. Sla dit bestand op als `sysdig-daemonset.yaml`.

Op Linux en OS X kunt u het volgende uitvoeren:

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

In PowerShell:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

Vervolgens bewerken dat bestand tooinsert uw toegangssleutel die u hebt ontvangen van uw account Sysdig.

Maak ten slotte Hallo DaemonSet:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>De bewaking weergeven
Eenmaal geïnstalleerd en wordt uitgevoerd, moeten Hallo agents gegevens back tooSysdig pomp.  Ga terug toothe [sysdig dashboard](https://app.sysdigcloud.com) en ziet u informatie over uw containers.

U kunt ook installeren Kubernetes-specifieke dashboards via de [wizard Nieuw dashboard](https://app.sysdigcloud.com/#/dashboards/new).
