---
title: PowerShell-voorbeeldscript - aaaAzure een web-app maken en implementeren van de code van een lokale Git-opslagplaats | Microsoft Docs
description: Azure PowerShell-voorbeeldscript - web-app maken en implementeren van de code van een lokale Git-opslagplaats
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="15ba4-103">Een web-app maken en implementeren van de code van een lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="15ba4-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="15ba4-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code in een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="15ba4-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="15ba4-105">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="15ba4-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="15ba4-106">Bovendien moet de toepassingscode toobe doorgevoerd in een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="15ba4-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="15ba4-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="15ba4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="15ba4-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="15ba4-108">Clean up deployment</span></span> 

<span data-ttu-id="15ba4-109">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="15ba4-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="15ba4-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="15ba4-110">Script explanation</span></span>

<span data-ttu-id="15ba4-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="15ba4-111">This script uses hello following commands.</span></span> <span data-ttu-id="15ba4-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="15ba4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="15ba4-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="15ba4-113">Command</span></span> | <span data-ttu-id="15ba4-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="15ba4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="15ba4-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="15ba4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="15ba4-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="15ba4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="15ba4-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="15ba4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="15ba4-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="15ba4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="15ba4-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="15ba4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="15ba4-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="15ba4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="15ba4-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="15ba4-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="15ba4-122">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="15ba4-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="15ba4-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="15ba4-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="15ba4-124">Profiel voor het publiceren van een web-app worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="15ba4-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="15ba4-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15ba4-125">Next steps</span></span>

<span data-ttu-id="15ba4-126">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="15ba4-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="15ba4-127">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="15ba4-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
