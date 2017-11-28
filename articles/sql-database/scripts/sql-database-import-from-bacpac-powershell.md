---
title: PowerShell-voorbeeld-import-Bacpac-bestand Azure SQL-database | Microsoft Docs
description: Azure PowerShell-voorbeeldscript om te importeren een Bacpac-tegel in een SQL-database
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 20e1d4c195314d6e828e1dac6afae8be11805b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="dc740-103">PowerShell gebruiken voor een Bacpac-bestand importeren in een Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="dc740-103">Use PowerShell to import a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="dc740-104">Voorbeeld van deze PowerShell-script importeert u een database van een **bacpac** -bestand in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dc740-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="dc740-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="dc740-105">Sample script</span></span>

<span data-ttu-id="dc740-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "SQL-Database maken")]</span><span class="sxs-lookup"><span data-stu-id="dc740-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="dc740-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="dc740-107">Clean up deployment</span></span>

<span data-ttu-id="dc740-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="dc740-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="dc740-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="dc740-109">Script explanation</span></span>

<span data-ttu-id="dc740-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="dc740-110">This script uses the following commands.</span></span> <span data-ttu-id="dc740-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="dc740-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dc740-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="dc740-112">Command</span></span> | <span data-ttu-id="dc740-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dc740-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dc740-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dc740-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dc740-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="dc740-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dc740-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="dc740-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="dc740-117">Maakt een logische server die als host fungeert voor de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="dc740-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="dc740-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="dc740-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="dc740-119">Maakt een firewallregel voor toegang tot alle SQL-Databases op de server van het opgegeven IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="dc740-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="dc740-120">Nieuwe AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="dc740-120">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="dc740-121">De invoer een Bacpac-bestand en een nieuwe database maken op de server.</span><span class="sxs-lookup"><span data-stu-id="dc740-121">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="dc740-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dc740-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="dc740-123">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="dc740-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dc740-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc740-124">Next steps</span></span>

<span data-ttu-id="dc740-125">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dc740-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="dc740-126">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dc740-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
