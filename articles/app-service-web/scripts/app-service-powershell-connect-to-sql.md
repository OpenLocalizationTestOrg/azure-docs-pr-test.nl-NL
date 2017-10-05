---
title: Azure PowerShell-Script voorbeeld - web-app verbinden met een SQL database | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een WebApp verbinden met een SQL-database'
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
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="f7984-103">Een WebApp verbinden met een SQL-database</span><span class="sxs-lookup"><span data-stu-id="f7984-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="f7984-104">In dit scenario leert u hoe u een Azure SQL database en een Azure-web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="f7984-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="f7984-105">Vervolgens koppelt u de SQL-database aan de web-app met behulp van appinstellingen.</span><span class="sxs-lookup"><span data-stu-id="f7984-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="f7984-106">Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview), en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="f7984-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f7984-107">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f7984-107">Sample script</span></span>

<span data-ttu-id="f7984-108">[!code-powershell[belangrijkste](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "een WebApp verbinden met een SQL-database")]</span><span class="sxs-lookup"><span data-stu-id="f7984-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f7984-109">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="f7984-109">Clean up deployment</span></span> 

<span data-ttu-id="f7984-110">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om de resourcegroep, web-app en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f7984-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f7984-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f7984-111">Script explanation</span></span>

<span data-ttu-id="f7984-112">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="f7984-112">This script uses the following commands.</span></span> <span data-ttu-id="f7984-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="f7984-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f7984-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f7984-114">Command</span></span> | <span data-ttu-id="f7984-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f7984-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f7984-116">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f7984-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f7984-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f7984-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f7984-118">Nieuwe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f7984-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f7984-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f7984-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f7984-120">Nieuwe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f7984-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f7984-121">Hiermee maakt u een web-app.</span><span class="sxs-lookup"><span data-stu-id="f7984-121">Creates a web app.</span></span> |
| [<span data-ttu-id="f7984-122">Nieuwe AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="f7984-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f7984-123">Maakt een SQL-Database-server.</span><span class="sxs-lookup"><span data-stu-id="f7984-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="f7984-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="f7984-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="f7984-125">Maakt een firewallregel voor een SQL-Database-server.</span><span class="sxs-lookup"><span data-stu-id="f7984-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="f7984-126">Nieuwe AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="f7984-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="f7984-127">Maakt een database of een elastische database.</span><span class="sxs-lookup"><span data-stu-id="f7984-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="f7984-128">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f7984-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f7984-129">Een web-app-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f7984-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f7984-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7984-130">Next steps</span></span>

<span data-ttu-id="f7984-131">Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f7984-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f7984-132">Aanvullende voorbeelden van de Azure Powershell voor Azure App Service Web Apps kunnen worden gevonden in de [voorbeelden van Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f7984-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
