---
title: aaaAzure PowerShell-voorbeeldscript - routeverkeer voor hoge beschikbaarheid van toepassingen | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - routeverkeer voor hoge beschikbaarheid van toepassingen
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="f102f-103">Verkeer leiden voor hoge beschikbaarheid van toepassingen</span><span class="sxs-lookup"><span data-stu-id="f102f-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="f102f-104">Dit script maakt een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="f102f-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="f102f-105">Traffic Manager stuurt verkeer toohello toepassing in één regio bevinden als de primaire regio Hallo en de secundaire regio toohello wanneer Hallo-toepassing in Hallo primaire regio niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="f102f-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="f102f-106">Voordat u Hallo script wordt uitgevoerd, moet u Hallo MyWebApp, MyWebAppL1 en MyWebAppL2 waarden toounique waarden in Azure.</span><span class="sxs-lookup"><span data-stu-id="f102f-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="f102f-107">Na het uitvoeren van script hello, kunt u in de primaire regio Hallo met Hallo URL mywebapp.trafficmanager.net Hallo app openen.</span><span class="sxs-lookup"><span data-stu-id="f102f-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="f102f-108">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="f102f-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f102f-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f102f-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="f102f-110">Hallo na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f102f-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="f102f-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f102f-111">Script explanation</span></span>

<span data-ttu-id="f102f-112">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep, web-app, traffic manager-profiel te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="f102f-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="f102f-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="f102f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f102f-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f102f-114">Command</span></span> | <span data-ttu-id="f102f-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f102f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f102f-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f102f-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="f102f-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f102f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f102f-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f102f-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f102f-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f102f-119">Creates an App Service plan.</span></span> <span data-ttu-id="f102f-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="f102f-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="f102f-121">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f102f-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f102f-122">Hiermee maakt u een Azure-web-app in het Hallo-App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f102f-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="f102f-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f102f-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="f102f-124">Hiermee maakt u een Azure-web-app in het Hallo-App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f102f-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="f102f-125">Nieuwe AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="f102f-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="f102f-126">Een Azure Traffic Manager-profiel maakt.</span><span class="sxs-lookup"><span data-stu-id="f102f-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="f102f-127">Nieuwe AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="f102f-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="f102f-128">Voegt een eindpunt tooan Azure Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="f102f-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f102f-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f102f-129">Next steps</span></span>

<span data-ttu-id="f102f-130">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f102f-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="f102f-131">Aanvullende voorbeelden voor netwerken PowerShell-script kunnen worden gevonden in Hallo [overzicht van Azure-netwerken documentatie](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f102f-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
