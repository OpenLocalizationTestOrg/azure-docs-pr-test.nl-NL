---
title: PowerShell voorbeeld-controle threat detectie-Azure SQL Database | Microsoft Docs
description: Azure PowerShell-voorbeeldscript voor het configureren van controle en detectie van bedreigingen in een Azure SQL Database
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
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="4ec2e-103">PowerShell gebruiken voor het configureren van SQL Database auditing en detectie van bedreigingen</span><span class="sxs-lookup"><span data-stu-id="4ec2e-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="4ec2e-104">Voorbeeld van deze PowerShell-script configureert SQL-Database controle en detectie van bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="4ec2e-105">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4ec2e-105">Sample script</span></span>

<span data-ttu-id="4ec2e-106">[!code-powershell[belangrijkste](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "controle en detectie van bedreigingen configureren")]</span><span class="sxs-lookup"><span data-stu-id="4ec2e-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4ec2e-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="4ec2e-107">Clean up deployment</span></span>

<span data-ttu-id="4ec2e-108">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="4ec2e-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4ec2e-109">Script explanation</span></span>

<span data-ttu-id="4ec2e-110">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-110">This script uses the following commands.</span></span> <span data-ttu-id="4ec2e-111">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4ec2e-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4ec2e-112">Command</span></span> | <span data-ttu-id="4ec2e-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4ec2e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4ec2e-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4ec2e-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4ec2e-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4ec2e-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="4ec2e-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="4ec2e-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="4ec2e-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="4ec2e-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="4ec2e-119">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="4ec2e-120">Nieuwe AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="4ec2e-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="4ec2e-121">Maakt een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="4ec2e-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="4ec2e-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="4ec2e-123">Hiermee stelt u het controlebeleid voor een database.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="4ec2e-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="4ec2e-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="4ec2e-125">Hiermee stelt u een bedreiging detectie-beleid voor een database.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="4ec2e-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4ec2e-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4ec2e-127">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="4ec2e-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ec2e-128">Next steps</span></span>

<span data-ttu-id="4ec2e-129">Zie voor meer informatie over Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4ec2e-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4ec2e-130">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in de [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4ec2e-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
