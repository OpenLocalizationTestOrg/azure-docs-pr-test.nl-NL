---
title: een Azure Analysis Services-server met behulp van PowerShell aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure Analysis Services-server met behulp van PowerShell
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="1ae57-103">Een Azure Analysis Services-server maken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ae57-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="1ae57-104">Deze snelstartgids wordt beschreven met behulp van PowerShell van Hallo opdrachtregel toocreate een Azure Analysis Services-server in een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1ae57-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="1ae57-105">Voor deze taak is Azure PowerShell-moduleversie 4.0 of hoger vereist.</span><span class="sxs-lookup"><span data-stu-id="1ae57-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="1ae57-106">toofind hello versie, voer ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="1ae57-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="1ae57-107">tooinstall upgraden, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1ae57-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="1ae57-108">Het maken van een server kan zorgen voor een nieuwe factureerbare service.</span><span class="sxs-lookup"><span data-stu-id="1ae57-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="1ae57-109">toolearn meer, Zie [Analysis Services-prijzen](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="1ae57-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ae57-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1ae57-110">Prerequisites</span></span>
<span data-ttu-id="1ae57-111">toocomplete deze snelstartgids die u nodig:</span><span class="sxs-lookup"><span data-stu-id="1ae57-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="1ae57-112">**Azure-abonnement**: Ga naar [gratis proefversie van Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate een account.</span><span class="sxs-lookup"><span data-stu-id="1ae57-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="1ae57-113">**Azure Active Directory**: uw abonnement moet worden gekoppeld aan een Azure Active Directory-tenant en u moet een account hebben in de betreffende map.</span><span class="sxs-lookup"><span data-stu-id="1ae57-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="1ae57-114">toolearn meer, Zie [verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="1ae57-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="1ae57-115">AzureRm.AnalysisServices-module importeren</span><span class="sxs-lookup"><span data-stu-id="1ae57-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="1ae57-116">een server in uw abonnement toocreate, gebruikt u Hallo [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) onderdeel module.</span><span class="sxs-lookup"><span data-stu-id="1ae57-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="1ae57-117">Hallo AzureRm.AnalysisServices module in uw PowerShell-sessie laden.</span><span class="sxs-lookup"><span data-stu-id="1ae57-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="1ae57-118">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="1ae57-118">Sign in tooAzure</span></span>

<span data-ttu-id="1ae57-119">Azure-abonnement tooyour aanmelden via Hallo [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1ae57-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="1ae57-120">Volg Hallo op het scherm-instructies.</span><span class="sxs-lookup"><span data-stu-id="1ae57-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="1ae57-121">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="1ae57-121">Create a resource group</span></span>
 
<span data-ttu-id="1ae57-122">Een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) is een logische container waarin Azure-resources worden geïmplementeerd en als groep beheerd.</span><span class="sxs-lookup"><span data-stu-id="1ae57-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="1ae57-123">Wanneer u de server maakt, moet u een resourcegroep opgeven in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="1ae57-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="1ae57-124">Als u nog geen een resourcegroep, kunt u een nieuwe met behulp van Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1ae57-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="1ae57-125">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in de regio VS-West Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ae57-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="1ae57-126">Een server maken</span><span class="sxs-lookup"><span data-stu-id="1ae57-126">Create a server</span></span>

<span data-ttu-id="1ae57-127">Maak een nieuwe server met behulp van Hallo [nieuw AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1ae57-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="1ae57-128">Hallo volgende voorbeeld maakt u een server met de naam MijnServer in myResourceGroup in Hallo VS-West regio op Hallo D1 laag, en geeft philipc@adventureworks.com als serverbeheerder.</span><span class="sxs-lookup"><span data-stu-id="1ae57-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="1ae57-129">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="1ae57-129">Clean up resources</span></span>

<span data-ttu-id="1ae57-130">U kunt Hallo server verwijderen uit uw abonnement via Hallo [verwijderen AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1ae57-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="1ae57-131">Verwijder de server niet als u met andere snelstartgidsen en zelfstudies in deze verzameling doorgaat.</span><span class="sxs-lookup"><span data-stu-id="1ae57-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="1ae57-132">Hallo verwijdert volgende voorbeeld Hallo-server in de vorige stap Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ae57-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="1ae57-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ae57-133">Next steps</span></span>
<span data-ttu-id="1ae57-134">[Azure Analysis Services beheren met PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="1ae57-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="1ae57-135">[Een model implementeren vanuit SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="1ae57-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="1ae57-136">Een model maken in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1ae57-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)