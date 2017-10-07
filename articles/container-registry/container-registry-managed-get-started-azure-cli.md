---
title: aaaCreate persoonlijke Docker-container register - Azure CLI | Microsoft Docs
description: Aan de slag maken en beheren van persoonlijke Docker-container registers Hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="4b646-103">Maken van een beheerde container register hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="4b646-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="4b646-104">Azure Container Registry is een beheerde service voor Docker-containerregisters die wordt gebruikt voor het opslaan van installatiekopieën van persoonlijke Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="4b646-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="4b646-105">Deze handleiding-gegevens voor het maken van een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4b646-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="4b646-106">Beheerde Azure-containerregisters zijn nog in preview en zijn niet in alle regio's beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4b646-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4b646-107">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="4b646-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4b646-108">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="4b646-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4b646-109">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4b646-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="4b646-110">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="4b646-110">Create a resource group</span></span>

<span data-ttu-id="4b646-111">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b646-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4b646-112">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="4b646-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="4b646-113">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westcentralus* locatie.</span><span class="sxs-lookup"><span data-stu-id="4b646-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="4b646-114">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="4b646-114">Create a container registry</span></span>

<span data-ttu-id="4b646-115">ACR-exemplaar met behulp van Hallo maken [az acr maken](/cli/azure/acr#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b646-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="4b646-116">Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="4b646-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="4b646-117">naam van de Hallo register in Hallo voorbeeld is *myContainerRegistry1*, vervangen door een unieke naam van uw eigen.</span><span class="sxs-lookup"><span data-stu-id="4b646-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="4b646-118">Bij Hallo register wordt gemaakt, is het Hallo-uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="4b646-118">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="4b646-119">Meld u bij tooACR exemplaar</span><span class="sxs-lookup"><span data-stu-id="4b646-119">Log in tooACR instance</span></span>

<span data-ttu-id="4b646-120">Voordat u pushen en installatiekopieën van de container binnenhalen, moet u zich aanmeldt toohello ACR-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="4b646-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="4b646-121">dus gebruiken Hallo toodo [az acr aanmelding](/cli/azure/acr#login) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b646-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="4b646-122">Hallo opdracht retourneert een bericht 'Aanmelding geslaagd' eenmaal is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4b646-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="4b646-123">Azure Container Registry gebruiken</span><span class="sxs-lookup"><span data-stu-id="4b646-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="4b646-124">Containerinstallatiekopieën opvragen</span><span class="sxs-lookup"><span data-stu-id="4b646-124">List container images</span></span>

<span data-ttu-id="4b646-125">Gebruik Hallo `az acr` CLI-opdrachten tooquery Hallo installatiekopieën en labels in een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4b646-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="4b646-126">Container register biedt momenteel geen ondersteuning voor Hallo `docker search` opdracht tooquery voor afbeeldingen en labels.</span><span class="sxs-lookup"><span data-stu-id="4b646-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="4b646-127">Opslagplaatsen weergeven</span><span class="sxs-lookup"><span data-stu-id="4b646-127">List repositories</span></span>

<span data-ttu-id="4b646-128">Hallo volgende voorbeeld worden Hallo-opslagplaatsen in een register, in JSON (JavaScript Object Notation)-indeling:</span><span class="sxs-lookup"><span data-stu-id="4b646-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="4b646-129">Tags weergeven</span><span class="sxs-lookup"><span data-stu-id="4b646-129">List tags</span></span>

<span data-ttu-id="4b646-130">Hallo volgende voorbeeld wordt een lijst Hallo labels op Hallo **samples/nginx** -opslagplaats, in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="4b646-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="4b646-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b646-131">Next steps</span></span>

<span data-ttu-id="4b646-132">In deze snel starten, kunt u een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure CLI hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4b646-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b646-133">Uw eerste installatiekopie met behulp van Docker CLI Hallo push</span><span class="sxs-lookup"><span data-stu-id="4b646-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
