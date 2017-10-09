---
title: PowerShell-voorbeeldscript - aaaAzure schalen een web-app wereldwijd een hoge beschikbaarheid-architectuur | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - schaal een web-app wereldwijd een hoge beschikbaarheid-architectuur
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="2b22f-103">Schalen van een web-app wereldwijd een hoge beschikbaarheid-architectuur</span><span class="sxs-lookup"><span data-stu-id="2b22f-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="2b22f-104">In dit scenario maakt u een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="2b22f-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="2b22f-105">Zodra de Hallo oefening is voltooid hebt u een hoog beschikbare architectuur waarmee biedt globale beschikbaarheid van uw web-app op basis van de laagste netwerklatentie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b22f-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="2b22f-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="2b22f-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2b22f-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="2b22f-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2b22f-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2b22f-108">Clean up deployment</span></span> 

<span data-ttu-id="2b22f-109">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="2b22f-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="2b22f-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2b22f-110">Script explanation</span></span>

<span data-ttu-id="2b22f-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="2b22f-111">This script uses hello following commands.</span></span> <span data-ttu-id="2b22f-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="2b22f-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2b22f-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2b22f-113">Command</span></span> | <span data-ttu-id="2b22f-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2b22f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b22f-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2b22f-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2b22f-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2b22f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2b22f-117">Nieuwe AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="2b22f-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="2b22f-118">Maakt een Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="2b22f-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="2b22f-119">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="2b22f-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="2b22f-120">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2b22f-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2b22f-121">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2b22f-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="2b22f-122">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="2b22f-122">Creates a web app.</span></span> |
| [<span data-ttu-id="2b22f-123">Nieuwe AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="2b22f-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="2b22f-124">Maakt een eindpunt in een Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="2b22f-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b22f-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b22f-125">Next steps</span></span>

<span data-ttu-id="2b22f-126">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2b22f-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2b22f-127">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2b22f-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
