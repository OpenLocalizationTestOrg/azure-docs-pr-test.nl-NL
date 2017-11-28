---
title: aaaAzure PowerShell-voorbeeldscript - Bind een aangepaste SSL-certificaat tooa web-app | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Bind een aangepaste SSL-certificaat tooa web-app
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
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="5d910-103">Binden van een aangepaste SSL-certificaat tooa web-app</span><span class="sxs-lookup"><span data-stu-id="5d910-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="5d910-104">Dit voorbeeldscript wordt gemaakt van een web-app in App Service met de bijbehorende resources en vervolgens Hallo SSL-certificaat van een aangepast domein naam tooit wordt gebonden.</span><span class="sxs-lookup"><span data-stu-id="5d910-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="5d910-105">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d910-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="5d910-106">Controleer ook of:</span><span class="sxs-lookup"><span data-stu-id="5d910-106">Also, ensure that:</span></span>

- <span data-ttu-id="5d910-107">Een verbinding met Azure is gemaakt met behulp van Hallo `az login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5d910-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="5d910-108">U hebt toegang tot tooyour domeinregistrar van DNS-configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="5d910-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="5d910-109">U hebt een geldig. PFX-bestand en het bijbehorende wachtwoord voor Hallo SSL-certificaat u wilt dat tooupload en een binding.</span><span class="sxs-lookup"><span data-stu-id="5d910-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5d910-110">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="5d910-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5d910-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="5d910-111">Clean up deployment</span></span> 

<span data-ttu-id="5d910-112">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="5d910-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="5d910-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="5d910-113">Script explanation</span></span>

<span data-ttu-id="5d910-114">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="5d910-114">This script uses hello following commands.</span></span> <span data-ttu-id="5d910-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="5d910-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5d910-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="5d910-116">Command</span></span> | <span data-ttu-id="5d910-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5d910-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d910-118">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d910-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5d910-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5d910-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5d910-120">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5d910-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5d910-121">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5d910-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5d910-122">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5d910-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5d910-123">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="5d910-123">Creates a web app.</span></span> |
| [<span data-ttu-id="5d910-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5d910-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="5d910-125">Hiermee wijzigt u een App Service plan toochange de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="5d910-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="5d910-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5d910-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="5d910-127">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5d910-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="5d910-128">Nieuwe AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="5d910-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="5d910-129">Hiermee maakt u een SSL-certificaat-binding voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="5d910-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d910-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d910-130">Next steps</span></span>

<span data-ttu-id="5d910-131">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d910-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5d910-132">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5d910-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
