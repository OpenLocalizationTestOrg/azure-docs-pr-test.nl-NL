---
title: 'Azure PowerShell-Script voorbeeld: een web-app maken met continue implementatie van GitHub | Microsoft Docs'
description: 'Azure PowerShell-Script voorbeeld: een web-app maken met continue implementatie van GitHub'
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="0a7ad-103">Een WebApp maken met continue implementatie van GitHub</span><span class="sxs-lookup"><span data-stu-id="0a7ad-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="0a7ad-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en vervolgens stelt continue implementatie van een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="0a7ad-105">Zie voor de implementatie van GitHub zonder continue implementatie [een web-app maken en implementeren van code vanuit GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="0a7ad-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="0a7ad-106">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a7ad-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="0a7ad-107">Controleer ook of:</span><span class="sxs-lookup"><span data-stu-id="0a7ad-107">Also, ensure that:</span></span>

- <span data-ttu-id="0a7ad-108">Een verbinding met Azure is gemaakt met behulp van de `az login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="0a7ad-109">De code van de toepassing is in een openbare of particuliere GitHub-opslagplaats waarvan u eigenaar.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="0a7ad-110">U hebt [een toegangstoken gemaakt in uw GitHub-account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="0a7ad-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="0a7ad-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0a7ad-111">Sample script</span></span>

<span data-ttu-id="0a7ad-112">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "een WebApp maken met continue implementatie van GitHub")]</span><span class="sxs-lookup"><span data-stu-id="0a7ad-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0a7ad-113">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="0a7ad-113">Clean up deployment</span></span> 

<span data-ttu-id="0a7ad-114">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="0a7ad-115">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0a7ad-115">Script explanation</span></span>

<span data-ttu-id="0a7ad-116">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-116">This script uses the following commands.</span></span> <span data-ttu-id="0a7ad-117">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0a7ad-118">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0a7ad-118">Command</span></span> | <span data-ttu-id="0a7ad-119">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0a7ad-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0a7ad-120">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0a7ad-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0a7ad-121">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0a7ad-122">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0a7ad-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="0a7ad-123">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0a7ad-124">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0a7ad-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="0a7ad-125">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-125">Creates a web app.</span></span> |
| [<span data-ttu-id="0a7ad-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="0a7ad-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="0a7ad-127">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0a7ad-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0a7ad-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a7ad-128">Next steps</span></span>

<span data-ttu-id="0a7ad-129">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a7ad-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0a7ad-130">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0a7ad-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
