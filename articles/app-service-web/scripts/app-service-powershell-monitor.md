---
title: Azure PowerShell-Script voorbeeld - Monitor voor een web-app met web server-Logboeken | Microsoft Docs
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
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="e0428-103">Een web-app met web server-logboeken bewaken</span><span class="sxs-lookup"><span data-stu-id="e0428-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="e0428-104">In dit scenario wordt u een resourcegroep, de app service-abonnement, de web-app maken en configureren van de web-app zodat web server-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="e0428-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="e0428-105">Vervolgens downloadt u de logboekbestanden voor revisie.</span><span class="sxs-lookup"><span data-stu-id="e0428-105">You will then download the log files for review.</span></span>

<span data-ttu-id="e0428-106">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="e0428-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e0428-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="e0428-107">Sample script</span></span>

<span data-ttu-id="e0428-108">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "een web-app met web server-logboeken bewaken")]</span><span class="sxs-lookup"><span data-stu-id="e0428-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e0428-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="e0428-109">Clean up deployment</span></span> 

<span data-ttu-id="e0428-110">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e0428-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e0428-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="e0428-111">Script explanation</span></span>

<span data-ttu-id="e0428-112">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="e0428-112">This script uses the following commands.</span></span> <span data-ttu-id="e0428-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="e0428-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e0428-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="e0428-114">Command</span></span> | <span data-ttu-id="e0428-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e0428-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e0428-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e0428-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e0428-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e0428-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e0428-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e0428-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="e0428-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e0428-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e0428-120">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e0428-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="e0428-121">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="e0428-121">Creates a web app.</span></span> |
| [<span data-ttu-id="e0428-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e0428-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="e0428-123">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e0428-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="e0428-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="e0428-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="e0428-125">Hiermee haalt u een web-app metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="e0428-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0428-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0428-126">Next steps</span></span>

<span data-ttu-id="e0428-127">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0428-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e0428-128">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e0428-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
