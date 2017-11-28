---
title: PowerShell-voorbeeldscript - aaaAzure toewijzen een aangepast domein tooa web-app | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - toewijzen een aangepast domein tooa web-app
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="9d05c-103">Toewijzen van een aangepast domein tooa web-app</span><span class="sxs-lookup"><span data-stu-id="9d05c-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="9d05c-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en wijst vervolgens `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="9d05c-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="9d05c-105">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="9d05c-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="9d05c-106">Bovendien moet u de pagina toohave toegang tooyour domeinregistrar van DNS-configuratie.</span><span class="sxs-lookup"><span data-stu-id="9d05c-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="9d05c-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9d05c-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9d05c-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="9d05c-108">Clean up deployment</span></span> 

<span data-ttu-id="9d05c-109">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="9d05c-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="9d05c-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9d05c-110">Script explanation</span></span>

<span data-ttu-id="9d05c-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="9d05c-111">This script uses hello following commands.</span></span> <span data-ttu-id="9d05c-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9d05c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9d05c-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9d05c-113">Command</span></span> | <span data-ttu-id="9d05c-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9d05c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d05c-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9d05c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9d05c-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9d05c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9d05c-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="9d05c-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="9d05c-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9d05c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9d05c-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9d05c-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="9d05c-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="9d05c-120">Creates a web app.</span></span> |
| [<span data-ttu-id="9d05c-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="9d05c-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="9d05c-122">Hiermee wijzigt u een App Service plan toochange de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="9d05c-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="9d05c-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9d05c-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="9d05c-124">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9d05c-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d05c-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d05c-125">Next steps</span></span>

<span data-ttu-id="9d05c-126">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d05c-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9d05c-127">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9d05c-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
