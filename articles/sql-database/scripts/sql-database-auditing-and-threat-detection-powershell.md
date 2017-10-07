---
title: aaaPowerShell voorbeeld-controle threat detectie-Azure SQL Database | Microsoft Docs
description: Azure PowerShell voorbeeld script tooconfigure controle en detectie van bedreigingen in een Azure SQL Database
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="5024c-103">Gebruik PowerShell tooconfigure SQL-Database controle en detectie van bedreigingen</span><span class="sxs-lookup"><span data-stu-id="5024c-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="5024c-104">Voorbeeld van deze PowerShell-script configureert SQL-Database controle en detectie van bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="5024c-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="5024c-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="5024c-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5024c-106">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="5024c-106">Clean up deployment</span></span>

<span data-ttu-id="5024c-107">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5024c-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5024c-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="5024c-108">Script explanation</span></span>

<span data-ttu-id="5024c-109">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="5024c-109">This script uses hello following commands.</span></span> <span data-ttu-id="5024c-110">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="5024c-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5024c-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="5024c-111">Command</span></span> | <span data-ttu-id="5024c-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5024c-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5024c-113">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5024c-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5024c-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5024c-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5024c-115">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="5024c-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="5024c-116">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="5024c-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5024c-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5024c-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="5024c-118">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="5024c-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="5024c-119">Nieuwe AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="5024c-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="5024c-120">Maakt een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5024c-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="5024c-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="5024c-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="5024c-122">Hiermee stelt u Hallo controlebeleid voor een database.</span><span class="sxs-lookup"><span data-stu-id="5024c-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="5024c-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="5024c-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="5024c-124">Hiermee stelt u een bedreiging detectie-beleid voor een database.</span><span class="sxs-lookup"><span data-stu-id="5024c-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="5024c-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5024c-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5024c-126">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="5024c-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5024c-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5024c-127">Next steps</span></span>

<span data-ttu-id="5024c-128">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5024c-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5024c-129">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5024c-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
