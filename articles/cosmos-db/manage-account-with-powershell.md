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
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>Een Azure DB die Cosmos-account maken met PowerShell

Hallo beschrijft volgende handleiding opdrachten tooautomate beheer van uw Azure Cosmos DB database accounts met Azure Powershell. Dit omvat ook opdrachten toomanage toegangscodes en failover prioriteiten in [meerdere landen/regio database accounts][scaling-globally]. Bijwerken van uw databaseaccount kunt u toomodify consistentie beleidsregels en regio's toevoegen of verwijderen. Voor het beheer van de platformoverschrijdende van uw Azure DB die Cosmos-account, kunt u een gebruiken [Azure CLI](cli-samples.md), Hallo [Resource Provider REST-API][rp-rest-api], of Hallo [Azure Portal](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Aan de slag

Volg de instructies in Hallo [hoe tooinstall en configureren van Azure PowerShell] [ powershell-install-configure] tooinstall en zich aanmelden tooyour Azure Resource Manager-account in Powershell.

### <a name="notes"></a>Opmerkingen

* Als u tooexecute Hallo opdrachten te volgen wilt zonder gebruikersbevestiging, toevoeg-Hallo `-Force` toohello opdracht vlag.
* Alle Hallo volgende opdrachten worden synchroon.

## <a id="create-documentdb-account-powershell"></a>Een Azure Cosmos DB-Account maken

Deze opdracht kunt u een databaseaccount Azure Cosmos DB toocreate. Uw nieuwe databaseaccount configureren als een regio of [meerdere landen/regio] [ scaling-globally] met een bepaald [consistentie beleid](consistency-levels.md).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`de locatienaam Hallo Hallo regio van het databaseaccount Hallo schrijven. Deze locatie is vereist toohave een prioriteitswaarde failover van 0. Er moet exact één schrijven regio per databaseaccount.
* `<read-region-location>`de locatienaam Hallo Hallo lezen regio van het databaseaccount Hallo. Deze locatie is vereist toohave failover prioriteitswaarde groter dan 0. Er zijn meer dan één lezen regio's per database-account.
* `<ip-range-filter>`Hiermee geeft u Hallo reeks IP-adressen of IP-adresbereiken in CIDR-formulier toobe Hallo toegestane lijst met client-IP-adressen voor een bepaalde database-account wordt opgenomen. IP-adressen of-adresbereiken moet door komma's gescheiden en mag geen spaties bevatten. Zie voor meer informatie [Azure Cosmos DB-Firewallondersteuning](firewall-support.md)
* `<default-consistency-level>`Hallo consistentie standaardniveau van hello Azure DB die Cosmos-account. Zie voor meer informatie [Consistentieniveaus in Azure Cosmos DB](consistency-levels.md).
* `<max-interval>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo tijd hoeveelheid veroudering (in seconden) toegestaan. Geaccepteerde bereik voor deze waarde is 1-100.
* `<max-staleness-prefix>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo aantal verlopen aanvragen toegestaan. Geaccepteerde bereik voor deze waarde is 1 – 2.147.483.647.
* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<resource-group-location>`Hallo-locatie van hello Azure-resourcegroep toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure Cosmos DB database account toobe gemaakt. Deze kan alleen worden gebruikt kleine letters, cijfers, Hallo '-' bevatten, en moet tussen 3 en 50 tekens.

Voorbeeld: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Opmerkingen
* Hallo voorgaande voorbeeld wordt een databaseaccount met twee regio's. Het is ook mogelijk toocreate een databaseaccount met één regio (die is aangewezen als Hallo schrijven regio en een failover-prioriteitswaarde van 0 hebben) of meer dan twee regio's. Zie voor meer informatie [meerdere landen/regio database accounts][scaling-globally].
* Hallo locaties moet gebieden waarin Azure Cosmos DB in het algemeen beschikbaar is. Hallo huidige lijst met regio's is beschikbaar op Hallo [Azure-gebieden pagina](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a>Een DocumentDB-databaseaccount bijwerken

Deze opdracht kunt u tooupdate de eigenschappen van uw Azure DB die Cosmos-database. Dit omvat Hallo consistentie beleid en het Hallo-locaties welke Hallo databaseaccount bestaat in.

