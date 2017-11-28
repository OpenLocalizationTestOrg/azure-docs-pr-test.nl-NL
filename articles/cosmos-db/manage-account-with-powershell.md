---
title: aaaAzure Cosmos DB Automation - beheer met Powershell | Microsoft Docs
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
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="dbef3-103">Een Azure DB die Cosmos-account maken met PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbef3-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="dbef3-104">Hallo beschrijft volgende handleiding opdrachten tooautomate beheer van uw Azure Cosmos DB database accounts met Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="dbef3-104">hello following guide describes commands tooautomate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="dbef3-105">Dit omvat ook opdrachten toomanage toegangscodes en failover prioriteiten in [meerdere landen/regio database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="dbef3-105">It also includes commands toomanage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="dbef3-106">Bijwerken van uw databaseaccount kunt u toomodify consistentie beleidsregels en regio's toevoegen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="dbef3-106">Updating your database account allows you toomodify consistency policies and add/remove regions.</span></span> <span data-ttu-id="dbef3-107">Voor het beheer van de platformoverschrijdende van uw Azure DB die Cosmos-account, kunt u een gebruiken [Azure CLI](cli-samples.md), Hallo [Resource Provider REST-API][rp-rest-api], of Hallo [Azure Portal](create-documentdb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="dbef3-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), hello [Resource Provider REST API][rp-rest-api], or hello [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="dbef3-108">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="dbef3-108">Getting Started</span></span>

<span data-ttu-id="dbef3-109">Volg de instructies in Hallo [hoe tooinstall en configureren van Azure PowerShell] [ powershell-install-configure] tooinstall en zich aanmelden tooyour Azure Resource Manager-account in Powershell.</span><span class="sxs-lookup"><span data-stu-id="dbef3-109">Follow hello instructions in [How tooinstall and configure Azure PowerShell][powershell-install-configure] tooinstall and log in tooyour Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="dbef3-110">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dbef3-110">Notes</span></span>

* <span data-ttu-id="dbef3-111">Als u tooexecute Hallo opdrachten te volgen wilt zonder gebruikersbevestiging, toevoeg-Hallo `-Force` toohello opdracht vlag.</span><span class="sxs-lookup"><span data-stu-id="dbef3-111">If you would like tooexecute hello following commands without requiring user confirmation, append hello `-Force` flag toohello command.</span></span>
* <span data-ttu-id="dbef3-112">Alle Hallo volgende opdrachten worden synchroon.</span><span class="sxs-lookup"><span data-stu-id="dbef3-112">All hello following commands are synchronous.</span></span>

## <span data-ttu-id="dbef3-113"><a id="create-documentdb-account-powershell"></a>Een Azure Cosmos DB-Account maken</span><span class="sxs-lookup"><span data-stu-id="dbef3-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="dbef3-114">Deze opdracht kunt u een databaseaccount Azure Cosmos DB toocreate.</span><span class="sxs-lookup"><span data-stu-id="dbef3-114">This command allows you toocreate an Azure Cosmos DB database account.</span></span> <span data-ttu-id="dbef3-115">Uw nieuwe databaseaccount configureren als een regio of [meerdere landen/regio] [ scaling-globally] met een bepaald [consistentie beleid](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dbef3-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="dbef3-116">`<write-region-location>`de locatienaam Hallo Hallo regio van het databaseaccount Hallo schrijven.</span><span class="sxs-lookup"><span data-stu-id="dbef3-116">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="dbef3-117">Deze locatie is vereist toohave een prioriteitswaarde failover van 0.</span><span class="sxs-lookup"><span data-stu-id="dbef3-117">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="dbef3-118">Er moet exact één schrijven regio per databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="dbef3-119">`<read-region-location>`de locatienaam Hallo Hallo lezen regio van het databaseaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbef3-119">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="dbef3-120">Deze locatie is vereist toohave failover prioriteitswaarde groter dan 0.</span><span class="sxs-lookup"><span data-stu-id="dbef3-120">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="dbef3-121">Er zijn meer dan één lezen regio's per database-account.</span><span class="sxs-lookup"><span data-stu-id="dbef3-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="dbef3-122">`<ip-range-filter>`Hiermee geeft u Hallo reeks IP-adressen of IP-adresbereiken in CIDR-formulier toobe Hallo toegestane lijst met client-IP-adressen voor een bepaalde database-account wordt opgenomen.</span><span class="sxs-lookup"><span data-stu-id="dbef3-122">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="dbef3-123">IP-adressen of-adresbereiken moet door komma's gescheiden en mag geen spaties bevatten.</span><span class="sxs-lookup"><span data-stu-id="dbef3-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="dbef3-124">Zie voor meer informatie [Azure Cosmos DB-Firewallondersteuning](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="dbef3-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="dbef3-125">`<default-consistency-level>`Hallo consistentie standaardniveau van hello Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="dbef3-125">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="dbef3-126">Zie voor meer informatie [Consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dbef3-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="dbef3-127">`<max-interval>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo tijd hoeveelheid veroudering (in seconden) toegestaan.</span><span class="sxs-lookup"><span data-stu-id="dbef3-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="dbef3-128">Geaccepteerde bereik voor deze waarde is 1-100.</span><span class="sxs-lookup"><span data-stu-id="dbef3-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="dbef3-129">`<max-staleness-prefix>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo aantal verlopen aanvragen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="dbef3-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="dbef3-130">Geaccepteerde bereik voor deze waarde is 1 – 2.147.483.647.</span><span class="sxs-lookup"><span data-stu-id="dbef3-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="dbef3-131">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-131">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-132">`<resource-group-location>`Hallo-locatie van hello Azure-resourcegroep toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-132">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-133">`<database-account-name>`Hallo-naam van hello Azure Cosmos DB database account toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dbef3-133">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe created.</span></span> <span data-ttu-id="dbef3-134">Deze kan alleen worden gebruikt kleine letters, cijfers, Hallo '-' bevatten, en moet tussen 3 en 50 tekens.</span><span class="sxs-lookup"><span data-stu-id="dbef3-134">It can only use lowercase letters, numbers, hello '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="dbef3-135">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="dbef3-136">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dbef3-136">Notes</span></span>
* <span data-ttu-id="dbef3-137">Hallo voorgaande voorbeeld wordt een databaseaccount met twee regio's.</span><span class="sxs-lookup"><span data-stu-id="dbef3-137">hello preceding example creates a database account with two regions.</span></span> <span data-ttu-id="dbef3-138">Het is ook mogelijk toocreate een databaseaccount met één regio (die is aangewezen als Hallo schrijven regio en een failover-prioriteitswaarde van 0 hebben) of meer dan twee regio's.</span><span class="sxs-lookup"><span data-stu-id="dbef3-138">It is also possible toocreate a database account with either one region (which is designated as hello write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="dbef3-139">Zie voor meer informatie [meerdere landen/regio database accounts][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="dbef3-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="dbef3-140">Hallo locaties moet gebieden waarin Azure Cosmos DB in het algemeen beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="dbef3-140">hello locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="dbef3-141">Hallo huidige lijst met regio's is beschikbaar op Hallo [Azure-gebieden pagina](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="dbef3-141">hello current list of regions is provided on hello [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="dbef3-142"><a id="update-documentdb-account-powershell"></a>Een DocumentDB-databaseaccount bijwerken</span><span class="sxs-lookup"><span data-stu-id="dbef3-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="dbef3-143">Deze opdracht kunt u tooupdate de eigenschappen van uw Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="dbef3-143">This command allows you tooupdate your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="dbef3-144">Dit omvat Hallo consistentie beleid en het Hallo-locaties welke Hallo databaseaccount bestaat in.</span><span class="sxs-lookup"><span data-stu-id="dbef3-144">This includes hello consistency policy and hello locations which hello database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="dbef3-145">Deze opdracht kunt u de regio's tooadd en wordt verwijderd, maar staat niet toe dat u toomodify failover prioriteiten.</span><span class="sxs-lookup"><span data-stu-id="dbef3-145">This command allows you tooadd and remove regions but does not allow you toomodify failover priorities.</span></span> <span data-ttu-id="dbef3-146">toomodify failover prioriteiten, Zie [hieronder](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="dbef3-146">toomodify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="dbef3-147">`<write-region-location>`de locatienaam Hallo Hallo regio van het databaseaccount Hallo schrijven.</span><span class="sxs-lookup"><span data-stu-id="dbef3-147">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="dbef3-148">Deze locatie is vereist toohave een prioriteitswaarde failover van 0.</span><span class="sxs-lookup"><span data-stu-id="dbef3-148">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="dbef3-149">Er moet exact één schrijven regio per databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="dbef3-150">`<read-region-location>`de locatienaam Hallo Hallo lezen regio van het databaseaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbef3-150">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="dbef3-151">Deze locatie is vereist toohave failover prioriteitswaarde groter dan 0.</span><span class="sxs-lookup"><span data-stu-id="dbef3-151">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="dbef3-152">Er zijn meer dan één lezen regio's per database-account.</span><span class="sxs-lookup"><span data-stu-id="dbef3-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="dbef3-153">`<default-consistency-level>`Hallo consistentie standaardniveau van hello Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="dbef3-153">`<default-consistency-level>` hello default consistency level of hello Azure Cosmos DB account.</span></span> <span data-ttu-id="dbef3-154">Zie voor meer informatie [Consistentieniveaus in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="dbef3-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="dbef3-155">`<ip-range-filter>`Hiermee geeft u Hallo reeks IP-adressen of IP-adresbereiken in CIDR-formulier toobe Hallo toegestane lijst met client-IP-adressen voor een bepaalde database-account wordt opgenomen.</span><span class="sxs-lookup"><span data-stu-id="dbef3-155">`<ip-range-filter>` Specifies hello set of IP addresses or IP address ranges in CIDR form toobe included as hello allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="dbef3-156">IP-adressen of-adresbereiken moet door komma's gescheiden en mag geen spaties bevatten.</span><span class="sxs-lookup"><span data-stu-id="dbef3-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="dbef3-157">Zie voor meer informatie [Azure Cosmos DB-Firewallondersteuning](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="dbef3-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="dbef3-158">`<max-interval>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo tijd hoeveelheid veroudering (in seconden) toegestaan.</span><span class="sxs-lookup"><span data-stu-id="dbef3-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents hello time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="dbef3-159">Geaccepteerde bereik voor deze waarde is 1-100.</span><span class="sxs-lookup"><span data-stu-id="dbef3-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="dbef3-160">`<max-staleness-prefix>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo aantal verlopen aanvragen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="dbef3-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents hello number of stale requests tolerated.</span></span> <span data-ttu-id="dbef3-161">Geaccepteerde bereik voor deze waarde is 1 – 2.147.483.647.</span><span class="sxs-lookup"><span data-stu-id="dbef3-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="dbef3-162">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-162">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-163">`<resource-group-location>`Hallo-locatie van hello Azure-resourcegroep toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-163">`<resource-group-location>` hello location of hello Azure Resource Group toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-164">`<database-account-name>`Hallo-naam van hello Azure Cosmos DB database account toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="dbef3-164">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe updated.</span></span>

<span data-ttu-id="dbef3-165">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="dbef3-166"><a id="delete-documentdb-account-powershell"></a>Een DocumentDB-databaseaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="dbef3-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="dbef3-167">Deze opdracht kunt u een bestaande Azure DB die Cosmos-databaseaccount toodelete.</span><span class="sxs-lookup"><span data-stu-id="dbef3-167">This command allows you toodelete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="dbef3-168">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-168">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-169">`<database-account-name>`Hallo-naam van hello Azure Cosmos DB database account toobe verwijderd.</span><span class="sxs-lookup"><span data-stu-id="dbef3-169">`<database-account-name>` hello name of hello Azure Cosmos DB database account toobe deleted.</span></span>

<span data-ttu-id="dbef3-170">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="dbef3-171"><a id="get-documentdb-properties-powershell"></a>Eigenschappen van een DocumentDB-databaseaccount opgehaald</span><span class="sxs-lookup"><span data-stu-id="dbef3-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="dbef3-172">Deze opdracht kunt u tooget Hallo eigenschappen van een bestaande account voor Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="dbef3-172">This command allows you tooget hello properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="dbef3-173">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-173">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-174">`<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-174">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="dbef3-175">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="dbef3-176"><a id="update-tags-powershell"></a>Labels van een Azure Cosmos DB databaseaccount bijwerken</span><span class="sxs-lookup"><span data-stu-id="dbef3-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="dbef3-177">Hallo volgende voorbeeld wordt beschreven hoe tooset [Azure resourcetags] [ azure-resource-tags] database voor uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="dbef3-177">hello following example describes how tooset [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="dbef3-178">Met deze opdracht kan worden gecombineerd met Hallo maken of bijwerken van opdrachten door toe te voegen Hallo `-Tags` markering op in de bijbehorende parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbef3-178">This command can be combined with hello create or update commands by appending hello `-Tags` flag with hello corresponding parameter.</span></span>

<span data-ttu-id="dbef3-179">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="dbef3-180"><a id="list-account-keys-powershell"></a>Lijst met sleutels</span><span class="sxs-lookup"><span data-stu-id="dbef3-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="dbef3-181">Wanneer u een Azure DB die Cosmos-account maakt, genereert Hallo service twee master toegangstoetsen die kunnen worden gebruikt voor verificatie wanneer hello Azure DB die Cosmos-account wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="dbef3-181">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="dbef3-182">Dankzij twee toegangssleutels, kunnen Azure Cosmos DB tooregenerate Hallo sleutels met niets onderbreking tooyour Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="dbef3-182">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> <span data-ttu-id="dbef3-183">Alleen-lezen sleutels voor het verifiëren van alleen-lezen bewerkingen zijn ook beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="dbef3-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="dbef3-184">Er zijn twee lezen / schrijven-sleutels (primair en secundair) en twee sleutels voor alleen-lezen (primair en secundair).</span><span class="sxs-lookup"><span data-stu-id="dbef3-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="dbef3-185">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-185">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-186">`<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-186">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="dbef3-187">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="dbef3-188"><a id="list-connection-strings-powershell"></a>Lijst met verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="dbef3-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="dbef3-189">Hallo connection string tooconnect die uw databaseaccount MongoDB app toohello kan worden opgehaald met volgende opdracht Hallo voor MongoDB-accounts.</span><span class="sxs-lookup"><span data-stu-id="dbef3-189">For MongoDB accounts, hello connection string tooconnect your MongoDB app toohello database account can be retrieved using hello following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="dbef3-190">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-190">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-191">`<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-191">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="dbef3-192">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="dbef3-193"><a id="regenerate-account-key-powershell"></a>Accountsleutel opnieuw genereren</span><span class="sxs-lookup"><span data-stu-id="dbef3-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="dbef3-194">Hallo sleutels tooyour Azure Cosmos DB toegangsaccount moet u regelmatig toohelp beter te beveiligen uw verbindingen.</span><span class="sxs-lookup"><span data-stu-id="dbef3-194">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="dbef3-195">Twee toegangssleutels toegewezen tooenable u toomaintain verbindingen toohello Azure DB die Cosmos-account met behulp van één toegangssleutel terwijl u genereren Hallo andere toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="dbef3-195">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="dbef3-196">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-196">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-197">`<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-197">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="dbef3-198">`<key-kind>`Een van de Hallo vier typen sleutels: ["Primaire" | " Secundaire "|" PrimaryReadonly "|" SecondaryReadonly"] waarin u tooregenerate zou willen.</span><span class="sxs-lookup"><span data-stu-id="dbef3-198">`<key-kind>` One of hello four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like tooregenerate.</span></span>

<span data-ttu-id="dbef3-199">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="dbef3-200"><a id="modify-failover-priority-powershell"></a>Prioriteit van de Failover van een databaseaccount Azure Cosmos DB wijzigen</span><span class="sxs-lookup"><span data-stu-id="dbef3-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="dbef3-201">U kunt Hallo failover prioriteit Hallo verschillende regio's die hello Azure DB die Cosmos-databaseaccount bestaat in wijzigen voor meerdere landen/regio-database-accounts.</span><span class="sxs-lookup"><span data-stu-id="dbef3-201">For multi-region database accounts, you can change hello failover priority of hello various regions which hello Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="dbef3-202">Zie voor meer informatie over failover in uw Azure DB die Cosmos-databaseaccount [gegevens globaal met Azure Cosmos DB distribueren][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="dbef3-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="dbef3-203">`<write-region-location>`de locatienaam Hallo Hallo regio van het databaseaccount Hallo schrijven.</span><span class="sxs-lookup"><span data-stu-id="dbef3-203">`<write-region-location>` hello location name of hello write region of hello database account.</span></span> <span data-ttu-id="dbef3-204">Deze locatie is vereist toohave een prioriteitswaarde failover van 0.</span><span class="sxs-lookup"><span data-stu-id="dbef3-204">This location is required toohave a failover priority value of 0.</span></span> <span data-ttu-id="dbef3-205">Er moet exact één schrijven regio per databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="dbef3-206">`<read-region-location>`de locatienaam Hallo Hallo lezen regio van het databaseaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbef3-206">`<read-region-location>` hello location name of hello read region of hello database account.</span></span> <span data-ttu-id="dbef3-207">Deze locatie is vereist toohave failover prioriteitswaarde groter dan 0.</span><span class="sxs-lookup"><span data-stu-id="dbef3-207">This location is required toohave a failover priority value of greater than 0.</span></span> <span data-ttu-id="dbef3-208">Er zijn meer dan één lezen regio's per database-account.</span><span class="sxs-lookup"><span data-stu-id="dbef3-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="dbef3-209">`<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.</span><span class="sxs-lookup"><span data-stu-id="dbef3-209">`<resource-group-name>` hello name of hello [Azure Resource Group][azure-resource-groups] toowhich hello new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="dbef3-210">`<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="dbef3-210">`<database-account-name>` hello name of hello Azure Cosmos DB database account.</span></span>

<span data-ttu-id="dbef3-211">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dbef3-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="dbef3-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dbef3-212">Next steps</span></span>

* <span data-ttu-id="dbef3-213">tooconnect met .NET, Zie [Connect en query met .NET](create-documentdb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dbef3-213">tooconnect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="dbef3-214">met .NET Core tooconnect Zie [Connect en query met .NET Core](create-documentdb-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="dbef3-214">tooconnect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="dbef3-215">tooconnect met behulp van Node.js, Zie [Connect en query met Node.js en een app MongoDB](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dbef3-215">tooconnect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
