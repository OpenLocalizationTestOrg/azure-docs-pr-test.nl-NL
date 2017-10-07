---
title: aaaMonitor Azure Kubernetes cluster met Datadog | Microsoft Docs
description: Bewaking van Kubernetes cluster in Azure Container Service met behulp van Datadog
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Een Azure Container Service-cluster met DataDog bewaken

## <a name="prerequisites"></a>Vereisten
In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).

Ook wordt ervan uitgegaan dat u Hallo hebt `az` Azure cli en `kubectl` hulpprogramma's geïnstalleerd.

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

## <a name="datadog"></a>DataDog
Datadog is een controleservice die bewakingsgegevens moeten worden verzameld uit uw containers in uw Azure Container Service-cluster. Datadog heeft een Docker-integratie Dashboard waarin u de specifieke metrische gegevens binnen uw containers kunt zien. Metrische gegevens die afkomstig zijn van uw containers worden ingedeeld op basis van CPU, geheugen, netwerk en i/o. Datadog splitst metrische gegevens in containers en afbeeldingen.

U moet eerst te[een account maken](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>Hallo Datadog Agent installeren met een DaemonSet
DaemonSets worden gebruikt door Kubernetes toorun één exemplaar van een container op elke host in Hallo-cluster.
Ze zijn ideaal voor bewaking agenten uit te voeren.

Nadat u zich bij Datadog hebt aangemeld, kunt u volgen Hallo [Datadog instructies](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents op uw cluster met behulp van een DaemonSet.

## <a name="conclusion"></a>Conclusie
Dat is alles. Zodra het Hallo-agents actief zijn en gegevens in de console Hallo waarop uitgevoerd. u ziet in een paar minuten. U kunt ook bezoeken Hallo geïntegreerd [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee een samenvatting van uw cluster.
