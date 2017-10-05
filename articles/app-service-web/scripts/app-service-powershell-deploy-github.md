---
title: Azure PowerShell-Script voorbeeld - web-app maken en implementeren van code vanuit GitHub | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - web-app maken en implementeren van code vanuit GitHub
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1f7fc21dc12c334f5d347ae9918bd62945bede64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="a1862-103">Een web-app maken en implementeren van code vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="a1862-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="a1862-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code uit een openbare GitHub-opslagplaats (zonder continue implementatie).</span><span class="sxs-lookup"><span data-stu-id="a1862-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="a1862-105">Zie voor een implementatie met continue implementatie van GitHub [een WebApp maken met continue implementatie van GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="a1862-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="a1862-106">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a1862-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="a1862-107">U moet ook een koppeling naar de GitHub-opslagplaats met de web-app-code.</span><span class="sxs-lookup"><span data-stu-id="a1862-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a1862-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a1862-108">Sample script</span></span>

<span data-ttu-id="a1862-109">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "een web-app maken en implementeren van code vanuit GitHub")]</span><span class="sxs-lookup"><span data-stu-id="a1862-109">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a1862-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a1862-110">Clean up deployment</span></span> 

<span data-ttu-id="a1862-111">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a1862-111">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a1862-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a1862-112">Script explanation</span></span>

<span data-ttu-id="a1862-113">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="a1862-113">This script uses the following commands.</span></span> <span data-ttu-id="a1862-114">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="a1862-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a1862-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a1862-115">Command</span></span> | <span data-ttu-id="a1862-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a1862-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a1862-117">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a1862-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a1862-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a1862-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a1862-119">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a1862-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a1862-120">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a1862-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a1862-121">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a1862-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a1862-122">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="a1862-122">Creates a web app.</span></span> |
| [<span data-ttu-id="a1862-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="a1862-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="a1862-124">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a1862-124">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a1862-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a1862-125">Next steps</span></span>

<span data-ttu-id="a1862-126">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a1862-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a1862-127">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a1862-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
