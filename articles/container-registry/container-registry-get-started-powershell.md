---
title: aaaAzure container register opslagplaatsen | Microsoft Docs
description: "Hoe toouse Azure Container register opslagplaatsen voor Docker-installatiekopieën"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="3071b-103">Maken van een persoonlijke Docker-container register hello Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="3071b-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="3071b-104">Gebruik de opdrachten in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate een register container en beheren van de instellingen van uw Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="3071b-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="3071b-105">U kunt ook maken en beheren van container registers met Hallo [Azure-portal](container-registry-get-started-portal.md), Hallo [Azure CLI](container-registry-get-started-azure-cli.md), of programmatisch met Hallo Container register [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="3071b-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="3071b-106">Zie voor de achtergrond en concepten [Hallo overzicht](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="3071b-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="3071b-107">Zie voor een volledige lijst van ondersteunde cmdlets [register-Cmdlets voor Azure Container](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="3071b-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3071b-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3071b-108">Prerequisites</span></span>
* <span data-ttu-id="3071b-109">**Azure PowerShell**: tooinstall en aan de slag met Azure PowerShell, Zie Hallo [installatie-instructies](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3071b-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="3071b-110">Meld u bij de Azure-abonnement tooyour door te voeren `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="3071b-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="3071b-111">Zie voor meer informatie [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="3071b-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="3071b-112">**Resourcegroep**: maak eerst een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) voordat u een containerregister maakt of gebruik een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3071b-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="3071b-113">Zorg ervoor dat Hallo resourcegroep bevindt zich in een locatie waar Hallo Container Registry-service is [beschikbaar](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="3071b-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="3071b-114">een resourcegroep met Azure PowerShell toocreate Zie [Hallo PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="3071b-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="3071b-115">**Storage-account** (optioneel): Maak een standaard Azure [opslagaccount](../storage/common/storage-introduction.md) tooback Hallo container register in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="3071b-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="3071b-116">Als u een opslagaccount niet opgeven bij het maken van een register met `New-AzureRMContainerRegistry`, Hallo opdracht maakt u een voor u.</span><span class="sxs-lookup"><span data-stu-id="3071b-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="3071b-117">toocreate een opslag-account met behulp van PowerShell, raadpleegt u [Hallo PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="3071b-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="3071b-118">Premium-opslag wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3071b-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="3071b-119">**Service-principal** (optioneel): wanneer u een register met PowerShell maakt, standaard het is niet ingesteld voor toegang.</span><span class="sxs-lookup"><span data-stu-id="3071b-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="3071b-120">Afhankelijk van uw behoeften kunt u een bestaande Azure Active Directory service principal tooa register toewijzen of maken en toewijzen van een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="3071b-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="3071b-121">U kunt ook van het register Hallo beheerder gebruikersaccount inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3071b-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="3071b-122">Zie Hallo secties verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3071b-122">See hello sections later in this article.</span></span> <span data-ttu-id="3071b-123">Zie voor meer informatie over toegang tot het register, [verifiëren met Hallo container register](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3071b-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="3071b-124">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="3071b-124">Create a container registry</span></span>
<span data-ttu-id="3071b-125">Voer Hallo `New-AzureRMContainerRegistry` opdracht toocreate een container-register.</span><span class="sxs-lookup"><span data-stu-id="3071b-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="3071b-126">Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="3071b-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="3071b-127">naam van de Hallo register in Hallo voorbeelden is `MyRegistry`, maar vervangen door een unieke naam van uw eigen.</span><span class="sxs-lookup"><span data-stu-id="3071b-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="3071b-128">Hallo van de volgende opdracht maakt gebruik van Hallo minimale parameters toocreate container register `MyRegistry` in de resourcegroep Hallo `MyResourceGroup` in Hallo Zuid-centraal VS locatie:</span><span class="sxs-lookup"><span data-stu-id="3071b-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="3071b-129">`-StorageAccountName` is optioneel.</span><span class="sxs-lookup"><span data-stu-id="3071b-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="3071b-130">Als dat niet is opgegeven, een opslagaccount is gemaakt met een naam die bestaan uit Hallo registernaam en een tijdstempel in Hallo opgegeven resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3071b-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="3071b-131">Een service-principal toewijzen</span><span class="sxs-lookup"><span data-stu-id="3071b-131">Assign a service principal</span></span>
<span data-ttu-id="3071b-132">Gebruik PowerShell-opdrachten tooassign een Azure Active Directory [service-principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa register.</span><span class="sxs-lookup"><span data-stu-id="3071b-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="3071b-133">Hallo service-principal in deze voorbeelden is toegewezen rol van eigenaar hello, maar u kunt toewijzen [andere rollen](../active-directory/role-based-access-control-configure.md) als u wilt.</span><span class="sxs-lookup"><span data-stu-id="3071b-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="3071b-134">Een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="3071b-134">Create a service principal</span></span>
<span data-ttu-id="3071b-135">In Hallo volgende opdracht, wordt een nieuwe service-principal gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3071b-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="3071b-136">Geef een sterk wachtwoord Hello `-Password` parameter.</span><span class="sxs-lookup"><span data-stu-id="3071b-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="3071b-137">Een nieuwe of bestaande service-principal toewijzen</span><span class="sxs-lookup"><span data-stu-id="3071b-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="3071b-138">U kunt een nieuwe of een bestaande service-principal tooa register toewijzen.</span><span class="sxs-lookup"><span data-stu-id="3071b-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="3071b-139">tooassign deze eigenaar rol toegang toohello register, uitvoeren van een opdracht vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="3071b-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="3071b-140">Meld u aan toohello register met Hallo service-principal</span><span class="sxs-lookup"><span data-stu-id="3071b-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="3071b-141">Na het toewijzen van Hallo service principal toohello register, kunt u zich aanmeldt met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3071b-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="3071b-142">Beheerreferenties beheren</span><span class="sxs-lookup"><span data-stu-id="3071b-142">Manage admin credentials</span></span>
<span data-ttu-id="3071b-143">Er wordt automatisch een beheeraccount gemaakt voor elk containerregister. Dit account is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3071b-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="3071b-144">Hallo volgende voorbeelden tonen PowerShell-opdrachten toomanage Hallo beheerdersreferenties voor de container-register.</span><span class="sxs-lookup"><span data-stu-id="3071b-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="3071b-145">Beheerreferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="3071b-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="3071b-146">Beheerder inschakelen voor een bestaand register</span><span class="sxs-lookup"><span data-stu-id="3071b-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="3071b-147">Beheerder uitschakelen voor een bestaand register</span><span class="sxs-lookup"><span data-stu-id="3071b-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="3071b-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3071b-148">Next steps</span></span>
* [<span data-ttu-id="3071b-149">Uw eerste installatiekopie met behulp van Docker CLI Hallo push</span><span class="sxs-lookup"><span data-stu-id="3071b-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
