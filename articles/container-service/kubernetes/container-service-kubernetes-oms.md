---
title: aaaMonitor Azure Kubernetes cluster - Operations Management | Microsoft Docs
description: Bewaking van Kubernetes cluster in Azure Container Service met behulp van Microsoft Operations Management Suite
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
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Een Azure Container Service-cluster met de Microsoft Operations Management Suite (OMS) bewaken

## <a name="prerequisites"></a>Vereisten
In dit scenario wordt ervan uitgegaan dat u hebt [gemaakt van een Kubernetes-cluster met behulp van Azure Container Service](container-service-kubernetes-walkthrough.md).

Ook wordt ervan uitgegaan dat u Hallo hebt `az` Azure cli en `kubectl` hulpprogramma's geïnstalleerd.

U kunt testen, hebt u Hallo `az` hulpprogramma is geïnstalleerd door te voeren:

```console
$ az --version
```

Als u geen Hallo `az` hulpprogramma is geïnstalleerd, er zijn instructies [hier](https://github.com/azure/azure-cli#installation).  
U kunt ook gebruiken [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), die Hallo heeft `az` Azure cli en `kubectl` hulpprogramma's voor u hebt geïnstalleerd.  

U kunt testen, hebt u Hallo `kubectl` hulpprogramma is geïnstalleerd door te voeren:

```console
$ kubectl version
```

Als u geen `kubectl` geïnstalleerd, u kunt uitvoeren:
```console
$ az acs kubernetes install-cli
```

tootest als u kubernetes sleutels die zijn geïnstalleerd in uw kubectl-hulpprogramma hebt die u kunt uitvoeren:
```console
$ kubectl get nodes
```

Als hello boven de fouten van de opdracht uit, moet u tooinstall kubernetes cluster sleutels in de kubectl tool. Met de volgende opdracht Hallo kunt u dat doen:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Bewaking van Containers met Operations Management Suite (OMS)

Microsoft Operations Management (OMS) is van Microsoft cloud-gebaseerde IT beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur. Container oplossing is een oplossing in OMS Log Analytics, waardoor u inventaris weergeven Hallo-container, prestaties en logboeken op één locatie. U kunt controleren, containers oplossen door bekijkt hello Logboeken in de centrale locatie en veel ruis veroorzaken verbruikt overtollige container op een host vinden.

![](media/container-service-monitoring-oms/image1.png)

Raadpleeg voor meer informatie over de oplossing Container toothe [Container oplossing Log Analytics](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>OMS installeren op Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Uw werkruimte-ID en sleutel ophalen
Hallo OMS-agent tootalk toohello-service moet toobe geconfigureerd met een werkruimte-id en een werkruimtesleutel. tooget hello werkruimte-id en sleutel moet u een OMS toocreate account op <https://mms.microsoft.com>. Volg Hallo stappen toocreate een account. Wanneer u klaar bent met het Hallo-account maken, moet u tooobtain uw id en -sleutel door te klikken op **instellingen**, klikt u vervolgens **verbonden bronnen**, en vervolgens **Linux-Servers**, zoals hieronder weergegeven.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Hallo OMS-agent met behulp van een DaemonSet installeren
DaemonSets worden gebruikt door Kubernetes toorun één exemplaar van een container op elke host in Hallo-cluster.
Ze zijn ideaal voor bewaking agenten uit te voeren.

Hier volgt Hallo [DaemonSet YAML bestand](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Sla het bestand tooa met de naam `oms-daemonset.yaml` en vervang Hallo placeholder waarden voor `WSID` en `KEY` door uw werkruimte-id en sleutel in Hallo-bestand.

Nadat u uw werkruimte-ID en sleutel toohello DaemonSet configuratie hebt toegevoegd, kunt u Hallo OMS-agent installeren op uw cluster Hello `kubectl` opdrachtregelprogramma:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Hallo OMS-agent met behulp van een geheim Kubernetes installeren
tooprotect uw OMS-werkruimte-ID en de sleutel die u kunt Kubernetes geheim gebruiken als onderdeel van DaemonSet YAML-bestand.

 - Hallo-script, geheime sjabloonbestand en Hallo DaemonSet YAML-bestand kopiëren (van [opslagplaats](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) en zorg ervoor dat ze zich op Hallo dezelfde directory. 
      - geheim script - geheim gen.sh genereren
      - geheime sjabloon - geheim template.yaml
   - Bestand DaemonSet YAML - omsagent-ds-secrets.yaml
 - Hallo-script uitvoeren. Hallo script vraagt naar Hallo OMS-werkruimte-ID en de primaire sleutel. Plaats die en Hallo script maakt een geheime yaml-bestand zodat u deze kunt uitvoeren.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Hallo geheimen schil maken door het uitvoeren van de volgende Hallo:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck hello volgende uitvoeren: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Maken van uw omsagent daemon-set door te voeren``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Conclusie
Dat is alles. U moet na een paar minuten kunnen toosee gegevens stromende tooyour OMS-dashboard.
