---
title: aaaDistributed transacties voor cloud-databases
description: Overzicht van transacties met Azure SQL Database elastische Database
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Over clouddatabases gedistribueerde transacties
Elastische databasetransacties voor Azure SQL Database (SQL DB) kunnen u toorun transacties die verschillende databases in SQL-database omvatten. Elastische databasetransacties voor SQL-database zijn beschikbaar voor .NET-toepassingen die gebruikmaken van ADO .NET en integreren met Hallo bekend programmeerervaring met Hallo [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) klassen. tooget hello bibliotheek, Zie [.NET Framework 4.6.1 (webinstallatie)](https://www.microsoft.com/download/details.aspx?id=49981).

On-premises vereist dergelijk scenario doorgaans Microsoft Distributed Transaction Coordinator (MSDTC) wordt uitgevoerd. Aangezien MSDTC is niet beschikbaar voor Platform-as-a-Service-toepassing in Azure, Hallo mogelijkheid toocoordinate gedistribueerde transacties is nu rechtstreeks geïntegreerd in SQL-database. Toepassingen kunnen verbinding maken tooany SQL-Database toolaunch gedistribueerde transacties en wordt een van de databases Hallo Hallo gedistribueerde transactie, transparant coördineren zoals weergegeven in de volgende afbeelding Hallo. 

  ![Gedistribueerde transacties met Azure SQL Database met behulp van transacties voor elastische database ][1]

## <a name="common-scenarios"></a>Algemene scenario's
Elastische databasetransacties voor SQL-database inschakelen toepassingen toomake atomische wijzigingen toodata opgeslagen in een aantal verschillende SQL-Databases. Hallo preview is gericht op de ervaringen van de client-side '-ontwikkeling in C# en .NET. Een server-side '-ervaring met T-SQL is gepland voor een later tijdstip.  
Elastische database transacties doelen Hallo volgen scenario's:

* Toepassingen in Azure meerdere databases: met dit scenario gegevens is verticaal gepartitioneerd in verschillende databases in SQL-database zodanig dat verschillende soorten gegevens zich op andere databases bevinden. Bepaalde bewerkingen vereist wijzigingen toodata die wordt bewaard in twee of meer databases. Hallo-toepassing maakt gebruik van de elastische database transacties toocoordinate Hallo wijzigingen over databases en zorg ervoor dat atomisch.
* Databasetoepassingen van de shard-in Azure: met dit scenario gebruikt gegevenslaag Hallo Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md) of self-sharding toohorizontally partitie Hallo gegevens tussen meerdere databases in SQL-database. Een opvallende gebruiksvoorbeeld is Hallo nodig tooperform atomische wijzigingen voor een toepassing met shard multitenant wanneer wijzigingen span tenants. Beschouw bijvoorbeeld een overdracht van een tenant tooanother, beide die zich op verschillende databases. Een tweede geval is fijnmazig sharding tooaccommodate capaciteitsbehoeften voor een grote tenant die op zijn beurt doorgaans impliceert dat een aantal atomische bewerkingen behoeften toostretch over verschillende databases gebruikt voor Hallo dezelfde tenant. Een derde wordt atomic updates tooreference gegevens die worden gerepliceerd tussen databases. Atomic, transactionele, bewerkingen langs deze regels kunnen nu worden gecoördineerd tussen verschillende databases met Hallo preview.
  Elastische databasetransacties gebruiken doorvoertransactie tooensure transactie atomisch in databases. Het is geschikt voor transacties met minder dan 100 databases op een tijdstip binnen een transactie. Deze limieten worden niet afgedwongen, maar een verwachte prestaties en het succespercentage voor elastische database transacties toosuffer wanneer deze limiet wordt overschreden.

## <a name="installation-and-migration"></a>Installatie en migratie
Hallo-mogelijkheden voor elastische databasetransacties in SQL-database zijn opgenomen in updates toohello .NET-bibliotheken System.Data.dll en System.Transactions.dll. Hallo dll's ervoor te zorgen dat doorvoertransactie wordt gebruikt, indien nodig tooensure atomisch. toostart ontwikkelen toepassingen met elastische databasetransacties, installeren [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) of een latere versie. Wanneer dit wordt uitgevoerd op een eerdere versie van .NET framework voor hello, transacties toopromote tooa gedistribueerde transactie mislukt en wordt een uitzondering wordt gegenereerd.

