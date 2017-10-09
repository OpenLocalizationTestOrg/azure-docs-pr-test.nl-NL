---
title: zelfstudie voor aaaAzure Container Service - toepassing schalen | Microsoft Docs
description: Zelfstudie voor Azure Container Service - toepassing schalen
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
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Schaal Kubernetes gehele product en Kubernetes infrastructuur

Als u Hallo zelfstudies volgt hebt, hebt u een werkende Kubernetes cluster in Azure Container Service en u hello Azure stemmen app hebt geïmplementeerd. 

In deze zelfstudie maakt deel uit vijf zeven, uitbreiden Hallo gehele product in Hallo-app en probeer het schil automatisch schalen. U leert ook hoe tooscale Hallo aantal Azure VM-agent knooppunten toochange Hallo capaciteit voor het hosten van werkbelastingen van het cluster. Taken zijn voltooid, zijn onder andere:

> [!div class="checklist"]
> * Handmatig schalen Kubernetes gehele product
> * Configureren voor automatisch schalen gehele product Hallo app-front-end uitgevoerd
> * Hallo Kubernetes Azure-agent knooppunten schalen

In volgende zelfstudies hello Azure stem toepassing wordt bijgewerkt en Operations Management Suite toomonitor hello Kubernetes cluster geconfigureerd.

## <a name="before-you-begin"></a>Voordat u begint

In vorige zelfstudies, een toepassing is ingepakt in een installatiekopie van een container, maar deze installatiekopie geüpload tooAzure register van de Container en een Kubernetes-cluster dat is gemaakt. Hallo toepassing is klikt u vervolgens op Hallo Kubernetes cluster uitgevoerd. Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, retourneren toohello [zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md). 

Deze zelfstudie vereist ten minste een Kubernetes-cluster met een actieve toepassing.

## <a name="manually-scale-pods"></a>Handmatig schalen gehele product

Tot dusver hello Azure stem front-end- en Redis-exemplaar zijn geïmplementeerd, elk met een enkele replica. tooverify, Voer Hallo [kubectl ophalen](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.

```azurecli-interactive
kubectl get pods
```

Uitvoer:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Hallo-nummer van het gehele product in Hallo handmatig wijzigen `azure-vote-front` implementatie met behulp van Hallo [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) opdracht. In dit voorbeeld verhoogt Hallo nummer too5.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Voer [kubectl ophalen gehele product](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes maken van Hallo gehele product. Na een minuut of zo worden Hallo aanvullende gehele product uitgevoerd:

```azurecli-interactive
kubectl get pods
```

Uitvoer:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Gehele product automatisch schalen

Biedt ondersteuning voor Kubernetes [horizontale schil automatisch schalen](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust Hallo aantal gehele product in een implementatie, afhankelijk van de CPU-gebruik of andere metrische gegevens selecteren. 

toouse hello autoscaler, moeten uw gehele product hebben met het aanvragen van de CPU en limieten die zijn gedefinieerd. In Hallo `azure-vote-front` implementatie, front-container aanvragen 0,25 CPU, met een limiet van 0,5 Hallo CPU. Hallo instellingen eruitzien als:

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

Hallo volgende voorbeeld wordt Hallo [kubectl automatisch schalen](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) tooautoscale Hallo aantal gehele product in Hallo opdracht `azure-vote-front` implementatie. Als het CPU-gebruik hoger is dan 50%, verhoogt Hallo autoscaler hier Hallo gehele product tooa maximaal 10.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

status van de toosee Hallo van Hallo autoscaler, Hallo volgende opdracht uitvoeren:

```azurecli-interactive
kubectl get hpa
```

Uitvoer:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Na een paar minuten, met een minimale belasting op Hallo Azure stem app, verlaagt Hallo aantal replica's schil automatisch too3.

## <a name="scale-hello-agents"></a>Schaal Hallo agents

Als u uw Kubernetes-cluster met standaardopdrachten in de vorige Hallo-zelfstudie hebt gemaakt, heeft deze drie knooppunten van de agent. Als u van plan meer of minder container werkbelastingen uw cluster bent, kunt u het aantal agents Hallo handmatig aanpassen. Gebruik Hallo [az acs schalen](/cli/azure/acs#scale) opdracht en geeft u het aantal agents Hallo Hello `--new-agent-count` parameter.

Hallo volgende voorbeeld worden verhoogd Hallo agent knooppunten too4 in Hallo Kubernetes cluster met de naam aantal *myK8sCluster*. Hallo opdracht duurt enkele minuten toocomplete.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Hallo opdrachtuitvoer toont Hallo aantal agent knooppunten in Hallo-waarde van `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie kunt u verschillende functies die schalen in uw cluster Kubernetes gebruikt. Taken aan de orde opgenomen:

> [!div class="checklist"]
> * Handmatig schalen Kubernetes gehele product
> * Configureren voor automatisch schalen gehele product Hallo app-front-end uitgevoerd
> * Hallo Kubernetes Azure-agent knooppunten schalen

Toohello volgende zelfstudie toolearn over het bijwerken van de toepassing in Kubernetes gaan.

> [!div class="nextstepaction"]
> [Bijwerken van een toepassing in Kubernetes](./container-service-tutorial-kubernetes-app-update.md)

