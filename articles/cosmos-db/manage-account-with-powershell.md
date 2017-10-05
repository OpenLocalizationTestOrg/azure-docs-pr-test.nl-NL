---
title: Azure Cosmos DB Automation - beheer met Powershell | Microsoft Docs
description: Gebruik Azure Powershell beheren uw Azure DB die Cosmos-accounts.
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 25c543528119410dff0684845a713dcb0d6151d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="2633e-103">Een Azure DB die Cosmos-account maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="2633e-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="2633e-104">De volgende handleiding beschrijft automatiseren beheer van uw Azure Cosmos DB database accounts met Azure Powershell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2633e-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="2633e-105">Dit omvat ook opdrachten voor het beheren van sleutels en failover prioriteiten in [meerdere landen/regio database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="2633e-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="2633e-106">Bijwerken van uw databaseaccount, kunt u consistentie beleid wijzigen en regio's toevoegen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2633e-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="2633e-107">Voor het beheer van de platformoverschrijdende van uw Azure DB die Cosmos-account, kunt u een gebruiken [Azure CLI](cli-samples.md), wordt de [Resource Provider REST-API][rp-rest-api], of de [Azure-portal ](create-documentdb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="2633e-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="2633e-108">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="2633e-108">Getting Started</span></span>

<span data-ttu-id="2633e-109">Volg de instructies in [installeren en configureren van Azure PowerShell] [ powershell-install-configure] installeren en aanmelden bij uw Azure Resource Manager-account in Powershell.</span><span class="sxs-lookup"><span data-stu-id="2633e-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="2633e-110">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2633e-110">Notes</span></span>

* <span data-ttu-id="2633e-111">Als u wilt de volgende opdrachten worden uitgevoerd zonder gebruikersbevestiging, toevoeg-de `-Force` vlag aan de opdracht.</span><span class="sxs-lookup"><span data-stu-id="2633e-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="2633e-112">De volgende opdrachten worden synchroon.</span><span class="sxs-lookup"><span data-stu-id="2633e-112">All the following commands are synchronous.</span></span>

