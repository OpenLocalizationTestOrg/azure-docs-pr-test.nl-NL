---
title: PowerShell-voorbeeldscript - aaaAzure een web-app maken en implementeren van code vanuit GitHub | Microsoft Docs
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
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="3d073-103">Een web-app maken en implementeren van code vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="3d073-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="3d073-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code uit een openbare GitHub-opslagplaats (zonder continue implementatie).</span><span class="sxs-lookup"><span data-stu-id="3d073-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="3d073-105">Zie voor een implementatie met continue implementatie van GitHub [een WebApp maken met continue implementatie van GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="3d073-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="3d073-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d073-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="3d073-107">U moet ook een koppeling tooGitHub opslagplaats die Hallo web-app-code bevat.</span><span class="sxs-lookup"><span data-stu-id="3d073-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3d073-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3d073-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3d073-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3d073-109">Clean up deployment</span></span> 

<span data-ttu-id="3d073-110">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="3d073-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3d073-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3d073-111">Script explanation</span></span>

<span data-ttu-id="3d073-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="3d073-112">This script uses hello following commands.</span></span> <span data-ttu-id="3d073-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="3d073-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3d073-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3d073-114">Command</span></span> | <span data-ttu-id="3d073-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3d073-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d073-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3d073-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3d073-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3d073-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3d073-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3d073-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3d073-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3d073-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3d073-120">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3d073-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3d073-121">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="3d073-121">Creates a web app.</span></span> |
| [<span data-ttu-id="3d073-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3d073-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="3d073-123">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3d073-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d073-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d073-124">Next steps</span></span>

<span data-ttu-id="3d073-125">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d073-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3d073-126">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3d073-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
