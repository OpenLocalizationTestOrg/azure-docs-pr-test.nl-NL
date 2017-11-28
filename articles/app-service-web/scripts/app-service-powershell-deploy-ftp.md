---
title: PowerShell-voorbeeldscript - Upload bestanden tooa web-app met FTP aaaAzure | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Upload bestanden tooa web-app met FTP
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="111ad-103">Met FTP-bestanden tooa web-app uploaden</span><span class="sxs-lookup"><span data-stu-id="111ad-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="111ad-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code met FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="111ad-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="111ad-105">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="111ad-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="111ad-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="111ad-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="111ad-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="111ad-107">Clean up deployment</span></span> 

<span data-ttu-id="111ad-108">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="111ad-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="111ad-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="111ad-109">Script explanation</span></span>

<span data-ttu-id="111ad-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="111ad-110">This script uses hello following commands.</span></span> <span data-ttu-id="111ad-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="111ad-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="111ad-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="111ad-112">Command</span></span> | <span data-ttu-id="111ad-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="111ad-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="111ad-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="111ad-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="111ad-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="111ad-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="111ad-116">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="111ad-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="111ad-117">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="111ad-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="111ad-118">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="111ad-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="111ad-119">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="111ad-119">Creates a web app.</span></span> |
| [<span data-ttu-id="111ad-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="111ad-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="111ad-121">Profiel voor het publiceren van een web-app worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="111ad-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="111ad-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="111ad-122">Next steps</span></span>

<span data-ttu-id="111ad-123">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="111ad-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="111ad-124">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="111ad-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
