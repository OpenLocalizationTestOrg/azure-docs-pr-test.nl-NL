---
title: aaaQuickstart - Azure Docker Swarm-cluster voor Linux | Microsoft Docs
description: Snel meer toocreate een Docker Swarm-cluster voor Linux-containers in Azure Container Service met hello Azure CLI.
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a>Docker Swarm-cluster implementeren

Een Docker Swarm-cluster wordt geïmplementeerd met behulp van hello Azure CLI in deze snel starten. Een container voor meerdere-toepassing die bestaan uit een webfront-end en een Redis-exemplaar wordt vervolgens geïmplementeerd en uitgevoerd op Hallo-cluster. Zodra de voltooid, Hallo-toepassing is toegankelijk via internet Hallo.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

Deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd.

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Uitvoer:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Docker Swarm-cluster maken

Maak een Docker Swarm-cluster in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht. 

Hallo volgende voorbeeld wordt een cluster met de naam *mySwarmCluster* hoofdsleutel met een Linux-knooppunt en drie knooppunten voor Linux-agent.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

Na enkele minuten Hallo-opdracht is voltooid en retourneert informatie over de json-indeling over Hallo-cluster.

## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello

In deze snel starten moet u Hallo IP-adres van zowel Hallo Docker Swarm hoofd- en Hallo Docker-agent van toepassingen. Voer Hallo volgende opdracht tooreturn beide IP-adressen.


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

Uitvoer:

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

Maak een SSH-tunnel toohello Swarm model. Vervang `IPAddress` met Hallo IP-adres van Hallo Swarm-master.

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

Set Hallo `DOCKER_HOST` omgevingsvariabele. Hiermee kunt u toorun docker opdrachten tegen Hallo Docker Swarm zonder toospecify Hallo-naam van Hallo host.

```bash
export DOCKER_HOST=:2375
```

U bent nu klaar toorun Docker-services op Hallo Docker Swarm.


## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Maak een bestand met de naam `docker-compose.yaml` en kopiëren Hallo inhoud in de App.

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Hallo na de opdracht toocreate hello Azure stem service worden uitgevoerd.

```bash
docker-compose up -d
```

Uitvoer:

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a>Hallo toepassing testen

Blader toohello IP-adres van Hallo Swarm-agent groep tootest uit hello Azure stem toepassing.

![Afbeelding van tooAzure stem bladeren](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Cluster verwijderen
Wanneer Hallo cluster niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, containerservice en alle gerelateerde resources.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Hallo code ophalen

In deze snel starten is de vooraf gemaakte container installatiekopieën gebruikte toocreate een Docker-service. Hallo gerelateerd toepassingscode, Dockerfile, en opstellen-bestand zijn beschikbaar op GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Volgende stappen

In deze snel starten een Docker Swarm-cluster wordt geïmplementeerd en een toepassing met meerdere container tooit geïmplementeerd.

toolearn over de integratie van Docker warme met Visual Studio Team Services, blijven toohello CI/CD met Docker Swarm en VSTS.

> [!div class="nextstepaction"]
> [CI/CD met Docker Swarm en VSTS](./container-service-docker-swarm-setup-ci-cd.md)