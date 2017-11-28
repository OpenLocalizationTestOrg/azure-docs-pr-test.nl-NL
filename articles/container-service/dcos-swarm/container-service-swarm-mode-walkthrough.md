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
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="75016-103">Docker CE-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="75016-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="75016-104">Een Docker CE-cluster wordt geïmplementeerd met behulp van hello Azure CLI in deze snel starten.</span><span class="sxs-lookup"><span data-stu-id="75016-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="75016-105">Een container voor meerdere-toepassing die bestaan uit een webfront-end en een Redis-exemplaar wordt vervolgens geïmplementeerd en uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="75016-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="75016-106">Zodra de voltooid, Hallo-toepassing is toegankelijk via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="75016-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="75016-107">Docker CE in Azure Container Service is in de preview-fase. **Gebruik dit daarom niet voor productieworkloads**.</span><span class="sxs-lookup"><span data-stu-id="75016-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="75016-108">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="75016-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="75016-109">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="75016-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="75016-110">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="75016-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="75016-111">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="75016-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="75016-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="75016-112">Create a resource group</span></span>

<span data-ttu-id="75016-113">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="75016-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="75016-114">Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="75016-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="75016-115">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *ukwest* locatie.</span><span class="sxs-lookup"><span data-stu-id="75016-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="75016-116">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="75016-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="75016-117">Docker Swarm-cluster maken</span><span class="sxs-lookup"><span data-stu-id="75016-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="75016-118">Een Docker CE-cluster maken in Azure Container Service met Hallo [az acs maken](/cli/azure/acs#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="75016-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="75016-119">Hallo volgende voorbeeld wordt een cluster met de naam *mySwarmCluster* hoofdsleutel met een Linux-knooppunt en drie knooppunten voor Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="75016-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="75016-120">Na enkele minuten Hallo-opdracht is voltooid en retourneert informatie over de json-indeling over Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="75016-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="75016-121">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="75016-121">Connect toohello cluster</span></span>

<span data-ttu-id="75016-122">In deze snel starten moet u Hallo FQDN-naam van zowel Hallo Docker Swarm hoofd- en Hallo Docker-agent van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="75016-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="75016-123">Hallo na de opdracht tooreturn beide Hallo hoofd- en agent FQDN's worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="75016-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="75016-124">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="75016-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="75016-125">Maak een SSH-tunnel toohello Swarm model.</span><span class="sxs-lookup"><span data-stu-id="75016-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="75016-126">Vervang `MasterFQDN` met Hallo FQDN-adres van Hallo Swarm-master.</span><span class="sxs-lookup"><span data-stu-id="75016-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="75016-127">Set Hallo `DOCKER_HOST` omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="75016-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="75016-128">Hiermee kunt u toorun docker opdrachten tegen Hallo Docker Swarm zonder toospecify Hallo-naam van Hallo host.</span><span class="sxs-lookup"><span data-stu-id="75016-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="75016-129">U bent nu klaar toorun Docker-services op Hallo Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="75016-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="75016-130">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="75016-130">Run hello application</span></span>

<span data-ttu-id="75016-131">Maak een bestand met de naam `azure-vote.yaml` en kopiëren Hallo inhoud in de App.</span><span class="sxs-lookup"><span data-stu-id="75016-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


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

<span data-ttu-id="75016-132">Voer Hallo [docker-stack implementeren](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate hello Azure stem service opdracht.</span><span class="sxs-lookup"><span data-stu-id="75016-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="75016-133">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="75016-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="75016-134">Gebruik Hallo [docker-stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) tooreturn Hallo implementatiestatus van de toepassing hello opdracht.</span><span class="sxs-lookup"><span data-stu-id="75016-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="75016-135">Eenmaal Hallo `CURRENT STATE` van elke service is `Running`, Hallo toepassing gereed is.</span><span class="sxs-lookup"><span data-stu-id="75016-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="75016-136">Hallo toepassing testen</span><span class="sxs-lookup"><span data-stu-id="75016-136">Test hello application</span></span>

<span data-ttu-id="75016-137">Blader toohello FQDN-naam van Hallo Swarm-agent groep tootest uit hello Azure stem toepassing.</span><span class="sxs-lookup"><span data-stu-id="75016-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Afbeelding van tooAzure stem bladeren](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="75016-139">Cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="75016-139">Delete cluster</span></span>
<span data-ttu-id="75016-140">Wanneer Hallo cluster niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, containerservice en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="75016-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="75016-141">Hallo code ophalen</span><span class="sxs-lookup"><span data-stu-id="75016-141">Get hello code</span></span>

<span data-ttu-id="75016-142">In deze snel starten is de vooraf gemaakte container installatiekopieën gebruikte toocreate een Docker-service.</span><span class="sxs-lookup"><span data-stu-id="75016-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="75016-143">Hallo gerelateerd toepassingscode, Dockerfile, en opstellen-bestand zijn beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="75016-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="75016-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="75016-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="75016-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="75016-145">Next steps</span></span>

<span data-ttu-id="75016-146">In deze snel starten een Docker Swarm-cluster wordt geïmplementeerd en een toepassing met meerdere container tooit geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="75016-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="75016-147">toolearn over de integratie van Docker warme met Visual Studio Team Services, blijven toohello CI/CD met Docker Swarm en VSTS.</span><span class="sxs-lookup"><span data-stu-id="75016-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75016-148">CI/CD met Docker Swarm en VSTS</span><span class="sxs-lookup"><span data-stu-id="75016-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)