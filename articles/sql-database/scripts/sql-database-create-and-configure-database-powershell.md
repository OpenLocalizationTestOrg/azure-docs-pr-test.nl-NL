---
title: aaaPowerShell voorbeeld-Maak een Azure SQL database | Microsoft Docs
description: Azure PowerShell-voorbeeld script toocreate een Azure SQL-database
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="f72a3-103">Gebruik PowerShell toocreate één Azure SQL database en een firewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="f72a3-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="f72a3-104">Voorbeeld van deze PowerShell-script maakt een Azure SQL database en configureert u een firewallregel op serverniveau.</span><span class="sxs-lookup"><span data-stu-id="f72a3-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="f72a3-105">Zodra het Hallo-script is uitgevoerd, Hallo die SQL-Database toegankelijk is vanaf alle Azure-services en Hallo geconfigureerd IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f72a3-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="f72a3-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f72a3-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f72a3-107">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="f72a3-107">Clean up deployment</span></span>

<span data-ttu-id="f72a3-108">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f72a3-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="f72a3-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f72a3-109">Script explanation</span></span>

<span data-ttu-id="f72a3-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="f72a3-110">This script uses hello following commands.</span></span> <span data-ttu-id="f72a3-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="f72a3-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f72a3-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f72a3-112">Command</span></span> | <span data-ttu-id="f72a3-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f72a3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f72a3-114">Nieuwe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f72a3-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f72a3-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f72a3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f72a3-116">Nieuwe AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="f72a3-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f72a3-117">Maakt een logische server die als host fungeert voor een database of elastische pool.</span><span class="sxs-lookup"><span data-stu-id="f72a3-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f72a3-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="f72a3-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="f72a3-119">Maakt een firewall regel tooallow toegang tooall SQL-Databases op Hallo-server uit Hallo opgegeven IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="f72a3-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="f72a3-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f72a3-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="f72a3-121">Maakt een database in een logische server als één of een gegroepeerde database.</span><span class="sxs-lookup"><span data-stu-id="f72a3-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f72a3-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f72a3-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f72a3-123">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="f72a3-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="f72a3-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f72a3-124">Next steps</span></span>

<span data-ttu-id="f72a3-125">Zie voor meer informatie over hello Azure PowerShell [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f72a3-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f72a3-126">Voorbeelden van aanvullende SQL Database PowerShell-script kunnen worden gevonden in Hallo [Azure SQL Database PowerShell-scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f72a3-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