## <span data-ttu-id="2633e-113"><a id="create-documentdb-account-powershell"></a>Een Azure Cosmos DB-Account maken</span><span class="sxs-lookup"><span data-stu-id="2633e-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="2633e-114">Met deze opdracht kunt u een Azure DB die Cosmos-databaseaccount maken.</span><span class="sxs-lookup"><span data-stu-id="2633e-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="2633e-115">Uw nieuwe databaseaccount configureren als een regio of [meerdere landen/regio] [ scaling-globally] met een bepaald [consistentie beleid](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2633e-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="2633e-116">`<write-region-location>`De locatienaam van de regio van het schrijven van het account van de database.</span><span class="sxs-lookup"><span data-stu-id="2633e-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="2633e-117">Deze locatie is vereist voor een failover-prioriteitswaarde van 0 hebben.</span><span class="sxs-lookup"><span data-stu-id="2633e-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="2633e-118">Er moet exact één schrijven regio per databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="2633e-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="2633e-119">`<read-region-location>`De locatienaam van de gelezen regio van het account van de database.</span><span class="sxs-lookup"><span data-stu-id="2633e-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="2633e-120">Deze locatie is vereist voor failover-prioriteit waarde groter dan 0.</span><span class="sxs-lookup"><span data-stu-id="2633e-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="2633e-121">Er zijn meer dan één lezen regio's per database-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="2633e-122">`<ip-range-filter>`Hiermee geeft u het IP-adressen of IP-adresbereiken in CIDR-vorm moet worden opgenomen als de lijst met toegestane van client-IP-adressen voor een bepaalde database-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="2633e-123">IP-adressen of-adresbereiken moet door komma's gescheiden en mag geen spaties bevatten.</span><span class="sxs-lookup"><span data-stu-id="2633e-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="2633e-124">Zie voor meer informatie [Azure Cosmos DB-Firewallondersteuning](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="2633e-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="2633e-125">`<default-consistency-level>`De consistentiecontrole standaardniveau van de Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="2633e-126">Zie voor meer informatie [Consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2633e-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="2633e-127">`<max-interval>`Bij gebruik met consistentie voor gebonden veroudering is vertegenwoordigt deze waarde de tijd hoeveelheid veroudering (in seconden) toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2633e-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="2633e-128">Geaccepteerde bereik voor deze waarde is 1-100.</span><span class="sxs-lookup"><span data-stu-id="2633e-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="2633e-129">`<max-staleness-prefix>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde aan het aantal verlopen aanvragen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2633e-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="2633e-130">Geaccepteerde bereik voor deze waarde is 1 – 2.147.483.647.</span><span class="sxs-lookup"><span data-stu-id="2633e-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="2633e-131">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-132">`<resource-group-location>`De locatie van de Azure-resourcegroep waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-133">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2633e-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="2633e-134">Het kan alleen kleine letters, cijfers, gebruiken de '-' bevatten, en moet tussen 3 en 50 tekens.</span><span class="sxs-lookup"><span data-stu-id="2633e-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="2633e-135">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="2633e-136">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2633e-136">Notes</span></span>
* <span data-ttu-id="2633e-137">Het vorige voorbeeld maakt een databaseaccount met twee regio's.</span><span class="sxs-lookup"><span data-stu-id="2633e-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="2633e-138">Het is ook mogelijk te maken van een databaseaccount met één regio (die is aangewezen als de regio schrijven en een failover-prioriteitswaarde van 0 hebben) of meer dan twee regio's.</span><span class="sxs-lookup"><span data-stu-id="2633e-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="2633e-139">Zie voor meer informatie [meerdere landen/regio database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="2633e-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="2633e-140">De locaties moet gebieden waarin Azure Cosmos DB in het algemeen beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2633e-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="2633e-141">De huidige lijst met regio's is opgegeven op de [Azure-gebieden pagina](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="2633e-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="2633e-142"><a id="update-documentdb-account-powershell"></a>Een DocumentDB-databaseaccount bijwerken</span><span class="sxs-lookup"><span data-stu-id="2633e-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="2633e-143">Met deze opdracht kunt u de eigenschappen van uw Azure DB die Cosmos-database bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2633e-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="2633e-144">Dit omvat het beleid van de consistentie en de locaties waarvan de account van de database bestaat in.</span><span class="sxs-lookup"><span data-stu-id="2633e-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="2633e-145">Met deze opdracht kunt u toevoegen en verwijderen van de regio's, maar is niet toegestaan voor u failover prioriteiten wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2633e-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="2633e-146">Zie het wijzigen van failover prioriteiten [hieronder](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="2633e-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="2633e-147">`<write-region-location>`De locatienaam van de regio van het schrijven van het account van de database.</span><span class="sxs-lookup"><span data-stu-id="2633e-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="2633e-148">Deze locatie is vereist voor een failover-prioriteitswaarde van 0 hebben.</span><span class="sxs-lookup"><span data-stu-id="2633e-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="2633e-149">Er moet exact één schrijven regio per databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="2633e-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="2633e-150">`<read-region-location>`De locatienaam van de gelezen regio van het account van de database.</span><span class="sxs-lookup"><span data-stu-id="2633e-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="2633e-151">Deze locatie is vereist voor failover-prioriteit waarde groter dan 0.</span><span class="sxs-lookup"><span data-stu-id="2633e-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="2633e-152">Er zijn meer dan één lezen regio's per database-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="2633e-153">`<default-consistency-level>`De consistentiecontrole standaardniveau van de Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="2633e-154">Zie voor meer informatie [Consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2633e-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="2633e-155">`<ip-range-filter>`Hiermee geeft u het IP-adressen of IP-adresbereiken in CIDR-vorm moet worden opgenomen als de lijst met toegestane van client-IP-adressen voor een bepaalde database-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="2633e-156">IP-adressen of-adresbereiken moet door komma's gescheiden en mag geen spaties bevatten.</span><span class="sxs-lookup"><span data-stu-id="2633e-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="2633e-157">Zie voor meer informatie [Azure Cosmos DB-Firewallondersteuning](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="2633e-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="2633e-158">`<max-interval>`Bij gebruik met consistentie voor gebonden veroudering is vertegenwoordigt deze waarde de tijd hoeveelheid veroudering (in seconden) toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2633e-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="2633e-159">Geaccepteerde bereik voor deze waarde is 1-100.</span><span class="sxs-lookup"><span data-stu-id="2633e-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="2633e-160">`<max-staleness-prefix>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde aan het aantal verlopen aanvragen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2633e-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="2633e-161">Geaccepteerde bereik voor deze waarde is 1 – 2.147.483.647.</span><span class="sxs-lookup"><span data-stu-id="2633e-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="2633e-162">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-163">`<resource-group-location>`De locatie van de Azure-resourcegroep waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-164">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database moet worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="2633e-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="2633e-165">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="2633e-166"><a id="delete-documentdb-account-powershell"></a>Een DocumentDB-databaseaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="2633e-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="2633e-167">Met deze opdracht kunt u een bestaande account voor Azure DB die Cosmos-database verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2633e-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="2633e-168">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-169">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database moet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2633e-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="2633e-170">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="2633e-171"><a id="get-documentdb-properties-powershell"></a>Eigenschappen van een DocumentDB-databaseaccount opgehaald</span><span class="sxs-lookup"><span data-stu-id="2633e-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="2633e-172">Met deze opdracht kunt u de eigenschappen van een bestaande account voor Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="2633e-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="2633e-173">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-174">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="2633e-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="2633e-175">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="2633e-176"><a id="update-tags-powershell"></a>Labels van een Azure Cosmos DB databaseaccount bijwerken</span><span class="sxs-lookup"><span data-stu-id="2633e-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="2633e-177">Het volgende voorbeeld wordt beschreven hoe u [Azure resourcetags] [ azure-resource-tags] database voor uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="2633e-178">Met deze opdracht kan worden gecombineerd met de opdrachten maken of bijwerken door toe te voegen de `-Tags` markering op in de bijbehorende parameter.</span><span class="sxs-lookup"><span data-stu-id="2633e-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="2633e-179">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="2633e-180"><a id="list-account-keys-powershell"></a>Lijst met sleutels</span><span class="sxs-lookup"><span data-stu-id="2633e-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="2633e-181">Wanneer u een Azure DB die Cosmos-account maakt, genereert de service twee master toegangstoetsen die kunnen worden gebruikt voor verificatie wanneer het account voor Azure Cosmos DB wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="2633e-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="2633e-182">Dankzij twee toegangssleutels, kunt u opnieuw genereren van de sleutels zonder onderbreking naar uw Azure DB die Cosmos-account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2633e-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="2633e-183">Alleen-lezen sleutels voor het verifiëren van alleen-lezen bewerkingen zijn ook beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2633e-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="2633e-184">Er zijn twee lezen / schrijven-sleutels (primair en secundair) en twee sleutels voor alleen-lezen (primair en secundair).</span><span class="sxs-lookup"><span data-stu-id="2633e-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="2633e-185">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-186">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="2633e-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="2633e-187">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="2633e-188"><a id="list-connection-strings-powershell"></a>Lijst met verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="2633e-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="2633e-189">MongoDB-accounts, worden de verbindingsreeks naar uw MongoDB-app verbinden met het account van de database opgehaald met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="2633e-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="2633e-190">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-191">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="2633e-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="2633e-192">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="2633e-193"><a id="regenerate-account-key-powershell"></a>Accountsleutel opnieuw genereren</span><span class="sxs-lookup"><span data-stu-id="2633e-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="2633e-194">Aan uw account voor Azure Cosmos DB regelmatig om te voorkomen dat uw verbindingen beter te beveiligen, moet u de toegangssleutels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2633e-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="2633e-195">Twee toegangssleutels zijn zodat u verbindingen met de Azure DB die Cosmos-account met behulp van één toegangssleutel terwijl u de toegangssleutel opnieuw genereert onderhouden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="2633e-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="2633e-196">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-197">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="2633e-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="2633e-198">`<key-kind>`Een van de vier typen sleutels: ["Primaire" | " Secundaire "|" PrimaryReadonly "|" SecondaryReadonly'] die u wilt genereren.</span><span class="sxs-lookup"><span data-stu-id="2633e-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="2633e-199">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="2633e-200"><a id="modify-failover-priority-powershell"></a>Prioriteit van de Failover van een databaseaccount Azure Cosmos DB wijzigen</span><span class="sxs-lookup"><span data-stu-id="2633e-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="2633e-201">U kunt de prioriteit van de failover van de verschillende regio's die het account van de Azure DB die Cosmos-database bestaat in wijzigen voor meerdere landen/regio-database-accounts.</span><span class="sxs-lookup"><span data-stu-id="2633e-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="2633e-202">Zie voor meer informatie over failover in uw Azure DB die Cosmos-databaseaccount [gegevens globaal met Azure Cosmos DB distribueren][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="2633e-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="2633e-203">`<write-region-location>`De locatienaam van de regio van het schrijven van het account van de database.</span><span class="sxs-lookup"><span data-stu-id="2633e-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="2633e-204">Deze locatie is vereist voor een failover-prioriteitswaarde van 0 hebben.</span><span class="sxs-lookup"><span data-stu-id="2633e-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="2633e-205">Er moet exact één schrijven regio per databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="2633e-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="2633e-206">`<read-region-location>`De locatienaam van de gelezen regio van het account van de database.</span><span class="sxs-lookup"><span data-stu-id="2633e-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="2633e-207">Deze locatie is vereist voor failover-prioriteit waarde groter dan 0.</span><span class="sxs-lookup"><span data-stu-id="2633e-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="2633e-208">Er zijn meer dan één lezen regio's per database-account.</span><span class="sxs-lookup"><span data-stu-id="2633e-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="2633e-209">`<resource-group-name>`De naam van de [Azure-resourcegroep] [ azure-resource-groups] waartoe het account van de nieuwe Azure Cosmos DB database behoort.</span><span class="sxs-lookup"><span data-stu-id="2633e-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="2633e-210">`<database-account-name>`De naam van de account van de Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="2633e-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="2633e-211">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2633e-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="2633e-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2633e-212">Next steps</span></span>

* <span data-ttu-id="2633e-213">Als u wilt verbinding maken met .NET, Zie [Connect en query met .NET](create-documentdb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2633e-213">To connect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="2633e-214">Zie voor verbinding met behulp van .NET Core, [Connect en query met .NET Core](create-documentdb-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="2633e-214">To connect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="2633e-215">Zie voor verbinding met behulp van Node.js, [Connect en query met Node.js en een app MongoDB](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2633e-215">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
