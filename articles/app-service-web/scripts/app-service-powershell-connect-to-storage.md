---
title: 'Azure PowerShell-Script voorbeeld: een WebApp verbinden met een opslagaccount | Microsoft Docs'
description: 'Azure PowerShell-Script voorbeeld: een WebApp verbinden met een opslagaccount'
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="f5f3b-103">Een WebApp verbinden met een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="f5f3b-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="f5f3b-104">In dit scenario leert u hoe u een Azure storage-account en een Azure-web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="f5f3b-105">Vervolgens koppelt u het storage-account aan de web-app met behulp van appinstellingen.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="f5f3b-106">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f5f3b-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f5f3b-107">Sample script</span></span>

<span data-ttu-id="f5f3b-108">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "een WebApp verbinden met een opslagaccount")]</span><span class="sxs-lookup"><span data-stu-id="f5f3b-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f5f3b-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="f5f3b-109">Clean up deployment</span></span> 

<span data-ttu-id="f5f3b-110">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f5f3b-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f5f3b-111">Script explanation</span></span>

<span data-ttu-id="f5f3b-112">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-112">This script uses the following commands.</span></span> <span data-ttu-id="f5f3b-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f5f3b-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f5f3b-114">Command</span></span> | <span data-ttu-id="f5f3b-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f5f3b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f5f3b-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f5f3b-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f5f3b-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f5f3b-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f5f3b-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f5f3b-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f5f3b-120">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f5f3b-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f5f3b-121">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-121">Creates a web app.</span></span> |
| [<span data-ttu-id="f5f3b-122">Nieuwe AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="f5f3b-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="f5f3b-123">Maakt een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="f5f3b-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="f5f3b-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="f5f3b-125">Hiermee haalt u de toegangssleutels voor een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="f5f3b-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f5f3b-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f5f3b-127">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f5f3b-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f5f3b-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5f3b-128">Next steps</span></span>

<span data-ttu-id="f5f3b-129">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5f3b-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f5f3b-130">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f5f3b-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