U kunt na de installatie Hallo gedistribueerde transactie API's gebruiken in System.Transactions met verbindingen tooSQL DB. Als er bestaande MSDTC-toepassingen met behulp van deze API's, gewoon uw bestaande .NET 4.6-toepassingen opnieuw na de installatie van Hallo 4.6.1 Framework. Als uw projecten .NET 4.6 richten, gebruiken ze automatisch bijgewerkt Hallo-dll's van Hallo nieuwe Framework-versie en de gedistribueerde transactie API-aanroepen in combinatie met verbindingen tooSQL die DB nu slaagt.

Houd er rekening mee dat transacties voor elastische database vereisen geen MSDTC installeren. In plaats daarvan worden elastische databasetransacties rechtstreeks beheerd door en binnen SQL-database. Dit vereenvoudigt scenario's voor de aanzienlijk omdat een implementatie van MSDTC niet nodig toouse gedistribueerde transacties met SQL-database is. Sectie 4 wordt in meer detail uitgelegd hoe toodeploy elastische databasetransacties en Hallo .NET framework samen met uw tooAzure cloud-toepassingen vereist.

## <a name="development-experience"></a>Ontwikkeling biedt
### <a name="multi-database-applications"></a>Meerdere databasetoepassingen
Hallo volgende voorbeeldcode maakt gebruik van Hallo bekend programmeerervaring met .NET System.Transactions. Hallo TransactionScope klasse stelt een ambient transactie in .NET. (Een 'ambient transactie' is een die zich in de huidige thread Hallo.) Alle verbindingen in Hallo TransactionScope geopend deel uitmaken van Hallo transactie. Als verschillende databases deelnemen, is het Hallo-transactie automatisch verhoogde tooa gedistribueerde transactie. Hallo-resultaat van Hallo transactie wordt beheerd door Hallo bereik toocomplete tooindicate een doorvoer.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Shard databasetoepassingen
Elastische databasetransacties voor SQL-database bieden ook ondersteuning voor gedistribueerde transacties waar u Hallo OpenConnectionForKey methode van Hallo elastische database-bibliotheek tooopen clientverbindingen voor een uitgebreid uit gegevens gebruiken coördineren laag. Houd rekening met gevallen waarin u tooguarantee transactionele consistentie wijzigingen via diverse verschillende sharding-sleutelwaarden moet. Verbindingen toohello shards die als host fungeert voor Hallo verschillende sharding sleutelwaarden worden geleverd met OpenConnectionForKey. In de algemene geval Hallo kunnen Hallo verbindingen toodifferent shards zijn, dat gezorgd transactionele garanties een gedistribueerde transactie vereist. Hallo volgende codevoorbeeld ziet u deze methode. Hierbij wordt ervan uitgegaan dat een variabele met de naam van shardmap gebruikte toorepresent een shard van clientbibliotheek voor elastische database Hallo toewijzen:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>.NET-installatie voor Azure Cloud Services
Azure biedt verschillende aanbiedingen toohost .NET-toepassingen. Een vergelijking van verschillende Hallo-aanbiedingen is beschikbaar in [vergelijking van Azure App Service, Cloud Services en virtuele Machines](../app-service-web/choose-web-site-cloud-service-vm.md). Als hello gastbesturingssysteem van de aanbieding Hallo kleiner dan .NET 4.6.1 vereist voor de elastische transacties is, moet u tooupgrade Hallo Gast OS too4.6.1. 

