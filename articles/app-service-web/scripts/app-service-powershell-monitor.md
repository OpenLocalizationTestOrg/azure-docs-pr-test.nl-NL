---
title: PowerShell-voorbeeldscript - aaaAzure een web-app met web server-logboeken bewaken | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Monitor voor een web-app met web server-Logboeken
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="4ca2d-103">Een web-app met web server-logboeken bewaken</span><span class="sxs-lookup"><span data-stu-id="4ca2d-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="4ca2d-104">In dit scenario wordt u een resourcegroep, de app service-abonnement, de web-app maken en configureren van Hallo web app tooenable web server-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="4ca2d-105">Hallo-logboekbestanden voor revisie wordt vervolgens gedownload.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="4ca2d-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="4ca2d-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4ca2d-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4ca2d-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="4ca2d-108">Clean up deployment</span></span> 

<span data-ttu-id="4ca2d-109">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4ca2d-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4ca2d-110">Script explanation</span></span>

<span data-ttu-id="4ca2d-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-111">This script uses hello following commands.</span></span> <span data-ttu-id="4ca2d-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4ca2d-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4ca2d-113">Command</span></span> | <span data-ttu-id="4ca2d-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4ca2d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4ca2d-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4ca2d-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4ca2d-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4ca2d-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4ca2d-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4ca2d-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4ca2d-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4ca2d-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4ca2d-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-120">Creates a web app.</span></span> |
| [<span data-ttu-id="4ca2d-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4ca2d-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="4ca2d-122">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="4ca2d-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="4ca2d-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="4ca2d-124">Hiermee haalt u een web-app metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="4ca2d-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4ca2d-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ca2d-125">Next steps</span></span>

<span data-ttu-id="4ca2d-126">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4ca2d-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4ca2d-127">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4ca2d-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
