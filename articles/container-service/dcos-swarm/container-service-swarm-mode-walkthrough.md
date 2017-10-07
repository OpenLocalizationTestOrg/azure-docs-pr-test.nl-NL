---
title: aaaQuickstart - cluster voor Linux Azure Docker CE | Microsoft Docs
description: Snel meer toocreate een Docker CE-cluster voor Linux-containers in Azure Container Service met hello Azure CLI.
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Docker CE-cluster implementeren

Een Docker CE-cluster wordt geïmplementeerd met behulp van hello Azure CLI in deze snel starten. Een container voor meerdere-toepassing die bestaan uit een webfront-end en een Redis-exemplaar wordt vervolgens geïmplementeerd en uitgevoerd op Hallo-cluster. Zodra de voltooid, Hallo-toepassing is toegankelijk via internet Hallo.

Docker CE in Azure Container Service is in de preview-fase. **Gebruik dit daarom niet voor productieworkloads**.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd.

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *ukwest* locatie.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
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

Een Docker CE-cluster maken in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht. 

Hallo volgende voorbeeld wordt een cluster met de naam *mySwarmCluster* hoofdsleutel met een Linux-knooppunt en drie knooppunten voor Linux-agent.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Na enkele minuten Hallo-opdracht is voltooid en retourneert informatie over de json-indeling over Hallo-cluster.

## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello

In deze snel starten moet u Hallo FQDN-naam van zowel Hallo Docker Swarm hoofd- en Hallo Docker-agent van toepassingen. Hallo na de opdracht tooreturn beide Hallo hoofd- en agent FQDN's worden uitgevoerd.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Uitvoer:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Maak een SSH-tunnel toohello Swarm model. Vervang `MasterFQDN` met Hallo FQDN-adres van Hallo Swarm-master.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Set Hallo `DOCKER_HOST` omgevingsvariabele. Hiermee kunt u toorun docker opdrachten tegen Hallo Docker Swarm zonder toospecify Hallo-naam van Hallo host.

```bash
export DOCKER_HOST=localhost:2374
```

U bent nu klaar toorun Docker-services op Hallo Docker Swarm.


## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Maak een bestand met de naam `azure-vote.yaml` en kopiëren Hallo inhoud in de App.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Voer Hallo [docker-stack implementeren](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate hello Azure stem service opdracht.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Uitvoer:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Gebruik Hallo [docker-stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) tooreturn Hallo implementatiestatus van de toepassing hello opdracht.

```bash
docker stack ps azure-vote
```

Eenmaal Hallo `CURRENT STATE` van elke service is `Running`, Hallo toepassing gereed is.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Hallo toepassing testen

Blader toohello FQDN-naam van Hallo Swarm-agent groep tootest uit hello Azure stem toepassing.

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