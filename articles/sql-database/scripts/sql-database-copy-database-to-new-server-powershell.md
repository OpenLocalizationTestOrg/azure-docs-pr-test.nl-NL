---
title: "aaaPowerShell voorbeeld-kopiëren-Azure SQL database-nieuwe server | Microsoft Docs"
description: Azure PowerShell-voorbeeld script toocopy een nieuwe server voor SQL database tooa
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
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="498ec-103">Gebruik PowerShell toocopy een nieuwe server voor SQL database tooa</span><span class="sxs-lookup"><span data-stu-id="498ec-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="498ec-104">Voorbeeld van deze PowerShell-script maakt een kopie van een bestaande database in een nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="498ec-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="498ec-105">Een nieuwe databaseserver voor tooa kopiëren</span><span class="sxs-lookup"><span data-stu-id="498ec-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="498ec-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="498ec-106">Clean up deployment</span></span>

<span data-ttu-id="498ec-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="498ec-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="498ec-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="498ec-108">Script explanation</span></span>

<span data-ttu-id="498ec-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="498ec-109">This script uses hello following commands.</span></span> <span data-ttu-id="498ec-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="498ec-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="498ec-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="498ec-111">Command</span></span> | <span data-ttu-id="498ec-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="498ec-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="498ec-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="498ec-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="498ec-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="498ec-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="498ec-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="498ec-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="498ec-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="498ec-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="498ec-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="498ec-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="498ec-118">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="498ec-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="498ec-119">Nieuwe AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="498ec-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="498ec-120">Maakt een kopie van een database die Hallo momentopname gebruikmaakt op Hallo van huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="498ec-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="498ec-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="498ec-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="498ec-122">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="498ec-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="498ec-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="498ec-123">Next steps</span></span>

<span data-ttu-id="498ec-124">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="498ec-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="498ec-125">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="498ec-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
