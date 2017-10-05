---
title: "Privé-Docker-register maken - Azure Portal | Microsoft Docs"
description: "Aan de slag met het maken en beheren van privé-Docker-containerregisters met Azure Portal"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 560aee42b0c5a61c37c594d7937f833ab7183d49
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-portal"></a><span data-ttu-id="b6634-103">Een beheerd containerregister maken met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b6634-103">Create a managed container registry using the Azure portal</span></span>

<span data-ttu-id="b6634-104">Azure Container Registry is een beheerde service voor Docker-containerregisters die wordt gebruikt voor het opslaan van installatiekopieën van persoonlijke Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="b6634-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="b6634-105">In deze handleiding vindt u instructies voor het maken van een beheerd exemplaar van Azure Container Registry via Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b6634-105">This guide details creating a managed Azure Container Registry instance using the Azure portal.</span></span>

<span data-ttu-id="b6634-106">Beheerde Azure-containerregisters zijn nog in preview en zijn niet in alle regio's beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b6634-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="b6634-107">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="b6634-107">Log in to Azure</span></span>

<span data-ttu-id="b6634-108">Meld u via http://portal.azure.com aan bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b6634-108">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="b6634-109">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="b6634-109">Create a container registry</span></span>

1. <span data-ttu-id="b6634-110">Klik op de knop **Nieuw** in de linkerbovenhoek van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b6634-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="b6634-111">Zoek in Marketplace naar **Azure Container Registry** en selecteer het product.</span><span class="sxs-lookup"><span data-stu-id="b6634-111">Search the marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="b6634-112">Klik op **Maken** om de blade ACR maken te openen.</span><span class="sxs-lookup"><span data-stu-id="b6634-112">Click **Create** which will open the ACR creation blade.</span></span>

    ![Container Registry-instellingen](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="b6634-114">Voer de volgende gegevens in op de blade **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="b6634-114">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="b6634-115">Klik op **Maken** wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="b6634-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="b6634-116">a.</span><span class="sxs-lookup"><span data-stu-id="b6634-116">a.</span></span> <span data-ttu-id="b6634-117">**Registernaam**: een unieke domeinnaam op het hoogste niveau voor uw specifieke register.</span><span class="sxs-lookup"><span data-stu-id="b6634-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="b6634-118">De registernaam in dit voorbeeld is *myAzureContainerRegistry1*, maar u moet deze naam vervangen door een eigen unieke naam.</span><span class="sxs-lookup"><span data-stu-id="b6634-118">In this example, the registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="b6634-119">De naam mag alleen uit letters en cijfers bestaan.</span><span class="sxs-lookup"><span data-stu-id="b6634-119">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="b6634-120">b.</span><span class="sxs-lookup"><span data-stu-id="b6634-120">b.</span></span> <span data-ttu-id="b6634-121">**Resourcegroep**: selecteer een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) of typ de gewenste naam voor een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b6634-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="b6634-122">c.</span><span class="sxs-lookup"><span data-stu-id="b6634-122">c.</span></span> <span data-ttu-id="b6634-123">**Locatie**: selecteer een Azure Datacenter-locatie waar de service [beschikbaar](https://azure.microsoft.com/regions/services/) is, zoals **Zuid-centraal VS**.</span><span class="sxs-lookup"><span data-stu-id="b6634-123">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="b6634-124">d.</span><span class="sxs-lookup"><span data-stu-id="b6634-124">d.</span></span> <span data-ttu-id="b6634-125">**Beheerder**: schakel eventueel toegang tot het register in voor een beheerder.</span><span class="sxs-lookup"><span data-stu-id="b6634-125">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="b6634-126">U kunt deze instelling wijzigen nadat u het register hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b6634-126">You can change this setting after creating the registry.</span></span>

    <span data-ttu-id="b6634-127">e.</span><span class="sxs-lookup"><span data-stu-id="b6634-127">e.</span></span> <span data-ttu-id="b6634-128">**Beheerd register gebruiken**: selecteer Ja als ACR automatisch de registeropslag moet beheren, webhooks moet gebruiken en AAD-verificatie moet toepassen.</span><span class="sxs-lookup"><span data-stu-id="b6634-128">**Use managed registry**: Select yes to have ACR automatically manage the registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="b6634-129">f.</span><span class="sxs-lookup"><span data-stu-id="b6634-129">f.</span></span> <span data-ttu-id="b6634-130">**Prijscategorie**: selecteer een prijscategorie, zie ACR-prijzen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b6634-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="b6634-131">Aanmelden bij ACR-exemplaar</span><span class="sxs-lookup"><span data-stu-id="b6634-131">Log in to ACR instance</span></span>

<span data-ttu-id="b6634-132">Voordat u installatiekopieën van containers gaat pushen en pullen, moet u zich aanmelden bij het ACR-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b6634-132">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> 

<span data-ttu-id="b6634-133">Gebruik hiervoor de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b6634-133">To do so, use the Azure CLI 2.0.</span></span> <span data-ttu-id="b6634-134">Meld u indien nodig eerst aan bij Azure, met behulp van de opdracht [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b6634-134">First, if needed, log into Azure using the [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="b6634-135">Gebruik vervolgens de opdracht [az acr login](/cli/azure/acr#login) om u aan te melden bij Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="b6634-135">Next, use the [az acr login](/cli/azure/acr#login) command to log in to the Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="b6634-136">Azure Container Registry gebruiken</span><span class="sxs-lookup"><span data-stu-id="b6634-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="b6634-137">Containerinstallatiekopieën opvragen</span><span class="sxs-lookup"><span data-stu-id="b6634-137">List container images</span></span>

<span data-ttu-id="b6634-138">Gebruik de `az acr`-CLI-opdrachten om query's toe te passen op de installatiekopieën en tags in een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b6634-138">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b6634-139">Container Registry ondersteunt momenteel de opdracht `docker search` niet voor het toepassen van query's op installatiekopieën en tags.</span><span class="sxs-lookup"><span data-stu-id="b6634-139">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="b6634-140">Opslagplaatsen weergeven</span><span class="sxs-lookup"><span data-stu-id="b6634-140">List repositories</span></span>

<span data-ttu-id="b6634-141">In het volgende voorbeeld worden de opslagplaatsen in een register weergegeven in JSON-indeling (JavaScript Object Notation):</span><span class="sxs-lookup"><span data-stu-id="b6634-141">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="b6634-142">Tags weergeven</span><span class="sxs-lookup"><span data-stu-id="b6634-142">List tags</span></span>

<span data-ttu-id="b6634-143">In het volgende voorbeeld worden de tags in de opslagplaats **samples/nginx** weergegeven in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="b6634-143">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="b6634-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b6634-144">Next steps</span></span>

<span data-ttu-id="b6634-145">In deze snelstartgids hebt u een beheerd exemplaar van Azure Container Registry gemaakt met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b6634-145">In this quick start, you've created a managed Azure Container Registry instance using the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6634-146">Uw eerste installatiekopie pushen met de Docker-CLI</span><span class="sxs-lookup"><span data-stu-id="b6634-146">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)