---
title: aaaPowerShell voorbeeld-import-Bacpac-bestand-Azure SQL database | Microsoft Docs
description: Azure PowerShell-voorbeeld script tooimport een bacpac-tegel in een SQL-database
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="0c582-103">Gebruik PowerShell tooimport een Bacpac-bestand in een Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="0c582-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="0c582-104">Voorbeeld van deze PowerShell-script importeert u een database van een **bacpac** -bestand in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0c582-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="0c582-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0c582-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0c582-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="0c582-106">Clean up deployment</span></span>

<span data-ttu-id="0c582-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="0c582-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0c582-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0c582-108">Script explanation</span></span>

<span data-ttu-id="0c582-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="0c582-109">This script uses hello following commands.</span></span> <span data-ttu-id="0c582-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="0c582-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0c582-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0c582-111">Command</span></span> | <span data-ttu-id="0c582-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0c582-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0c582-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0c582-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0c582-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0c582-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0c582-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="0c582-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0c582-116">Maakt een logische server dat hosts Hallo SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="0c582-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="0c582-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="0c582-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="0c582-118">Maakt een firewall regel tooallow toegang tooall SQL-Databases op Hallo-server uit Hallo opgegeven IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="0c582-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="0c582-119">Nieuwe AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="0c582-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="0c582-120">De invoer een Bacpac-bestand en een nieuwe database maken op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="0c582-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="0c582-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0c582-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0c582-122">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="0c582-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0c582-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c582-123">Next steps</span></span>

<span data-ttu-id="0c582-124">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0c582-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0c582-125">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0c582-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
