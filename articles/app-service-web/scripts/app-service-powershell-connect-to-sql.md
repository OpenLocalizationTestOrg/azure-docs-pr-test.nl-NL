---
title: aaaAzure PowerShell-voorbeeldscript - verbinding maken met een web-app tooa SQL-database | Microsoft Docs
description: Azure PowerShell-Script steekproef - verbinding maken met een web-app tooa SQL-database
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="8de40-103">Verbinding maken met een web-app tooa SQL-database</span><span class="sxs-lookup"><span data-stu-id="8de40-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="8de40-104">In dit scenario leert u hoe toocreate een Azure SQL database en een Azure web-app.</span><span class="sxs-lookup"><span data-stu-id="8de40-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="8de40-105">Vervolgens koppelt u Hallo SQL database toohello web-app met app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8de40-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="8de40-106">Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="8de40-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="8de40-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="8de40-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8de40-108">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="8de40-108">Clean up deployment</span></span> 

<span data-ttu-id="8de40-109">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="8de40-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="8de40-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="8de40-110">Script explanation</span></span>

<span data-ttu-id="8de40-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="8de40-111">This script uses hello following commands.</span></span> <span data-ttu-id="8de40-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="8de40-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8de40-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="8de40-113">Command</span></span> | <span data-ttu-id="8de40-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="8de40-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8de40-115">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8de40-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8de40-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8de40-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8de40-117">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8de40-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="8de40-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8de40-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8de40-119">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8de40-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="8de40-120">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="8de40-120">Creates a web app.</span></span> |
| [<span data-ttu-id="8de40-121">Nieuwe AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="8de40-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8de40-122">Maakt een SQL-Database-server.</span><span class="sxs-lookup"><span data-stu-id="8de40-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="8de40-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="8de40-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="8de40-124">Maakt een firewallregel voor een SQL-Database-server.</span><span class="sxs-lookup"><span data-stu-id="8de40-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="8de40-125">Nieuwe AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="8de40-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="8de40-126">Maakt een database of een elastische database.</span><span class="sxs-lookup"><span data-stu-id="8de40-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="8de40-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8de40-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="8de40-128">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8de40-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8de40-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8de40-129">Next steps</span></span>

<span data-ttu-id="8de40-130">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8de40-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8de40-131">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in Hallo [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8de40-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
