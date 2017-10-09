---
title: zelfstudie voor aaaAzure Container Service - toepassing implementeren | Microsoft Docs
description: Zelfstudie voor Azure Container Service - toepassing implementeren
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Toepassingen uitvoeren in Kubernetes

In deze zelfstudie maakt deel uit van vier van zeven, een voorbeeld van een toepassing wordt geïmplementeerd in een cluster met Kubernetes. Stappen voltooid omvatten:

> [!div class="checklist"]
> * Kubernetes manifest-bestanden downloaden
> * Toepassing uitvoert in Kubernetes
> * Hallo toepassing testen

In volgende zelfstudies deze toepassing is uitgebreid, bijgewerkt, en Operations Management Suite toomonitor hello Kubernetes cluster geconfigureerd.

Deze zelfstudie wordt ervan uitgegaan dat een basiskennis van Kubernetes concepten, Zie voor gedetailleerde informatie over Kubernetes hello [Kubernetes documentatie](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Voordat u begint

In vorige zelfstudies een toepassing in een installatiekopie van een container is verpakt, deze installatiekopie is geüploade tooAzure register van de Container en een Kubernetes-cluster is gemaakt. Als u deze stappen nog niet hebt gedaan en u toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md). 

Deze zelfstudie vereist ten minste een Kubernetes-cluster.

## <a name="get-manifest-file"></a>Manifestbestand ophalen

Voor deze zelfstudie [Kubernetes objecten](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) zijn geïmplementeerd met een Kubernetes manifest. Een manifest Kubernetes is een YAML of JSON opgemaakte met Kubernetes object implementatie en configuratie-instructies.

Hallo toepassing manifestbestand voor deze zelfstudie is beschikbaar in hello Azure stem toepassing opslagplaats, die in een vorige zelfstudie is gekloond. Als u dit nog niet hebt gedaan, klonen Hallo opslagplaats Hello volgende opdracht: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Hallo-manifestbestand is gevonden in het Hallo-map van Hallo gekloond opslagplaats te volgen.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Manifestbestand bijwerken

Als Azure-Container register toostore Hallo container installatiekopieën gebruikt, Hallo manifest behoeften toobe bijgewerkt met Hallo ACR loginServer-naam.

Hallo ACR server aanmeldingsnaam Hello ophalen [az acr lijst](/cli/azure/acr#list) opdracht.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Hallo voorbeeld manifest is vooraf gemaakt met de naam van een opslagplaats van *microsoft*. Hallo-bestand openen met een teksteditor en vervang Hallo *microsoft* waarde met de naam van de aanmelding Hallo van uw ACR-exemplaar.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Toepassing implementeren

Gebruik Hallo [kubectl maken](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) opdracht toorun Hallo-toepassing. Deze opdracht parseert Hallo manifestbestand en Hallo gedefinieerd Kubernetes objecten maken.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

Uitvoer:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Toepassing testen

Een [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) wordt gemaakt die beschrijft Hallo toepassing toohello internet. Dit proces kan enkele minuten duren. 

toomonitor gemaakt, maar gebruik Hallo [kubectl ophalen service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) opdracht Hello `--watch` argument.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

In eerste instantie Hallo **extern IP-** voor Hallo *azure stem voorgrond* service wordt weergegeven als *in behandeling*. Nadat u Hallo extern IP-adres is gewijzigd van *in behandeling* tooan *IP-adres*, gebruik `CTRL-C` toostop hello kubectl controle proces.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

toosee hello toepassing bladeren toohello externe IP-adres.

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie is hello Azure stem toepassing geïmplementeerde tooan Kubernetes van Azure Container Service-cluster. Taken zijn voltooid, zijn onder andere:  

> [!div class="checklist"]
> * Kubernetes manifest-bestanden downloaden
> * Hallo-toepassing uitvoeren in Kubernetes
> * Geteste Hallo-toepassing

Toohello volgende zelfstudie toolearn over het schalen van een Kubernetes toepassing en de onderliggende infrastructuur Kubernetes Hallo gaan. 

> [!div class="nextstepaction"]
> [Schaal Kubernetes toepassingen en infrastructuur](./container-service-tutorial-kubernetes-scale.md)