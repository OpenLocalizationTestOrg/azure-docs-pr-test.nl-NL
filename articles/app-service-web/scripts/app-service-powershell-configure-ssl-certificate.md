---
title: Azure PowerShell-Script voorbeeld - Bind een aangepaste SSL-certificaat voor een web-app | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Bind een aangepaste SSL-certificaat voor een web-app
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: de8deccadcd9571be75447a117888bf2b3f571a0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="8a4eb-103">Een aangepaste SSL-certificaat binden aan een web-app</span><span class="sxs-lookup"><span data-stu-id="8a4eb-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="8a4eb-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en vervolgens koppelt het SSL-certificaat van een aangepaste domeinnaam aan deze.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="8a4eb-105">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a4eb-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="8a4eb-106">Controleer ook of:</span><span class="sxs-lookup"><span data-stu-id="8a4eb-106">Also, ensure that:</span></span>

- <span data-ttu-id="8a4eb-107">Een verbinding met Azure is gemaakt met behulp van de `az login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="8a4eb-108">U hebt toegang tot uw domeinregistrar DNS-configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="8a4eb-109">U hebt een geldig. PFX-bestand en het bijbehorende wachtwoord voor het SSL-certificaat dat u wilt uploaden en binden.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="8a4eb-110">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="8a4eb-110">Sample script</span></span>

<span data-ttu-id="8a4eb-111">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "een aangepaste SSL-certificaat binden aan een web-app")]</span><span class="sxs-lookup"><span data-stu-id="8a4eb-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8a4eb-112">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="8a4eb-112">Clean up deployment</span></span> 

<span data-ttu-id="8a4eb-113">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="8a4eb-114">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="8a4eb-114">Script explanation</span></span>

<span data-ttu-id="8a4eb-115">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-115">This script uses the following commands.</span></span> <span data-ttu-id="8a4eb-116">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8a4eb-117">Opdracht</span><span class="sxs-lookup"><span data-stu-id="8a4eb-117">Command</span></span> | <span data-ttu-id="8a4eb-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="8a4eb-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8a4eb-119">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8a4eb-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8a4eb-120">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8a4eb-121">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8a4eb-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="8a4eb-122">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8a4eb-123">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8a4eb-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="8a4eb-124">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-124">Creates a web app.</span></span> |
| [<span data-ttu-id="8a4eb-125">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8a4eb-125">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="8a4eb-126">Hiermee wijzigt u een App Service-abonnement als de prijscategorie wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-126">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="8a4eb-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8a4eb-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="8a4eb-128">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-128">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="8a4eb-129">Nieuwe AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="8a4eb-129">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="8a4eb-130">Hiermee maakt u een SSL-certificaat-binding voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="8a4eb-130">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8a4eb-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a4eb-131">Next steps</span></span>

<span data-ttu-id="8a4eb-132">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a4eb-132">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8a4eb-133">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8a4eb-133">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
