---
title: Azure PowerShell-Script voorbeeld - bestanden uploaden naar een web-app met FTP | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - bestanden uploaden naar een web-app met FTP
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
ms.openlocfilehash: 96b99110b63b037746fcc40eb15db5d718eb71a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="7c32a-103">Bestanden uploaden naar een web-app met FTP</span><span class="sxs-lookup"><span data-stu-id="7c32a-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="7c32a-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code met FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="7c32a-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="7c32a-105">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="7c32a-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7c32a-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="7c32a-106">Sample script</span></span>

<span data-ttu-id="7c32a-107">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "bestanden uploaden naar een web-app met FTP")]</span><span class="sxs-lookup"><span data-stu-id="7c32a-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7c32a-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="7c32a-108">Clean up deployment</span></span> 

<span data-ttu-id="7c32a-109">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7c32a-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7c32a-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="7c32a-110">Script explanation</span></span>

<span data-ttu-id="7c32a-111">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7c32a-111">This script uses the following commands.</span></span> <span data-ttu-id="7c32a-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="7c32a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7c32a-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="7c32a-113">Command</span></span> | <span data-ttu-id="7c32a-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7c32a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c32a-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c32a-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7c32a-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7c32a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c32a-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7c32a-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7c32a-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7c32a-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7c32a-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7c32a-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7c32a-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="7c32a-120">Creates a web app.</span></span> |
| [<span data-ttu-id="7c32a-121">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="7c32a-121">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="7c32a-122">Profiel voor het publiceren van een web-app worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7c32a-122">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c32a-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7c32a-123">Next steps</span></span>

<span data-ttu-id="7c32a-124">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c32a-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7c32a-125">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c32a-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
