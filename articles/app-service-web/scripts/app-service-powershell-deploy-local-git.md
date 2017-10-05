---
title: Azure PowerShell-voorbeeldscript - web-app maken en implementeren van de code van een lokale Git-opslagplaats | Microsoft Docs
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
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="4a618-103">Een web-app maken en implementeren van de code van een lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="4a618-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="4a618-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code in een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4a618-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="4a618-105">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="4a618-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="4a618-106">Bovendien moet de toepassingscode worden vastgelegd in een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4a618-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="4a618-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4a618-107">Sample script</span></span>

<span data-ttu-id="4a618-108">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "een web-app maken en implementeren van de code van een lokale Git-opslagplaats")]</span><span class="sxs-lookup"><span data-stu-id="4a618-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4a618-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="4a618-109">Clean up deployment</span></span> 

<span data-ttu-id="4a618-110">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4a618-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4a618-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4a618-111">Script explanation</span></span>

<span data-ttu-id="4a618-112">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4a618-112">This script uses the following commands.</span></span> <span data-ttu-id="4a618-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="4a618-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4a618-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4a618-114">Command</span></span> | <span data-ttu-id="4a618-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4a618-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4a618-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4a618-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4a618-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4a618-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4a618-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4a618-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4a618-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4a618-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4a618-120">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4a618-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4a618-121">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="4a618-121">Creates a web app.</span></span> |
| [<span data-ttu-id="4a618-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4a618-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="4a618-123">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="4a618-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="4a618-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="4a618-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="4a618-125">Profiel voor het publiceren van een web-app worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="4a618-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4a618-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a618-126">Next steps</span></span>

<span data-ttu-id="4a618-127">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4a618-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4a618-128">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4a618-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
