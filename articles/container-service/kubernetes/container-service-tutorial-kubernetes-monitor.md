---
title: zelfstudie voor aaaAzure Container Service - Monitor Kubernetes | Microsoft Docs
description: Zelfstudie voor Azure Container Service - Monitor Kubernetes met Microsoft Operations Management Suite (OMS)
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Monitor voor een cluster Kubernetes met Operations Management Suite

Uw cluster Kubernetes en containers is niet kritiek, vooral wanneer u een productiecluster op schaal met meerdere apps beheren. 

U kunt profiteren van verschillende Kubernetes bewakingsoplossingen, van Microsoft of andere providers. In deze zelfstudie maakt u uw cluster Kubernetes controleren met behulp van Hallo Containers oplossing in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), van de Microsoft cloud-gebaseerde IT-oplossing. (Hallo OMS Containers oplossing is in preview.)

Deze zelfstudie maakt deel uit zeven zeven, heeft betrekking op Hallo taken te volgen:

> [!div class="checklist"]
> * OMS-werkruimte-instellingen ophalen
> * Instellen van OMS-agents op Hallo Kubernetes knooppunten
> * Toegang tot informatie over prestatiebewaking op Hallo OMS-portal of Azure-portal

## <a name="before-you-begin"></a>Voordat u begint

In vorige zelfstudies, een toepassing is ingepakt in container-installatiekopieën, maar deze installatiekopieën geüpload tooAzure register van de Container en een Kubernetes-cluster dat is gemaakt. Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md). 

Deze zelfstudie vereist ten minste een Kubernetes-cluster met knooppunten voor Linux-agent en een account van Operations Management Suite (OMS). Indien nodig, zich aanmelden voor een [gratis proefabonnement van OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Werkruimte-instellingen ophalen

Wanneer u toegang hebt tot Hallo [OMS-portal](https://mms.microsoft.com), gaat u te**instellingen** > **verbonden bronnen** > **Linux-Servers**. Daar vindt u Hallo *werkruimte-ID* en een primaire of secundaire site *Werkruimtesleutel*. Noteer deze waarden, u moet tooset up OMS-agents op Hallo-cluster.

## <a name="set-up-oms-agents"></a>Instellen van OMS-agents

Hier volgt een tooset YAML-bestand van OMS-agents op Hallo Linux clusterknooppunten. Het maken van een Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), die een enkele identiek schil wordt uitgevoerd op elk clusterknooppunt. Hallo DaemonSet resource is ideaal voor het implementeren van een agent voor toepassingsbewaking. 

Hallo na tooa tekstbestand met de naam opslaan `oms-daemonset.yaml`, en vervang de waarden van het Hallo-tijdelijke aanduiding voor *myWorkspaceID* en *myWorkspaceKey* OMS-werkruimte-ID en sleutel van uw. (In productie, kunt u deze waarden coderen als geheimen.)

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Hallo DaemonSet maken met de volgende opdracht Hallo:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee die Hallo DaemonSet is gemaakt, worden uitgevoerd:

```azurecli-interactive
kubectl get daemonset
```

Uitvoer is vergelijkbaar toohello volgende:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Nadat het Hallo-agents worden uitgevoerd, duurt het enkele minuten voor OMS tooingest en proces Hallo gegevens.

## <a name="access-monitoring-data"></a>Toegang tot bewakingsgegevens

Weergeven en analyseren van Hallo OMS container bewakingsgegevens Hello [Container oplossing](../../log-analytics/log-analytics-containers.md) in Hallo OMS-portal of hello Azure-portal. 

tooinstall hello Container oplossing met behulp van Hallo [OMS-portal](https://mms.microsoft.com), gaat u te**galerie met oplossingen**. Voeg vervolgens **Container oplossing**. Hallo Containers oplossing ook toevoegen van Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

In de OMS-portal hello, zoekt u naar een **Containers** tegel samenvatting op Hallo OMS-dashboard. Klik op de tegel Hallo voor meer informatie, met inbegrip van: container gebeurtenissen, fouten, status, inventaris van de installatiekopie en CPU- en geheugengebruik. Voor meer gedetailleerde informatie op een rij op een tegel of voer een [logboek zoeken](../../log-analytics/log-analytics-log-searches.md).

![Containers dashboard in OMS-portal](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

Op deze manier in hello Azure-portal, gaat u te**logboekanalyse** en selecteer de Werkruimtenaam van uw. Hallo toosee **Containers** tegel samenvatting, klikt u op **oplossingen** > **Containers**. toosee, klikt u op de tegel Hallo.

Zie Hallo [Azure Log Analytics-documentatie](../../log-analytics/index.md) voor gedetailleerde hulp bij het uitvoeren van query's en analyseren van bewakingsgegevens.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt bewaakt u uw cluster Kubernetes met OMS. Taken aan de orde opgenomen:

> [!div class="checklist"]
> * OMS-werkruimte-instellingen ophalen
> * Instellen van OMS-agents op Hallo Kubernetes knooppunten
> * Toegang tot informatie over prestatiebewaking op Hallo OMS-portal of Azure-portal


Volg deze link toosee vooraf gemaakte scriptvoorbeelden voor Container Service.

> [!div class="nextstepaction"]
> [Azure Container Service script-voorbeelden](cli-samples.md)
