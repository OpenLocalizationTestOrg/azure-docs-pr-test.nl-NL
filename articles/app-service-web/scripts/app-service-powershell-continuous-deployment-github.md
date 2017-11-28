---
title: PowerShell-voorbeeldscript - aaaAzure een web-app maken met continue implementatie van GitHub | Microsoft Docs
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
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="c9451-103">Een WebApp maken met continue implementatie van GitHub</span><span class="sxs-lookup"><span data-stu-id="c9451-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="c9451-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en vervolgens stelt continue implementatie van een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="c9451-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="c9451-105">Zie voor de implementatie van GitHub zonder continue implementatie [een web-app maken en implementeren van code vanuit GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="c9451-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="c9451-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9451-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="c9451-107">Controleer ook of:</span><span class="sxs-lookup"><span data-stu-id="c9451-107">Also, ensure that:</span></span>

- <span data-ttu-id="c9451-108">Een verbinding met Azure is gemaakt met behulp van Hallo `az login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c9451-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="c9451-109">Hallo-toepassingscode is in een openbare of particuliere GitHub-opslagplaats waarvan u eigenaar.</span><span class="sxs-lookup"><span data-stu-id="c9451-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="c9451-110">U hebt [een toegangstoken gemaakt in uw GitHub-account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="c9451-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="c9451-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c9451-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c9451-112">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="c9451-112">Clean up deployment</span></span> 

<span data-ttu-id="c9451-113">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="c9451-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c9451-114">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c9451-114">Script explanation</span></span>

<span data-ttu-id="c9451-115">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="c9451-115">This script uses hello following commands.</span></span> <span data-ttu-id="c9451-116">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="c9451-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c9451-117">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c9451-117">Command</span></span> | <span data-ttu-id="c9451-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c9451-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9451-119">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9451-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c9451-120">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c9451-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9451-121">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c9451-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c9451-122">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9451-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c9451-123">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c9451-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c9451-124">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="c9451-124">Creates a web app.</span></span> |
| [<span data-ttu-id="c9451-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c9451-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="c9451-126">Hiermee wijzigt u een resource in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c9451-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9451-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9451-127">Next steps</span></span>

<span data-ttu-id="c9451-128">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9451-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c9451-129">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c9451-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
