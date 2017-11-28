---
title: Azure PowerShell-Script voorbeeld - web-app maken en implementeren van code in een testomgeving | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - web-app maken en implementeren van code in een testomgeving
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
ms.openlocfilehash: 55adc13350eb0f4711efa3c901f6e4e7755dfb27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="74acc-103">Een web-app maken en implementeren van code in een testomgeving</span><span class="sxs-lookup"><span data-stu-id="74acc-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="74acc-104">Dit voorbeeldscript maakt u een web-app in App Service met een extra implementatiesleuf naam 'staging', en implementeert u een voorbeeld-app in de sleuf 'staging'.</span><span class="sxs-lookup"><span data-stu-id="74acc-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="74acc-105">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="74acc-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="74acc-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="74acc-106">Sample script</span></span>

<span data-ttu-id="74acc-107">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "een web-app maken en implementeren van code in een testomgeving")]</span><span class="sxs-lookup"><span data-stu-id="74acc-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="74acc-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="74acc-108">Clean up deployment</span></span> 

<span data-ttu-id="74acc-109">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="74acc-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="74acc-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="74acc-110">Script explanation</span></span>

<span data-ttu-id="74acc-111">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="74acc-111">This script uses the following commands.</span></span> <span data-ttu-id="74acc-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="74acc-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="74acc-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="74acc-113">Command</span></span> | <span data-ttu-id="74acc-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="74acc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="74acc-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="74acc-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="74acc-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="74acc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="74acc-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="74acc-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="74acc-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="74acc-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="74acc-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="74acc-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="74acc-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="74acc-120">Creates a web app.</span></span> |
| [<span data-ttu-id="74acc-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="74acc-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="74acc-122">Hiermee wijzigt u een App Service-abonnement als de prijscategorie wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="74acc-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="74acc-123">Nieuwe AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="74acc-123">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="74acc-124">Maakt een implementatiesleuf voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="74acc-124">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="74acc-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="74acc-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="74acc-126">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="74acc-126">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="74acc-127">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="74acc-127">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="74acc-128">Wisselt de uitrolfase van een web-app in productie.</span><span class="sxs-lookup"><span data-stu-id="74acc-128">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74acc-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74acc-129">Next steps</span></span>

<span data-ttu-id="74acc-130">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="74acc-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="74acc-131">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="74acc-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
