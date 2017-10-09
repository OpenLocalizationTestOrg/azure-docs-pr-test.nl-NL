---
title: PowerShell-voorbeeldscript - aaaAzure een web-app handmatig schalen | Microsoft Docs
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
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="a98a1-103">Een web-app handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="a98a1-103">Scale a web app manually</span></span>

<span data-ttu-id="a98a1-104">In dit scenario leert u een resourcegroep toocreate app service-plan en web-app.</span><span class="sxs-lookup"><span data-stu-id="a98a1-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="a98a1-105">U wordt vervolgens Hallo App Service-Plan van een enkele instantie toomultiple exemplaren te schalen.</span><span class="sxs-lookup"><span data-stu-id="a98a1-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="a98a1-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="a98a1-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a98a1-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a98a1-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a98a1-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a98a1-108">Clean up deployment</span></span> 

<span data-ttu-id="a98a1-109">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="a98a1-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a98a1-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a98a1-110">Script explanation</span></span>

<span data-ttu-id="a98a1-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a98a1-111">This script uses hello following commands.</span></span> <span data-ttu-id="a98a1-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a98a1-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a98a1-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a98a1-113">Command</span></span> | <span data-ttu-id="a98a1-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a98a1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a98a1-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a98a1-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a98a1-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a98a1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a98a1-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a98a1-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a98a1-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a98a1-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a98a1-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a98a1-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a98a1-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="a98a1-120">Creates a web app.</span></span> |
| [<span data-ttu-id="a98a1-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a98a1-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="a98a1-122">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a98a1-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a98a1-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a98a1-123">Next steps</span></span>

<span data-ttu-id="a98a1-124">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a98a1-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a98a1-125">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a98a1-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
