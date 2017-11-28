---
title: een cluster met Docker-container - Azure CLI aaaDeploy | Microsoft Docs
description: Een Kubernetes-, DC/OS-, of Docker Swarm-oplossing implementeren in Azure Container Service met behulp van de Azure CLI 2.0
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a><span data-ttu-id="2b02a-103">Een oplossing met behulp van Azure CLI 2.0 Hallo hosting Docker-container implementeren</span><span class="sxs-lookup"><span data-stu-id="2b02a-103">Deploy a Docker container hosting solution using hello Azure CLI 2.0</span></span>

<span data-ttu-id="2b02a-104">Gebruik Hallo `az acs` opdrachten in hello Azure CLI 2.0 toocreate en beheren van clusters in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="2b02a-104">Use hello `az acs` commands in hello Azure CLI 2.0 toocreate and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="2b02a-105">U kunt ook een Azure Container Service-cluster implementeren met behulp van Hallo [Azure-portal](container-service-deployment.md) of hello Azure Container Service API's.</span><span class="sxs-lookup"><span data-stu-id="2b02a-105">You can also deploy an Azure Container Service cluster by using hello [Azure portal](container-service-deployment.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="2b02a-106">Voor meer informatie over `az acs` opdrachten, doorgeven Hallo `-h` parameter tooany opdracht.</span><span class="sxs-lookup"><span data-stu-id="2b02a-106">For help on `az acs` commands, pass hello `-h` parameter tooany command.</span></span> <span data-ttu-id="2b02a-107">Bijvoorbeeld: `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="2b02a-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="2b02a-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2b02a-108">Prerequisites</span></span>
<span data-ttu-id="2b02a-109">een Azure Container Service-cluster gebruikt toocreate hello Azure CLI 2.0, moet:</span><span class="sxs-lookup"><span data-stu-id="2b02a-109">toocreate an Azure Container Service cluster using hello Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="2b02a-110">beschikken over een Azure-account ([krijg een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="2b02a-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="2b02a-111">hebt geïnstalleerd en geconfigureerd Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="2b02a-111">have installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="2b02a-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="2b02a-112">Get started</span></span> 
### <a name="log-in-tooyour-account"></a><span data-ttu-id="2b02a-113">Meld u bij tooyour account</span><span class="sxs-lookup"><span data-stu-id="2b02a-113">Log in tooyour account</span></span>
```azurecli
az login 
```

<span data-ttu-id="2b02a-114">Volg interactief Hallo prompts toolog in.</span><span class="sxs-lookup"><span data-stu-id="2b02a-114">Follow hello prompts toolog in interactively.</span></span> <span data-ttu-id="2b02a-115">Zie voor andere methoden toolog in, [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="2b02a-115">For other methods toolog in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="2b02a-116">Uw Azure-abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="2b02a-116">Set your Azure subscription</span></span>

<span data-ttu-id="2b02a-117">Als u meer dan één Azure-abonnement hebt, stelt u Hallo standaardabonnement.</span><span class="sxs-lookup"><span data-stu-id="2b02a-117">If you have more than one Azure subscription, set hello default subscription.</span></span> <span data-ttu-id="2b02a-118">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2b02a-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="2b02a-119">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="2b02a-119">Create a resource group</span></span>
<span data-ttu-id="2b02a-120">Het wordt aangeraden om een resourcegroep te maken voor elk cluster.</span><span class="sxs-lookup"><span data-stu-id="2b02a-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="2b02a-121">Geef een Azure-regio op waarin Azure Container Service [beschikbaar](https://azure.microsoft.com/en-us/regions/services/) is.</span><span class="sxs-lookup"><span data-stu-id="2b02a-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="2b02a-122">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2b02a-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="2b02a-123">Uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="2b02a-123">Output is similar toohello following:</span></span>

![Een resourcegroep maken](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="2b02a-125">Een Azure Container Service-cluster maken</span><span class="sxs-lookup"><span data-stu-id="2b02a-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="2b02a-126">gebruik van een cluster toocreate `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="2b02a-126">toocreate a cluster, use `az acs create`.</span></span>
<span data-ttu-id="2b02a-127">Een naam voor Hallo cluster en het Hallo-naam van resourcegroep Hallo gemaakt in de vorige stap Hallo zijn verplichte parameters.</span><span class="sxs-lookup"><span data-stu-id="2b02a-127">A name for hello cluster and hello name of hello resource group created in hello previous step are mandatory parameters.</span></span> 

<span data-ttu-id="2b02a-128">Andere invoer zijn set toodefault waarden (Zie het volgende scherm Hallo) tenzij overschreven met behulp van hun respectieve switches.</span><span class="sxs-lookup"><span data-stu-id="2b02a-128">Other inputs are set toodefault values (see hello following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="2b02a-129">Bijvoorbeeld, is Hallo orchestrator ingesteld door Standaardbesturingssysteem tooDC.</span><span class="sxs-lookup"><span data-stu-id="2b02a-129">For example, hello orchestrator is set by default tooDC/OS.</span></span> <span data-ttu-id="2b02a-130">En als u niet opgeeft, een DNS-voorvoegsel is gemaakt op basis van de clusternaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b02a-130">And if you don't specify one, a DNS name prefix is created based on hello cluster name.</span></span>

![Azure ACS gebruiken en maken](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="2b02a-132">Snel `acs create` met standaardinstellingen</span><span class="sxs-lookup"><span data-stu-id="2b02a-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="2b02a-133">Als u een openbare SSH-RSA-sleutelbestand hebt `id_rsa.pub` op de standaardlocatie hello (of gemaakt voor [OS X- en Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) of [Windows](../../virtual-machines/linux/ssh-from-windows.md)), een opdracht zoals Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2b02a-133">If you have an SSH RSA public key file `id_rsa.pub` in hello default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like hello following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="2b02a-134">Als u geen openbare SSH-sleutel hebt, gebruikt u deze tweede opdracht.</span><span class="sxs-lookup"><span data-stu-id="2b02a-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="2b02a-135">Deze opdracht met Hallo `--generate-ssh-keys` switch maakt voor u.</span><span class="sxs-lookup"><span data-stu-id="2b02a-135">This command with hello `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="2b02a-136">Nadat u Hallo opdracht invoert, wacht u ongeveer 10 minuten voor Hallo cluster toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2b02a-136">After you enter hello command, wait for about 10 minutes for hello cluster toobe created.</span></span> <span data-ttu-id="2b02a-137">Hallo-opdrachtuitvoer bevat volledig gekwalificeerde domeinnamen (FQDN's) van Hallo master en agent knooppunten en een SSH-opdracht tooconnect toohello eerste model.</span><span class="sxs-lookup"><span data-stu-id="2b02a-137">hello command output includes fully qualified domain names (FQDNs) of hello master and agent nodes and an SSH command tooconnect toohello first master.</span></span> <span data-ttu-id="2b02a-138">Hier volgt de verkorte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2b02a-138">Here is abbreviated output:</span></span>

![Afbeelding van ACS maken](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="2b02a-140">Hallo [Kubernetes scenario](../kubernetes/container-service-kubernetes-walkthrough.md) ziet u hoe toouse `az acs create` met standaard waarden toocreate een Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="2b02a-140">hello [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how toouse `az acs create` with default values toocreate a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="2b02a-141">ACS-clusters beheren</span><span class="sxs-lookup"><span data-stu-id="2b02a-141">Manage ACS clusters</span></span>

<span data-ttu-id="2b02a-142">Gebruik aanvullende `az acs` opdrachten toomanage uw cluster.</span><span class="sxs-lookup"><span data-stu-id="2b02a-142">Use additional `az acs` commands toomanage your cluster.</span></span> <span data-ttu-id="2b02a-143">Hier volgen enkele voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="2b02a-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="2b02a-144">Clusters groeperen onder een abonnement</span><span class="sxs-lookup"><span data-stu-id="2b02a-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="2b02a-145">Clusters groeperen onder een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="2b02a-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![ACS-lijst](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="2b02a-147">Details van een Container Service-cluster weergeven</span><span class="sxs-lookup"><span data-stu-id="2b02a-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![ACS weergeven](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a><span data-ttu-id="2b02a-149">Schaal Hallo cluster</span><span class="sxs-lookup"><span data-stu-id="2b02a-149">Scale hello cluster</span></span>
<span data-ttu-id="2b02a-150">Zowel het opschalen als het uitschalen van agentknooppunten is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2b02a-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="2b02a-151">parameter Hallo `new-agent-count` Hallo nieuwe aantal agents in Hallo ACS-cluster is.</span><span class="sxs-lookup"><span data-stu-id="2b02a-151">hello parameter `new-agent-count` is hello new number of agents in hello ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![ACS-schaal](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="2b02a-153">Een Container Service-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="2b02a-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="2b02a-154">Met deze opdracht worden alle resources (netwerk en opslag) zijn gemaakt tijdens het maken van Hallo containerservice niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2b02a-154">This command does not delete all resources (network and storage) created while creating hello container service.</span></span> <span data-ttu-id="2b02a-155">toodelete alle resources gemakkelijk, verdient het implementeren van ieder cluster in een afzonderlijke resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2b02a-155">toodelete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="2b02a-156">Hallo resourcegroep vervolgens verwijderen wanneer het Hallo-cluster is niet langer vereist.</span><span class="sxs-lookup"><span data-stu-id="2b02a-156">Then, delete hello resource group when hello cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b02a-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b02a-157">Next steps</span></span>
<span data-ttu-id="2b02a-158">Nu u een werkend cluster hebt, kunt u deze documenten lezen voor meer informatie over verbinding en beheer:</span><span class="sxs-lookup"><span data-stu-id="2b02a-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="2b02a-159">Verbinding maken met tooan Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="2b02a-159">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="2b02a-160">Werken met de Azure Container Service en DC/OS</span><span class="sxs-lookup"><span data-stu-id="2b02a-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="2b02a-161">Werken met de Azure Container Service en Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="2b02a-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="2b02a-162">Werken met de Azure Container Service en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2b02a-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)