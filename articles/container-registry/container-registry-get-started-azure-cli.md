---
title: aaaCreate persoonlijke Docker-container register - Azure CLI | Microsoft Docs
description: Aan de slag maken en beheren van persoonlijke Docker-container registers Hello Azure CLI 2.0
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="a1b6d-103">Maken van een persoonlijke Docker-container register met hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a1b6d-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="a1b6d-104">Met de opdrachten in Hallo [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate een register container en beheren van de instellingen van uw Linux, Mac of Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="a1b6d-105">U kunt ook maken en beheren van container registers met Hallo [Azure-portal](container-registry-get-started-portal.md) of programmatisch met Hallo Container register [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="a1b6d-106">Zie voor de achtergrond en concepten [Hallo overzicht](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a1b6d-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="a1b6d-107">Voor meer informatie over Container register CLI-opdrachten (`az acr` opdrachten), doorgegeven Hallo `-h` parameter tooany opdracht.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a1b6d-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a1b6d-108">Prerequisites</span></span>
* <span data-ttu-id="a1b6d-109">**Azure CLI 2.0**: tooinstall en aan de slag met Hallo CLI 2.0, Zie Hallo [installatie-instructies](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a1b6d-110">Meld u bij de Azure-abonnement tooyour door te voeren `az login`.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="a1b6d-111">Zie voor meer informatie [aan de slag met Hallo CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="a1b6d-112">**Resourcegroep**: maak eerst een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) voordat u een containerregister maakt of gebruik een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="a1b6d-113">Zorg ervoor dat Hallo resourcegroep bevindt zich in een locatie waar Hallo Container Registry-service is [beschikbaar](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="a1b6d-114">een resource-groep met toocreate Hallo CLI 2.0, Zie [Hallo CLI 2.0 verwijzing](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="a1b6d-115">**Storage-account** (optioneel): Maak een standaard Azure [opslagaccount](../storage/common/storage-introduction.md) tooback Hallo container register in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="a1b6d-116">Als u een opslagaccount niet opgeven bij het maken van een register met `az acr create`, Hallo opdracht maakt u een voor u.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="a1b6d-117">een storage-account met toocreate Hallo CLI 2.0, Zie [Hallo CLI 2.0 verwijzing](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="a1b6d-118">Premium-opslag wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="a1b6d-119">**Service-principal** (optioneel): wanneer u een register met CLI hello maakt, standaard het is niet ingesteld voor toegang.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="a1b6d-120">Afhankelijk van uw behoeften kunt u een bestaande Azure Active Directory service principal tooa register toewijzen (of maken en toewijzen van een nieuw), of van het register Hallo beheerder gebruikersaccount in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="a1b6d-121">Zie Hallo secties verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-121">See hello sections later in this article.</span></span> <span data-ttu-id="a1b6d-122">Zie voor meer informatie over toegang tot het register, [verifiëren met Hallo container register](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="a1b6d-123">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="a1b6d-123">Create a container registry</span></span>
<span data-ttu-id="a1b6d-124">Voer Hallo `az acr create` opdracht toocreate een container-register.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="a1b6d-125">Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="a1b6d-126">naam van de Hallo register in Hallo voorbeelden is `myRegistry1`, maar vervangen door een unieke naam van uw eigen.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="a1b6d-127">Hallo van de volgende opdracht maakt gebruik van Hallo minimale parameters toocreate container register `myRegistry1` in de resourcegroep Hallo `myResourceGroup`, en het gebruik van Hallo *Basic* sku:</span><span class="sxs-lookup"><span data-stu-id="a1b6d-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="a1b6d-128">`--storage-account-name` is optioneel.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="a1b6d-129">Als dat niet is opgegeven, een opslagaccount is gemaakt met een naam die bestaan uit Hallo registernaam en een tijdstempel in Hallo opgegeven resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="a1b6d-130">Bij Hallo register wordt gemaakt, is het Hallo-uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a1b6d-130">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="a1b6d-131">Belangrijk:</span><span class="sxs-lookup"><span data-stu-id="a1b6d-131">Take special note:</span></span>

* <span data-ttu-id="a1b6d-132">`id`-ID voor Hallo register in uw abonnement, u moet als u wilt dat een service-principal tooassign.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="a1b6d-133">`loginServer`-Hallo volledig gekwalificeerde naam die u te opgeeft[toohello register aanmelden](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="a1b6d-134">In dit voorbeeld is de naam van de Hallo `myregistry1.exp.azurecr.io` (alle kleine letters).</span><span class="sxs-lookup"><span data-stu-id="a1b6d-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="a1b6d-135">Een service-principal toewijzen</span><span class="sxs-lookup"><span data-stu-id="a1b6d-135">Assign a service principal</span></span>
<span data-ttu-id="a1b6d-136">CLI 2.0 opdrachten tooassign een Azure Active Directory-service-principal tooa registry gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="a1b6d-137">Hallo service-principal in deze voorbeelden is toegewezen rol van eigenaar hello, maar u kunt toewijzen [andere rollen](../active-directory/role-based-access-control-configure.md) als u wilt.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="a1b6d-138">Een service-principal maken en toewijzen van toegang toohello register</span><span class="sxs-lookup"><span data-stu-id="a1b6d-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="a1b6d-139">In Hallo volgende opdracht, een nieuwe service-principal eigenaar rol toegang toohello register-id doorgegeven Hello toegewezen `--scopes` parameter.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="a1b6d-140">Geef een sterk wachtwoord Hello `--password` parameter.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="a1b6d-141">Een bestaande service-principal toewijzen</span><span class="sxs-lookup"><span data-stu-id="a1b6d-141">Assign an existing service principal</span></span>
<span data-ttu-id="a1b6d-142">Als u al een service-principal en tooassign wilt deze eigenaar rol toegang toohello register, uitvoeren van een opdracht vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="a1b6d-143">U Hallo service principal app-ID met Hallo doorgeeft `--assignee` parameter:</span><span class="sxs-lookup"><span data-stu-id="a1b6d-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="a1b6d-144">Beheerreferenties beheren</span><span class="sxs-lookup"><span data-stu-id="a1b6d-144">Manage admin credentials</span></span>
<span data-ttu-id="a1b6d-145">Er wordt automatisch een beheeraccount gemaakt voor elk containerregister. Dit account is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="a1b6d-146">Hallo volgen voorbeelden `az acr` CLI-opdrachten toomanage Hallo beheerdersreferenties voor de container-register.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="a1b6d-147">Beheerreferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="a1b6d-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="a1b6d-148">Beheerder inschakelen voor een bestaand register</span><span class="sxs-lookup"><span data-stu-id="a1b6d-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="a1b6d-149">Beheerder uitschakelen voor een bestaand register</span><span class="sxs-lookup"><span data-stu-id="a1b6d-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="a1b6d-150">Installatiekopieën en tags weergeven</span><span class="sxs-lookup"><span data-stu-id="a1b6d-150">List images and tags</span></span>
<span data-ttu-id="a1b6d-151">Gebruik Hallo `az acr` CLI-opdrachten tooquery Hallo installatiekopieën en labels in een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a1b6d-152">Container register biedt momenteel geen ondersteuning voor Hallo `docker search` opdracht tooquery voor afbeeldingen en labels.</span><span class="sxs-lookup"><span data-stu-id="a1b6d-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="a1b6d-153">Opslagplaatsen weergeven</span><span class="sxs-lookup"><span data-stu-id="a1b6d-153">List repositories</span></span>
<span data-ttu-id="a1b6d-154">Hallo volgende voorbeeld worden Hallo-opslagplaatsen in een register, in JSON (JavaScript Object Notation)-indeling:</span><span class="sxs-lookup"><span data-stu-id="a1b6d-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="a1b6d-155">Tags weergeven</span><span class="sxs-lookup"><span data-stu-id="a1b6d-155">List tags</span></span>
<span data-ttu-id="a1b6d-156">Hallo volgende voorbeeld wordt een lijst Hallo labels op Hallo **samples/nginx** -opslagplaats, in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="a1b6d-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="a1b6d-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a1b6d-157">Next steps</span></span>
* [<span data-ttu-id="a1b6d-158">Uw eerste installatiekopie met behulp van Docker CLI Hallo push</span><span class="sxs-lookup"><span data-stu-id="a1b6d-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
