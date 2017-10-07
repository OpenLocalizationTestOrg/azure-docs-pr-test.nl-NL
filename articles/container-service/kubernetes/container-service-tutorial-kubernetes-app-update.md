---
title: zelfstudie voor aaaAzure Container Service - Update-toepassing | Microsoft Docs
description: Zelfstudie voor Azure Container Service - Update-toepassing
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Bijwerken van een toepassing in Kubernetes

Nadat u een toepassing in Kubernetes hebt geïmplementeerd, kan deze worden bijgewerkt door te geven van een nieuwe container afbeeldings- of image versie. Wanneer u een toepassing bijwerkt, update-implementatie Hallo tijdelijk worden opgeslagen zodat alleen een deel van Hallo implementatie gelijktijdig worden bijgewerkt. Deze update gefaseerde kan Hallo toepassing tookeep uitgevoerd tijdens het bijwerken van Hallo en biedt een terugdraaimechanisme als een implementatie-fout optreedt. 

In deze zelfstudie maakt wordt deel uit zes van zeven, hello Azure stem voorbeeldapp bijgewerkt. Taken die u uitvoert, zijn onder andere:

> [!div class="checklist"]
> * Hallo-front-toepassingscode bijwerken
> * Maken van een installatiekopie van een bijgewerkte container
> * Hallo container installatiekopie tooAzure Container register pushen
> * Hallo bijgewerkte container installatiekopie implementeren

In volgende zelfstudies is Operations Management Suite geconfigureerde toomonitor hello Kubernetes cluster.

## <a name="before-you-begin"></a>Voordat u begint

In vorige zelfstudies, een toepassing is ingepakt in een installatiekopie van een container, Hallo afbeelding geüpload tooAzure register van de Container en een Kubernetes-cluster dat is gemaakt. Hallo toepassing is klikt u vervolgens op Hallo Kubernetes cluster uitgevoerd. 

Als u deze stappen niet zijn voltooid en toofollow langs wilt, te retourneren[zelfstudie 1 – installatiekopieën van de container maken](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Toepassing bijwerken

toocomplete hello stappen in deze zelfstudie, u moet hebt gekloond een kopie van hello Azure stem toepassing. Indien nodig, maakt u deze gekloonde kopie met Hallo volgende opdracht:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Open Hallo `config_file.cfg` bestand met een code- of teksteditor. U vindt dit bestand onder Hallo-map van Hallo gekloond opslagplaats te volgen.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Hallo-waarden voor `VOTE1VALUE` en `VOTE2VALUE`, en sla Hallo-bestand.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Gebruik [docker compose](https://docs.docker.com/compose/) toore-Hallo front-installatiekopie en Voer Hallo bijgewerkt toepassing maken.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Toepassing lokaal testen

Te bladeren`http://localhost:8080` toosee Hallo toepassing bijgewerkt.

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Installatiekopieën van het label en pushmeldingen

Tag Hallo *azure stem voorgrond* installatiekopie met de Hallo loginServer van Hallo container register.

Als u Azure Container register, de naam van de aanmelding Hallo Hello ophalen [az acr lijst](/cli/azure/acr#list) opdracht.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Gebruik [docker-tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag Hallo installatiekopie. Vervang `<acrLoginServer>` met uw Azure-Container register server aanmeldingsnaam of openbare register hostnaam.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Gebruik [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload Hallo installatiekopie tooyour register. Vervang `<acrLoginServer>` met uw Azure-Container register server aanmeldingsnaam of openbare register hostnaam.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Updatetoepassing implementeren

maximale uptime tooensure, meerdere exemplaren van Hallo toepassing schil moeten worden uitgevoerd. Controleer de configuratie met Hallo [kubectl ophalen schil](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht.

```bash
kubectl get pod
```

Uitvoer:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Als u geen meerdere gehele product met hello azure-stem-front-installatiekopie, schalen Hallo *azure stem voorgrond* implementatie.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

Gebruik Hallo-toepassing hello tooupdate [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) opdracht. Update `<acrLoginServer>` met Hallo server- of host aanmeldingsnaam van het register van de container.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

Gebruik Hallo-implementatie Hallo toomonitor [kubectl ophalen schil](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) opdracht. Als de toepassing hello bijgewerkt is geïmplementeerd, worden uw gehele product is beëindigd en opnieuw gemaakt met de nieuwe container installatiekopie Hallo.

```azurecli-interactive
kubectl get pod
```

Uitvoer:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Bijgewerkte toepassing testen

Het externe IP-adres Hallo Hallo *azure stem voorgrond* service.

```azurecli-interactive
kubectl get service azure-vote-front
```

Bladeren toohello IP-adres toosee Hallo toepassing bijgewerkt.

![Afbeelding van Kubernetes-cluster in Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie die u kunt een toepassing bijgewerkt en deze update tooa Kubernetes cluster uitgerold. Hallo na taken zijn voltooid:

> [!div class="checklist"]
> * Bijgewerkte Hallo front-code
> * Een installatiekopie van een bijgewerkte container gemaakt
> * Hallo container installatiekopie tooAzure Container register gepusht
> * Toepassing van de geïmplementeerde Hallo bijgewerkt

Toohello volgende zelfstudie toolearn over het vooraf toomonitor Kubernetes bij Operations Management Suite.

> [!div class="nextstepaction"]
> [Kubernetes bewaken met OMS](./container-service-tutorial-kubernetes-monitor.md)