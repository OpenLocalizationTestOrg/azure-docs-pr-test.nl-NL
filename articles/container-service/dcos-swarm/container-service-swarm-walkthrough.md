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
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="c33cd-103">Docker Swarm-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="c33cd-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="c33cd-104">Een Docker Swarm-cluster wordt geïmplementeerd met behulp van hello Azure CLI in deze snel starten.</span><span class="sxs-lookup"><span data-stu-id="c33cd-104">In this quick start, a Docker Swarm cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="c33cd-105">Een container voor meerdere-toepassing die bestaan uit een webfront-end en een Redis-exemplaar wordt vervolgens geïmplementeerd en uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c33cd-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="c33cd-106">Zodra de voltooid, Hallo-toepassing is toegankelijk via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c33cd-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="c33cd-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="c33cd-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="c33cd-108">Deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="c33cd-108">This quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c33cd-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="c33cd-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c33cd-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c33cd-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="c33cd-111">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="c33cd-111">Create a resource group</span></span>

<span data-ttu-id="c33cd-112">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c33cd-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c33cd-113">Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="c33cd-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="c33cd-114">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westus* locatie.</span><span class="sxs-lookup"><span data-stu-id="c33cd-114">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c33cd-115">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c33cd-115">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="c33cd-116">Docker Swarm-cluster maken</span><span class="sxs-lookup"><span data-stu-id="c33cd-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="c33cd-117">Maak een Docker Swarm-cluster in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c33cd-117">Create a Docker Swarm cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="c33cd-118">Hallo volgende voorbeeld wordt een cluster met de naam *mySwarmCluster* hoofdsleutel met een Linux-knooppunt en drie knooppunten voor Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="c33cd-118">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="c33cd-119">Na enkele minuten Hallo-opdracht is voltooid en retourneert informatie over de json-indeling over Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c33cd-119">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="c33cd-120">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="c33cd-120">Connect toohello cluster</span></span>

<span data-ttu-id="c33cd-121">In deze snel starten moet u Hallo IP-adres van zowel Hallo Docker Swarm hoofd- en Hallo Docker-agent van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c33cd-121">Throughout this quick start, you need hello IP address of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="c33cd-122">Voer Hallo volgende opdracht tooreturn beide IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="c33cd-122">Run hello following command tooreturn both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="c33cd-123">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c33cd-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="c33cd-124">Maak een SSH-tunnel toohello Swarm model.</span><span class="sxs-lookup"><span data-stu-id="c33cd-124">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="c33cd-125">Vervang `IPAddress` met Hallo IP-adres van Hallo Swarm-master.</span><span class="sxs-lookup"><span data-stu-id="c33cd-125">Replace `IPAddress` with hello IP address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="c33cd-126">Set Hallo `DOCKER_HOST` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="c33cd-126">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="c33cd-127">Hiermee kunt u toorun docker opdrachten tegen Hallo Docker Swarm zonder toospecify Hallo-naam van Hallo host.</span><span class="sxs-lookup"><span data-stu-id="c33cd-127">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="c33cd-128">U bent nu klaar toorun Docker-services op Hallo Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c33cd-128">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="c33cd-129">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c33cd-129">Run hello application</span></span>

<span data-ttu-id="c33cd-130">Maak een bestand met de naam `docker-compose.yaml` en kopiëren Hallo inhoud in de App.</span><span class="sxs-lookup"><span data-stu-id="c33cd-130">Create a file named `docker-compose.yaml` and copy hello following content into it.</span></span>

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

<span data-ttu-id="c33cd-131">Hallo na de opdracht toocreate hello Azure stem service worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c33cd-131">Run hello following command toocreate hello Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="c33cd-132">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c33cd-132">Output:</span></span>

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

## <a name="test-hello-application"></a><span data-ttu-id="c33cd-133">Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="c33cd-133">Test hello application</span></span>

<span data-ttu-id="c33cd-134">Blader toohello IP-adres van Hallo Swarm-agent groep tootest uit hello Azure stem toepassing.</span><span class="sxs-lookup"><span data-stu-id="c33cd-134">Browse toohello IP address of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Afbeelding van tooAzure stem bladeren](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="c33cd-136">Cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="c33cd-136">Delete cluster</span></span>
<span data-ttu-id="c33cd-137">Wanneer Hallo cluster niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, containerservice en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="c33cd-137">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="c33cd-138">Hallo code ophalen</span><span class="sxs-lookup"><span data-stu-id="c33cd-138">Get hello code</span></span>

<span data-ttu-id="c33cd-139">In deze snel starten is de vooraf gemaakte container installatiekopieën gebruikte toocreate een Docker-service.</span><span class="sxs-lookup"><span data-stu-id="c33cd-139">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="c33cd-140">Hallo gerelateerd toepassingscode, Dockerfile, en opstellen-bestand zijn beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="c33cd-140">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="c33cd-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="c33cd-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="c33cd-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c33cd-142">Next steps</span></span>

<span data-ttu-id="c33cd-143">In deze snel starten een Docker Swarm-cluster wordt geïmplementeerd en een toepassing met meerdere container tooit geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c33cd-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="c33cd-144">toolearn over de integratie van Docker warme met Visual Studio Team Services, blijven toohello CI/CD met Docker Swarm en VSTS.</span><span class="sxs-lookup"><span data-stu-id="c33cd-144">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c33cd-145">CI/CD met Docker Swarm en VSTS</span><span class="sxs-lookup"><span data-stu-id="c33cd-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)