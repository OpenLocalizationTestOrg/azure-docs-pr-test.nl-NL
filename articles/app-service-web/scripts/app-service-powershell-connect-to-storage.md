---
title: aaaAzure PowerShell-voorbeeldscript - verbinding maken met een web-app tooa storage-account | Microsoft Docs
description: Azure PowerShell-Script steekproef - verbinding maken met een web-app tooa storage-account
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
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="6078b-103">Verbinding maken met een web-app tooa storage-account</span><span class="sxs-lookup"><span data-stu-id="6078b-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="6078b-104">In dit scenario leert u hoe toocreate Azure storage-account en een Azure web-app.</span><span class="sxs-lookup"><span data-stu-id="6078b-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="6078b-105">Vervolgens koppelt u Hallo storage account toohello web-app met app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="6078b-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="6078b-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="6078b-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6078b-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="6078b-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6078b-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="6078b-108">Clean up deployment</span></span> 

<span data-ttu-id="6078b-109">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="6078b-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6078b-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="6078b-110">Script explanation</span></span>

<span data-ttu-id="6078b-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="6078b-111">This script uses hello following commands.</span></span> <span data-ttu-id="6078b-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="6078b-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6078b-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6078b-113">Command</span></span> | <span data-ttu-id="6078b-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6078b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6078b-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6078b-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6078b-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6078b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6078b-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6078b-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6078b-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6078b-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6078b-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6078b-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6078b-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="6078b-120">Creates a web app.</span></span> |
| [<span data-ttu-id="6078b-121">Nieuwe AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="6078b-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="6078b-122">Maakt een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6078b-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="6078b-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="6078b-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="6078b-124">Hiermee haalt u Hallo toegangstoetsen voor een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="6078b-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="6078b-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6078b-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="6078b-126">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6078b-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6078b-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6078b-127">Next steps</span></span>

<span data-ttu-id="6078b-128">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6078b-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6078b-129">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6078b-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