Upgrade voor Azure App Services toohello Gast die OS worden momenteel niet ondersteund. Voor Azure Virtual Machines gewoon aanmelden op Hallo VM en voer het Hallo-installatieprogramma voor Hallo nieuwste .NET framework. Voor Azure Cloud Services moet u tooinclude Hallo installatie van een nieuwere versie van .NET in Hallo starten van de taken van uw implementatie. Hallo-concepten en stappen worden beschreven in [.NET installeren op een Cloud Service-functie](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

Let op Hallo installatieprogramma voor .NET 4.6.1 mogelijk meer tijdelijke opslag tijdens het uitvoeren van de bootstrap-proces op Azure-cloudservices dan installatieprogramma voor .NET 4.6 Hallo Hallo. tooensure een geslaagde installatie, moet u tooincrease tijdelijke opslag voor uw Azure-cloud-service in uw bestand ServiceDefinition.csdef in Hallo LocalResources sectie en omgevingsinstellingen Hallo van uw taak starten, zoals wordt weergegeven in de volgende Hallo Voorbeeld:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Transacties op meerdere servers
Elastische databasetransacties worden ondersteund tussen de verschillende logische Azure SQL Database-servers. Meerdere grenzen van de logische server, moeten Hallo deelnemende servers eerst toobe ingevoerd in een relatie wederzijdse communicatie. Zodra het Hallo communicatie relatie tot stand is gebracht, Hallo eender welke database in een van twee servers elastische transacties met databases van deelnemen kunnen Hallo andere server. Met transacties spanning van meer dan twee logische servers moet een relatie communicatie toobe in plaats voor elk paar logische servers.

Gebruik Hallo PowerShell-cmdlets toomanage communicatie tussen servers relaties voor elastische databasetransacties te volgen:

* **Nieuwe AzureRmSqlServerCommunicationLink**: Gebruik deze cmdlet toocreate een nieuwe relatie van de communicatie tussen twee logische Azure SQL DB-servers. Hallo-relatie is symmetrische dat beide servers kunnen initiëren transacties met Hallo andere server.
* **Get-AzureRmSqlServerCommunicationLink**: Gebruik deze cmdlet tooretrieve bestaande communicatie relaties en hun eigenschappen.
* **Verwijder AzureRmSqlServerCommunicationLink**: Gebruik deze cmdlet tooremove een bestaande relatie voor de communicatie. 

## <a name="monitoring-transaction-status"></a>Controle van transactiestatus
Gebruik dynamische beheerweergaven (DMV's) in SQL-database toomonitor status en voortgang van uw transacties lopende elastische database. Alle DMV's gerelateerde tootransactions zijn relevant voor gedistribueerde transacties die in SQL-database. U kunt Hallo bijbehorende lijst van de DMV's hier vinden: [transactie gerelateerde dynamische Management weergaven en -functies (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).

Deze DMV's zijn vooral handig:

* **sys.DM\_tran\_active\_transacties**: een lijst met huidige actieve transacties en hun status. Hallo UOW (werkeenheid) kolom kunt identificeren Hallo verschillende onderliggende transacties die deel uitmaken van toohello dezelfde gedistribueerde transactie. Alle transacties in dezelfde gedistribueerde transactie uitvoeren Hallo Hallo dezelfde UOW-waarde. Zie Hallo [DMV documentatie](https://msdn.microsoft.com/library/ms174302.aspx) voor meer informatie.
* **sys.DM\_tran\_database\_transacties**: biedt aanvullende informatie over transacties, zoals de plaatsing van Hallo transactie in Hallo logboek. Zie Hallo [DMV documentatie](https://msdn.microsoft.com/library/ms186957.aspx) voor meer informatie.
* **sys.DM\_tran\_vergrendelingen**: bevat informatie over Hallo vergrendelingen die momenteel zijn ingesteld door actieve transacties. Zie Hallo [DMV documentatie](https://msdn.microsoft.com/library/ms190345.aspx) voor meer informatie.

## <a name="limitations"></a>Beperkingen
Hallo beperkingen momenteel volgende van toepassing tooelastic databasetransacties in SQL-database:

* Alleen de transacties voor databases in SQL-database worden ondersteund. Andere [X / Open XA](https://en.wikipedia.org/wiki/X/Open_XA) resourceproviders en databases buiten SQL-database kunnen niet deelnemen aan elastische databasetransacties. Dit betekent dat transacties voor elastische database kunnen niet uitrekken on-premises SQL Server en Azure SQL-Databases. Voor gedistribueerde transacties on-premises blijven toouse MSDTC. 
* Alleen client gecoördineerd transacties van een .NET-toepassing worden ondersteund. Server-side-ondersteuning voor T-SQL zoals BEGIN DISTRIBUTED TRANSACTION is gepland, maar nog niet beschikbaar. 
* Transacties die in de hele WCF-services worden niet ondersteund. U hebt bijvoorbeeld een WCF-service-methode die een transactie wordt uitgevoerd. Hallo-aanroepen vanuit een transactiebereik insluitende mislukt als een [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Volgende stappen
Voor vragen kunt contact toous op Hallo [SQL Database-forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) en voor functieaanvragen, deze toe te voegen toohello [forum met feedback van SQL-Database](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



