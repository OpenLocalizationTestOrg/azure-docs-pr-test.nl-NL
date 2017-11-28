---
title: aaaCreate persoonlijke Docker-register - Azure-portal | Microsoft Docs
description: Maken en beheren van persoonlijke Docker-container registers Hello Azure-portal aan de slag
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
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="72e86-103">Maken van een beheerde container register met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="72e86-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="72e86-104">Azure Container Registry is een beheerde service voor Docker-containerregisters die wordt gebruikt voor het opslaan van installatiekopieën van persoonlijke Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="72e86-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="72e86-105">Deze handleiding-gegevens voor het maken van een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="72e86-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="72e86-106">Beheerde Azure-containerregisters zijn nog in preview en zijn niet in alle regio's beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="72e86-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="72e86-107">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="72e86-107">Log in tooAzure</span></span>

<span data-ttu-id="72e86-108">Toohello aanmelden met Azure-portal op http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="72e86-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="72e86-109">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="72e86-109">Create a container registry</span></span>

1. <span data-ttu-id="72e86-110">Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="72e86-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="72e86-111">Zoeken Hallo marketplace voor **Azure container register** en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="72e86-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="72e86-112">Klik op **maken** die blade Hallo ACR-maken wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="72e86-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Container Registry-instellingen](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="72e86-114">In Hallo **Azure Container register** blade Hallo volgende informatie invoeren.</span><span class="sxs-lookup"><span data-stu-id="72e86-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="72e86-115">Klik op **Maken** wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="72e86-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="72e86-116">a.</span><span class="sxs-lookup"><span data-stu-id="72e86-116">a.</span></span> <span data-ttu-id="72e86-117">**Registernaam**: een unieke domeinnaam op het hoogste niveau voor uw specifieke register.</span><span class="sxs-lookup"><span data-stu-id="72e86-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="72e86-118">In dit voorbeeld is de naam van Hallo register *myAzureContainerRegistry1*, maar vervangen door een unieke naam van uw eigen.</span><span class="sxs-lookup"><span data-stu-id="72e86-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="72e86-119">Hallo-naam mag alleen letters en cijfers zijn.</span><span class="sxs-lookup"><span data-stu-id="72e86-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="72e86-120">b.</span><span class="sxs-lookup"><span data-stu-id="72e86-120">b.</span></span> <span data-ttu-id="72e86-121">**Resourcegroep**: Selecteer een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="72e86-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="72e86-122">c.</span><span class="sxs-lookup"><span data-stu-id="72e86-122">c.</span></span> <span data-ttu-id="72e86-123">**Locatie**: Selecteer een Azure-datacenter locatie van Hallo service [beschikbaar](https://azure.microsoft.com/regions/services/), zoals **Zuid-centraal VS**.</span><span class="sxs-lookup"><span data-stu-id="72e86-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="72e86-124">d.</span><span class="sxs-lookup"><span data-stu-id="72e86-124">d.</span></span> <span data-ttu-id="72e86-125">**Gebruiker met beheerdersrechten**: als u wilt, schakelt u het register voor een beheerder de gebruiker tooaccess Hallo.</span><span class="sxs-lookup"><span data-stu-id="72e86-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="72e86-126">U kunt deze instelling na het maken van Hallo register kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="72e86-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="72e86-127">e.</span><span class="sxs-lookup"><span data-stu-id="72e86-127">e.</span></span> <span data-ttu-id="72e86-128">**Gebruik beheerde register**: Selecteer Ja toohave ACR automatisch Hallo register opslag te beheren, gebruik webhooks en gebruik AAD-verificaties.</span><span class="sxs-lookup"><span data-stu-id="72e86-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="72e86-129">f.</span><span class="sxs-lookup"><span data-stu-id="72e86-129">f.</span></span> <span data-ttu-id="72e86-130">**Prijscategorie**: selecteer een prijscategorie, zie ACR-prijzen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="72e86-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="72e86-131">Meld u bij tooACR exemplaar</span><span class="sxs-lookup"><span data-stu-id="72e86-131">Log in tooACR instance</span></span>

<span data-ttu-id="72e86-132">Voordat u pushen en installatiekopieën van de container binnenhalen, moet u zich aanmeldt toohello ACR-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="72e86-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="72e86-133">toodo gebruik dus hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="72e86-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="72e86-134">Eerst, indien nodig, meld u aan bij Azure met behulp van Hallo [az aanmelding](/cli/azure/#login) opdracht.</span><span class="sxs-lookup"><span data-stu-id="72e86-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="72e86-135">Gebruik vervolgens Hallo [az acr aanmelding](/cli/azure/acr#login) opdracht toolog in Azure Container register toohello.</span><span class="sxs-lookup"><span data-stu-id="72e86-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="72e86-136">Azure Container Registry gebruiken</span><span class="sxs-lookup"><span data-stu-id="72e86-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="72e86-137">Containerinstallatiekopieën opvragen</span><span class="sxs-lookup"><span data-stu-id="72e86-137">List container images</span></span>

<span data-ttu-id="72e86-138">Gebruik Hallo `az acr` CLI-opdrachten tooquery Hallo installatiekopieën en labels in een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="72e86-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="72e86-139">Container register biedt momenteel geen ondersteuning voor Hallo `docker search` opdracht tooquery voor afbeeldingen en labels.</span><span class="sxs-lookup"><span data-stu-id="72e86-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="72e86-140">Opslagplaatsen weergeven</span><span class="sxs-lookup"><span data-stu-id="72e86-140">List repositories</span></span>

<span data-ttu-id="72e86-141">Hallo volgende voorbeeld worden Hallo-opslagplaatsen in een register, in JSON (JavaScript Object Notation)-indeling:</span><span class="sxs-lookup"><span data-stu-id="72e86-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="72e86-142">Tags weergeven</span><span class="sxs-lookup"><span data-stu-id="72e86-142">List tags</span></span>

<span data-ttu-id="72e86-143">Hallo volgende voorbeeld wordt een lijst Hallo labels op Hallo **samples/nginx** -opslagplaats, in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="72e86-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="72e86-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72e86-144">Next steps</span></span>

<span data-ttu-id="72e86-145">In deze snel starten, kunt u een beheerde Azure-Container register-exemplaar met gebruikmaking van hello Azure-portal hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="72e86-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72e86-146">Uw eerste installatiekopie met behulp van Docker CLI Hallo push</span><span class="sxs-lookup"><span data-stu-id="72e86-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
