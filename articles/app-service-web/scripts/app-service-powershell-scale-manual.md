---
title: 'Azure PowerShell-Script voorbeeld: een web-app handmatig schalen | Microsoft Docs'
description: 'Azure PowerShell-Script voorbeeld: een web-app handmatig schalen'
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="6507e-103">Een web-app handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="6507e-103">Scale a web app manually</span></span>

<span data-ttu-id="6507e-104">In dit scenario leert u een resourcegroep, de app service-plan en web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="6507e-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="6507e-105">U wordt vervolgens de schaal de App Service-abonnement van één exemplaar naar meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="6507e-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="6507e-106">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="6507e-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6507e-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="6507e-107">Sample script</span></span>

<span data-ttu-id="6507e-108">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "handmatig schalen van een web-app")]</span><span class="sxs-lookup"><span data-stu-id="6507e-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6507e-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="6507e-109">Clean up deployment</span></span> 

<span data-ttu-id="6507e-110">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6507e-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6507e-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="6507e-111">Script explanation</span></span>

<span data-ttu-id="6507e-112">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="6507e-112">This script uses the following commands.</span></span> <span data-ttu-id="6507e-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="6507e-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6507e-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6507e-114">Command</span></span> | <span data-ttu-id="6507e-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6507e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6507e-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6507e-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6507e-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6507e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6507e-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6507e-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6507e-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6507e-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6507e-120">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6507e-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6507e-121">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="6507e-121">Creates a web app.</span></span> |
| [<span data-ttu-id="6507e-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6507e-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="6507e-123">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6507e-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6507e-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6507e-124">Next steps</span></span>

<span data-ttu-id="6507e-125">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6507e-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6507e-126">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6507e-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
