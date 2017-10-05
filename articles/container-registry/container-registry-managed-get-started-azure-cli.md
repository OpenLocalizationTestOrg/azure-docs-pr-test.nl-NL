---
title: "Privé-Docker-containerregister maken - Azure CLI | Microsoft Docs"
description: "Aan de slag met het maken en beheren van privé-Docker-containerregisters met Azure CLI 2.0"
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
ms.openlocfilehash: c7cdb1b13bf32388d18c2a25af28337a81861c1e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-cli"></a><span data-ttu-id="a6d9e-103">Een beheerd containerregister maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a6d9e-103">Create a managed container registry using the Azure CLI</span></span>

<span data-ttu-id="a6d9e-104">Azure Container Registry is een beheerde service voor Docker-containerregisters die wordt gebruikt voor het opslaan van installatiekopieën van persoonlijke Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="a6d9e-105">In deze handleiding vindt u instructies voor het maken van een beheerd exemplaar van Azure Container Registry met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-105">This guide details creating a managed Azure Container Registry instance using the Azure CLI.</span></span>

<span data-ttu-id="a6d9e-106">Beheerde Azure-containerregisters zijn nog in preview en zijn niet in alle regio's beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a6d9e-107">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor deze Quickstart gebruikmaken van Azure CLI versie 2.0.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a6d9e-108">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="a6d9e-109">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a6d9e-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="a6d9e-110">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="a6d9e-110">Create a resource group</span></span>

<span data-ttu-id="a6d9e-111">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a6d9e-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a6d9e-112">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="a6d9e-113">In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *westcentralus*.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-113">The following example creates a resource group named *myResourceGroup* in the *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="a6d9e-114">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="a6d9e-114">Create a container registry</span></span>

<span data-ttu-id="a6d9e-115">Maak een ACR-exemplaar met de opdracht [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="a6d9e-115">Create an ACR instance using the [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="a6d9e-116">Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="a6d9e-117">De registernaam in de voorbeelden is *myContainerRegistry1*, maar u moet deze vervangen door uw eigen unieke naam.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-117">The registry name in the example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="a6d9e-118">Wanneer het register is gemaakt, is de uitvoer vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="a6d9e-118">When the registry is created, the output is similar to the following:</span></span>

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

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="a6d9e-119">Aanmelden bij ACR-exemplaar</span><span class="sxs-lookup"><span data-stu-id="a6d9e-119">Log in to ACR instance</span></span>

<span data-ttu-id="a6d9e-120">Voordat u installatiekopieën van containers gaat pushen en pullen, moet u zich aanmelden bij het ACR-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-120">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="a6d9e-121">Gebruik hiervoor de opdracht [az acr login](/cli/azure/acr#login).</span><span class="sxs-lookup"><span data-stu-id="a6d9e-121">To do so, use the [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="a6d9e-122">De opdracht retourneert een bericht dat de aanmelding is gelukt.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-122">The command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="a6d9e-123">Azure Container Registry gebruiken</span><span class="sxs-lookup"><span data-stu-id="a6d9e-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="a6d9e-124">Containerinstallatiekopieën opvragen</span><span class="sxs-lookup"><span data-stu-id="a6d9e-124">List container images</span></span>

<span data-ttu-id="a6d9e-125">Gebruik de `az acr`-CLI-opdrachten om query's toe te passen op de installatiekopieën en tags in een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-125">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a6d9e-126">Container Registry ondersteunt momenteel de opdracht `docker search` niet voor het toepassen van query's op installatiekopieën en tags.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-126">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="a6d9e-127">Opslagplaatsen weergeven</span><span class="sxs-lookup"><span data-stu-id="a6d9e-127">List repositories</span></span>

<span data-ttu-id="a6d9e-128">In het volgende voorbeeld worden de opslagplaatsen in een register weergegeven in JSON-indeling (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="a6d9e-128">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="a6d9e-129">Tags weergeven</span><span class="sxs-lookup"><span data-stu-id="a6d9e-129">List tags</span></span>

<span data-ttu-id="a6d9e-130">In het volgende voorbeeld worden de tags in de opslagplaats **samples/nginx** weergegeven in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="a6d9e-130">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="a6d9e-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6d9e-131">Next steps</span></span>

<span data-ttu-id="a6d9e-132">In deze snelstartgids hebt u een beheerd exemplaar van Azure Container Registry gemaakt met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6d9e-132">In this quick start, you've created a managed Azure Container Registry instance using the Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a6d9e-133">Uw eerste installatiekopie pushen met de Docker-CLI</span><span class="sxs-lookup"><span data-stu-id="a6d9e-133">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