> [!NOTE]
> Deze opdracht kunt u de regio's tooadd en wordt verwijderd, maar staat niet toe dat u toomodify failover prioriteiten. toomodify failover prioriteiten, Zie [hieronder](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`de locatienaam Hallo Hallo regio van het databaseaccount Hallo schrijven. Deze locatie is vereist toohave een prioriteitswaarde failover van 0. Er moet exact één schrijven regio per databaseaccount.
* `<read-region-location>`de locatienaam Hallo Hallo lezen regio van het databaseaccount Hallo. Deze locatie is vereist toohave failover prioriteitswaarde groter dan 0. Er zijn meer dan één lezen regio's per database-account.
* `<default-consistency-level>`Hallo consistentie standaardniveau van hello Azure DB die Cosmos-account. Zie voor meer informatie [Consistentieniveaus in Azure Cosmos DB](consistency-levels.md).
* `<ip-range-filter>`Hiermee geeft u Hallo reeks IP-adressen of IP-adresbereiken in CIDR-formulier toobe Hallo toegestane lijst met client-IP-adressen voor een bepaalde database-account wordt opgenomen. IP-adressen of-adresbereiken moet door komma's gescheiden en mag geen spaties bevatten. Zie voor meer informatie [Azure Cosmos DB-Firewallondersteuning](firewall-support.md)
* `<max-interval>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo tijd hoeveelheid veroudering (in seconden) toegestaan. Geaccepteerde bereik voor deze waarde is 1-100.
* `<max-staleness-prefix>`Met consistentie voor gebonden veroudering wordt gebruikt, geeft deze waarde Hallo aantal verlopen aanvragen toegestaan. Geaccepteerde bereik voor deze waarde is 1 – 2.147.483.647.
* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<resource-group-location>`Hallo-locatie van hello Azure-resourcegroep toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure Cosmos DB database account toobe bijgewerkt.

Voorbeeld: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a>Een DocumentDB-databaseaccount verwijderen

Deze opdracht kunt u een bestaande Azure DB die Cosmos-databaseaccount toodelete.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure Cosmos DB database account toobe verwijderd.

Voorbeeld:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a>Eigenschappen van een DocumentDB-databaseaccount opgehaald

Deze opdracht kunt u tooget Hallo eigenschappen van een bestaande account voor Azure DB die Cosmos-database.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.

Voorbeeld:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a>Labels van een Azure Cosmos DB databaseaccount bijwerken

Hallo volgende voorbeeld wordt beschreven hoe tooset [Azure resourcetags] [ azure-resource-tags] database voor uw Azure DB die Cosmos-account.

> [!NOTE]
> Met deze opdracht kan worden gecombineerd met Hallo maken of bijwerken van opdrachten door toe te voegen Hallo `-Tags` markering op in de bijbehorende parameter Hallo.

Voorbeeld:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a>Lijst met sleutels

Wanneer u een Azure DB die Cosmos-account maakt, genereert Hallo service twee master toegangstoetsen die kunnen worden gebruikt voor verificatie wanneer hello Azure DB die Cosmos-account wordt geopend. Dankzij twee toegangssleutels, kunnen Azure Cosmos DB tooregenerate Hallo sleutels met niets onderbreking tooyour Azure DB die Cosmos-account. Alleen-lezen sleutels voor het verifiëren van alleen-lezen bewerkingen zijn ook beschikbaar. Er zijn twee lezen / schrijven-sleutels (primair en secundair) en twee sleutels voor alleen-lezen (primair en secundair).

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.

Voorbeeld:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a>Lijst met verbindingsreeksen

Hallo connection string tooconnect die uw databaseaccount MongoDB app toohello kan worden opgehaald met volgende opdracht Hallo voor MongoDB-accounts.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.

Voorbeeld:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a>Accountsleutel opnieuw genereren

Hallo sleutels tooyour Azure Cosmos DB toegangsaccount moet u regelmatig toohelp beter te beveiligen uw verbindingen. Twee toegangssleutels toegewezen tooenable u toomaintain verbindingen toohello Azure DB die Cosmos-account met behulp van één toegangssleutel terwijl u genereren Hallo andere toegangssleutel.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.
* `<key-kind>`Een van de Hallo vier typen sleutels: ["Primaire" | " Secundaire "|" PrimaryReadonly "|" SecondaryReadonly"] waarin u tooregenerate zou willen.

Voorbeeld:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a>Prioriteit van de Failover van een databaseaccount Azure Cosmos DB wijzigen

U kunt Hallo failover prioriteit Hallo verschillende regio's die hello Azure DB die Cosmos-databaseaccount bestaat in wijzigen voor meerdere landen/regio-database-accounts. Zie voor meer informatie over failover in uw Azure DB die Cosmos-databaseaccount [gegevens globaal met Azure Cosmos DB distribueren][distribute-data-globally].

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`de locatienaam Hallo Hallo regio van het databaseaccount Hallo schrijven. Deze locatie is vereist toohave een prioriteitswaarde failover van 0. Er moet exact één schrijven regio per databaseaccount.
* `<read-region-location>`de locatienaam Hallo Hallo lezen regio van het databaseaccount Hallo. Deze locatie is vereist toohave failover prioriteitswaarde groter dan 0. Er zijn meer dan één lezen regio's per database-account.
* `<resource-group-name>`Hallo-naam van Hallo [Azure-resourcegroep] [ azure-resource-groups] toowhich Hallo nieuwe Azure DB die Cosmos-databaseaccount behoort.
* `<database-account-name>`Hallo-naam van hello Azure DB die Cosmos-databaseaccount.

Voorbeeld:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Volgende stappen

* tooconnect met .NET, Zie [Connect en query met .NET](create-documentdb-dotnet.md).
* met .NET Core tooconnect Zie [Connect en query met .NET Core](create-documentdb-dotnet-core.md).
* tooconnect met behulp van Node.js, Zie [Connect en query met Node.js en een app MongoDB](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
