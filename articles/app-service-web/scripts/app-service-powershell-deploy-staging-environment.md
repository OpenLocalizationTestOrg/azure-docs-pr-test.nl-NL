---
title: PowerShell-voorbeeldscript - aaaAzure een web-app maken en implementeren van code tooa staging-omgeving | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - web-app maken en implementeren van code tooa staging-omgeving
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="a39f8-103">Een web-app maken en implementeren van code tooa staging-omgeving</span><span class="sxs-lookup"><span data-stu-id="a39f8-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="a39f8-104">Dit voorbeeldscript maakt u een web-app in App Service met een extra implementatiesleuf "fasering" genoemd, en implementeert u een voorbeeld-app toohello 'fasering' sleuf.</span><span class="sxs-lookup"><span data-stu-id="a39f8-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="a39f8-105">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="a39f8-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a39f8-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a39f8-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a39f8-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a39f8-107">Clean up deployment</span></span> 

<span data-ttu-id="a39f8-108">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="a39f8-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a39f8-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a39f8-109">Script explanation</span></span>

<span data-ttu-id="a39f8-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a39f8-110">This script uses hello following commands.</span></span> <span data-ttu-id="a39f8-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a39f8-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a39f8-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a39f8-112">Command</span></span> | <span data-ttu-id="a39f8-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a39f8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a39f8-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a39f8-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a39f8-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a39f8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a39f8-116">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a39f8-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a39f8-117">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a39f8-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a39f8-118">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a39f8-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a39f8-119">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="a39f8-119">Creates a web app.</span></span> |
| [<span data-ttu-id="a39f8-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a39f8-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="a39f8-121">Hiermee wijzigt u een App Service plan toochange de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="a39f8-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="a39f8-122">Nieuwe AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="a39f8-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="a39f8-123">Maakt een implementatiesleuf voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="a39f8-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="a39f8-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="a39f8-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="a39f8-125">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a39f8-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="a39f8-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="a39f8-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="a39f8-127">Wisselt de uitrolfase van een web-app in productie.</span><span class="sxs-lookup"><span data-stu-id="a39f8-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a39f8-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a39f8-128">Next steps</span></span>

<span data-ttu-id="a39f8-129">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a39f8-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a39f8-130">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a39f8-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
