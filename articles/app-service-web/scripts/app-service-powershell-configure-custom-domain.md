---
title: Azure PowerShell-Script voorbeeld - toewijzen een aangepast domein in een web-app | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - toewijzen een aangepast domein in een web-app
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
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="3cce7-103">Een aangepast domein toewijzen aan een web-app</span><span class="sxs-lookup"><span data-stu-id="3cce7-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="3cce7-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en wijst vervolgens `www.<yourdomain>` aan.</span><span class="sxs-lookup"><span data-stu-id="3cce7-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="3cce7-105">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="3cce7-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="3cce7-106">U moet ook toegang hebben tot uw domeinregistrar DNS-configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="3cce7-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3cce7-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="3cce7-107">Sample script</span></span>

<span data-ttu-id="3cce7-108">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "een aangepast domein toewijzen aan een web-app")]</span><span class="sxs-lookup"><span data-stu-id="3cce7-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3cce7-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="3cce7-109">Clean up deployment</span></span> 

<span data-ttu-id="3cce7-110">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3cce7-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3cce7-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="3cce7-111">Script explanation</span></span>

<span data-ttu-id="3cce7-112">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="3cce7-112">This script uses the following commands.</span></span> <span data-ttu-id="3cce7-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="3cce7-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3cce7-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="3cce7-114">Command</span></span> | <span data-ttu-id="3cce7-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3cce7-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3cce7-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3cce7-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3cce7-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3cce7-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3cce7-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3cce7-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3cce7-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3cce7-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3cce7-120">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3cce7-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3cce7-121">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="3cce7-121">Creates a web app.</span></span> |
| [<span data-ttu-id="3cce7-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3cce7-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="3cce7-123">Hiermee wijzigt u een App Service-abonnement als de prijscategorie wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3cce7-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="3cce7-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3cce7-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="3cce7-125">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3cce7-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3cce7-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cce7-126">Next steps</span></span>

<span data-ttu-id="3cce7-127">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3cce7-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3cce7-128">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3cce7-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
