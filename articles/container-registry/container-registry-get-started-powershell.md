---
title: Azure-container register opslagplaatsen | Microsoft Docs
description: "Het gebruik van Azure Container register-opslagplaatsen voor Docker-installatiekopieën"
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
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="122e2-103">Maken van een persoonlijke Docker-container register met de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="122e2-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="122e2-104">Gebruik de opdrachten in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) een register container maken en beheren van de instellingen van uw Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="122e2-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="122e2-105">U kunt ook maken en beheren van container registers met behulp van de [Azure-portal](container-registry-get-started-portal.md), wordt de [Azure CLI](container-registry-get-started-azure-cli.md), of programmatisch met het register van de Container [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="122e2-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="122e2-106">Zie [het overzicht](container-registry-intro.md) voor meer achtergrondinformatie en concepten</span><span class="sxs-lookup"><span data-stu-id="122e2-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="122e2-107">Zie voor een volledige lijst van ondersteunde cmdlets [register-Cmdlets voor Azure Container](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="122e2-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="122e2-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="122e2-108">Prerequisites</span></span>
* <span data-ttu-id="122e2-109">**Azure PowerShell**: wilt installeren en aan de slag met Azure PowerShell, Zie de [installatie-instructies](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="122e2-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="122e2-110">Meld u aan bij uw Azure-abonnement door `Login-AzureRMAccount` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="122e2-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="122e2-111">Zie voor meer informatie [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="122e2-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="122e2-112">**Resourcegroep**: maak eerst een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) voordat u een containerregister maakt of gebruik een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="122e2-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="122e2-113">De resourcegroep moet op een locatie staan waar de Container Registry-service [beschikbaar](https://azure.microsoft.com/regions/services/) is.</span><span class="sxs-lookup"><span data-stu-id="122e2-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="122e2-114">Zie het maken van een resourcegroep met Azure PowerShell [de PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="122e2-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="122e2-115">**Opslagaccount** (optioneel): maak een standaard-Azure-[opslagaccount](../storage/common/storage-introduction.md) om een back-up van het containerregister te maken op dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="122e2-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="122e2-116">Als u geen opslagaccount opgeeft bij het maken van een register met `New-AzureRMContainerRegistry`, maakt de opdracht er een.</span><span class="sxs-lookup"><span data-stu-id="122e2-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="122e2-117">Zie het maken van een opslagaccount met behulp van PowerShell [de PowerShell-referentie](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="122e2-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="122e2-118">Premium-opslag wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="122e2-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="122e2-119">**Service-principal** (optioneel): wanneer u een register met PowerShell maakt, standaard het is niet ingesteld voor toegang.</span><span class="sxs-lookup"><span data-stu-id="122e2-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="122e2-120">Afhankelijk van uw behoeften kunt u een bestaand Azure Active Directory-service-principal toewijzen aan een register of maken en toewijzen van een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="122e2-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="122e2-121">U kunt ook kunt u een gebruikersaccount in het register beheerder inschakelen.</span><span class="sxs-lookup"><span data-stu-id="122e2-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="122e2-122">Zie de gedeelten verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="122e2-122">See the sections later in this article.</span></span> <span data-ttu-id="122e2-123">Bekijk voor meer informatie over registertoegang [Verifiëren met het containerregister](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="122e2-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="122e2-124">Een containerregister maken</span><span class="sxs-lookup"><span data-stu-id="122e2-124">Create a container registry</span></span>
<span data-ttu-id="122e2-125">Voer de opdracht `New-AzureRMContainerRegistry` uit om een containerregister te maken.</span><span class="sxs-lookup"><span data-stu-id="122e2-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="122e2-126">Geef bij het maken van een register een unieke domeinnaam op het hoogste niveau op, bestaande uit alleen letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="122e2-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="122e2-127">De registernaam in de voorbeelden is `MyRegistry`, maar u hoort deze door uw eigen unieke naam te vervangen.</span><span class="sxs-lookup"><span data-stu-id="122e2-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="122e2-128">De volgende opdracht maakt gebruik van de minimale parameters om containerregister `MyRegistry` te maken in de resourcegroep `MyResourceGroup` in de locatie Zuid-centraal VS:</span><span class="sxs-lookup"><span data-stu-id="122e2-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="122e2-129">`-StorageAccountName` is optioneel.</span><span class="sxs-lookup"><span data-stu-id="122e2-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="122e2-130">Als deze optie niet wordt opgegeven, wordt er een opslagaccount gemaakt in de opgegeven resourcegroep met een naam die bestaat uit de registernaam en een tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="122e2-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="122e2-131">Een service-principal toewijzen</span><span class="sxs-lookup"><span data-stu-id="122e2-131">Assign a service principal</span></span>
<span data-ttu-id="122e2-132">PowerShell-opdrachten gebruiken voor het toewijzen van een Azure Active Directory [service-principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) met een register.</span><span class="sxs-lookup"><span data-stu-id="122e2-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="122e2-133">Aan de service-principal in deze voorbeelden is de rol Eigenaar toegewezen, maar u kunt ook [andere rollen](../active-directory/role-based-access-control-configure.md) toewijzen.</span><span class="sxs-lookup"><span data-stu-id="122e2-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="122e2-134">Een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="122e2-134">Create a service principal</span></span>
<span data-ttu-id="122e2-135">In de volgende opdracht, wordt een nieuwe service-principal gemaakt.</span><span class="sxs-lookup"><span data-stu-id="122e2-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="122e2-136">Geef een sterk wachtwoord op voor de parameter `-Password`.</span><span class="sxs-lookup"><span data-stu-id="122e2-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="122e2-137">Een nieuwe of bestaande service-principal toewijzen</span><span class="sxs-lookup"><span data-stu-id="122e2-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="122e2-138">U kunt een nieuwe of een bestaande service-principal toewijzen aan een register.</span><span class="sxs-lookup"><span data-stu-id="122e2-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="122e2-139">Toe te wijzen eigenaar roltoegang aan het register, een opdracht die vergelijkbaar is met het volgende voorbeeld wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="122e2-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="122e2-140">Meld u aan met het register met de service-principal</span><span class="sxs-lookup"><span data-stu-id="122e2-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="122e2-141">Na het toewijzen van de service-principal in het register, kunt u aanmelden met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="122e2-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="122e2-142">Beheerreferenties beheren</span><span class="sxs-lookup"><span data-stu-id="122e2-142">Manage admin credentials</span></span>
<span data-ttu-id="122e2-143">Er wordt automatisch een beheeraccount gemaakt voor elk containerregister. Dit account is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="122e2-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="122e2-144">De volgende voorbeelden tonen PowerShell-opdrachten voor het beheren van de beheerdersreferenties voor de container-register.</span><span class="sxs-lookup"><span data-stu-id="122e2-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="122e2-145">Beheerreferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="122e2-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="122e2-146">Beheerder inschakelen voor een bestaand register</span><span class="sxs-lookup"><span data-stu-id="122e2-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="122e2-147">Beheerder uitschakelen voor een bestaand register</span><span class="sxs-lookup"><span data-stu-id="122e2-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="122e2-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="122e2-148">Next steps</span></span>
* [<span data-ttu-id="122e2-149">Uw eerste installatiekopie pushen met de Docker-CLI</span><span class="sxs-lookup"><span data-stu-id="122e2-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
