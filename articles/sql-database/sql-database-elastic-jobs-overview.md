---
title: aaaManaging cloud uitgebreide databases | Microsoft Docs
description: Illustreert Hallo elastische database taak service
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Cloud uitgebreide databases beheren
toomanage uitgebreid shard-databases Hallo **elastische Database taken** functie (preview) kunt u tooreliably uitvoeren van een script Transact-SQL (T-SQL) in een groep van databases, met inbegrip van:

* een aangepaste verzameling van databases (Zie hieronder)
* alle databases in een [elastische groep](sql-database-elastic-pool.md)
* een set shard (gemaakt met behulp van [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md)). 

## <a name="documentation"></a>Documentatie
* [Hallo elastische Database taak onderdelen installeren](sql-database-elastic-jobs-service-installation.md). 
* [Aan de slag met elastische Database taken](sql-database-elastic-jobs-getting-started.md).
* [Maken en beheren van taken met behulp van PowerShell](sql-database-elastic-jobs-powershell.md).
* [Maken en beheren van geschaalde uit Azure SQL-Databases](sql-database-elastic-jobs-getting-started.md)

**Elastische Database taken** is momenteel een klant gehost Azure Cloud Service waarmee Hallo uitvoering van ad-hoc en geplande administratieve taken die worden aangeroepen **taken**. Met taken, kan eenvoudig en betrouwbaar grote groepen van Azure SQL-Databases beheren door het uitvoeren van Transact-SQL-scripts tooperform administratieve bewerkingen. 

![Service voor elastische database-taak][1]

## <a name="why-use-jobs"></a>Waarom taken gebruiken?
**Beheren**

Schemawijzigingen eenvoudig doen, Referentiebeheer, verwijzing Gegevensupdates, prestatiegegevens verzamelen of telemetrie tenantverzameling (klant).

**Rapporten**

Cumulatieve gegevens uit een verzameling van Azure SQL-Databases in een doeltabel met één.

**Overhead verminderen**

Normaal gesproken moet u verbinding maken met de database tooeach onafhankelijk in volgorde toorun Transact-SQL-instructies of andere beheertaken uitvoeren. Een taak verwerkt Hallo taak in de database in de doelgroep Hallo tooeach aan te melden. U ook definiëren, onderhouden en persistent maken van Transact-SQL-scripts toobe uitgevoerd in een groep van Azure SQL-Databases.

**Accounting**

Taken uitgevoerd Hallo script- en logboekbestanden Hallo status van de uitvoering voor elke database. Automatisch opnieuw wordt ook krijgen als er fouten optreden.

**Flexibiliteit**

Aangepaste groepen van Azure SQL-Databases, en schema's voor het uitvoeren van een taak te definiëren.

> [!NOTE]
> Hallo Azure-portal, alleen een beperkte set functies beperkt tooSQL Azure elastische groepen is beschikbaar. Hallo PowerShell APIs tooaccess Hallo volledige set van de huidige functionaliteit gebruiken.
> 
> 

## <a name="applications"></a>Toepassingen
* Administratieve taken uitvoeren, zoals het implementeren van een nieuw schema.
* Algemene referentie gegevens product-informatie voor alle databases bijwerken. Of schema's automatische updates elke weekdag, na uur.
* Prestaties van query's tooimprove indexen opnieuw worden opgebouwd. Hallo opnieuw opbouwen kan worden geconfigureerd tooexecute in een verzameling van databases op periodieke basis, zoals tijdens de daluren.
* Queryresultaten uit een set van databases in een centrale tabel op basis van de lopende verzamelen. Prestaties van query's kunnen worden voortdurend uitgevoerd en geconfigureerd tootrigger extra taken toobe uitgevoerd.
* Langer actief gegevensverwerking-query's uitvoeren in een groot aantal databases, bijvoorbeeld Hallo verzameling telemetrie van de klant. Resultaten worden verzameld in een doeltabel met één voor verdere analyse.

## <a name="elastic-database-jobs-end-to-end"></a>Elastische taken van de Database: end-to-end
1. Hallo installeren **elastische Database taken** onderdelen. Zie voor meer informatie [elastische Database installeren taken](sql-database-elastic-jobs-service-installation.md). Als het Hallo-installatie mislukt, raadpleegt u [hoe toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Gebruik PowerShell APIs tooaccess Hallo meer functionaliteit, bijvoorbeeld het maken van aangepaste database verzamelingen, schema's toe te voegen en/of resultatensets verzamelen. Hallo-portal gebruiken voor eenvoudige installatie en het maken/bewaking van taken beperkt tooexecution tegen een **elastische pool**. 
3. Gecodeerde referenties voor het uitvoeren van taak maken en [Hallo gebruiker (of rol) tooeach database toevoegen in de groep Hallo](sql-database-security-overview.md).
4. Maak een idempotent T-SQL-script dat kan worden uitgevoerd op elke database in Hallo-groep. 
5. Volg deze stappen toocreate taken met behulp van hello Azure-portal: [maken en beheren van taken voor elastische Database](sql-database-elastic-jobs-create-and-manage.md). 
6. Of PowerShell-scripts gebruiken: [maken en beheren van een SQL-Database elastische database taken met behulp van PowerShell (preview)](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>De Idempotent-scripts
Hallo scripts moet [idempotent](https://en.wikipedia.org/wiki/Idempotence). In simpele termen betekent 'idempotent' dat als Hallo script kan worden uitgevoerd en wordt opnieuw uitgevoerd, hello hetzelfde resultaat plaatsvindt. Een script mislukken vanwege netwerkproblemen tootransient. In dat geval opnieuw Hallo taak automatisch uitgevoerd Hallo script een vooraf ingestelde aantal keren voordat desisting. Een script idempotent heeft Hallo hetzelfde resultaat, zelfs als is twee keer met succes is uitgevoerd. 

Een eenvoudige e-mailbericht is tootest Hallo bestaan van een object voordat u deze maakt.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

Op deze manier een script moet kunnen tooexecute is door logisch voor testen en tegen te gaan eventuele voorwaarden gevonden.

## <a name="failures-and-logs"></a>Logboeken en fouten
Een script mislukt na meerdere pogingen, Hallo taak Hallo fout wordt vastgelegd als blijft. Nadat een taak is beëindigd kunt (wat betekent een uitgevoerd tegen alle databases in de groep Hallo), u controleren de lijst met mislukte pogingen. Hallo Logboeken vindt u informatie toodebug defecte scripts. 

## <a name="group-types-and-creation"></a>Groep typen en maken
Er zijn twee soorten groepen: 

1. Shard sets
2. Aangepaste groepen

Shard set groepen zijn gemaakt met behulp van Hallo [hulpmiddelen voor elastische databases](sql-database-elastic-scale-introduction.md). Wanneer u een set shard groep maakt, worden de databases toegevoegd of uit Hallo groep automatisch verwijderd. Bijvoorbeeld, een nieuwe shard worden automatisch in de groep Hallo wanneer u deze toohello shard-toewijzing toevoegen. Een taak kan vervolgens worden uitgevoerd tegen Hallo-groep.

Aangepaste groepen op Hallo daarentegen, streng worden gedefinieerd. U moet expliciet toevoegen of verwijderen van databases uit aangepaste groepen. Als een database in de groep hello wordt verbroken, probeert Hallo taak toorun Hallo-script op Hallo database, wat resulteert in een problemen. Groepen die zijn gemaakt met behulp van hello Azure-portal op dit moment zijn aangepaste groepen. 

## <a name="components-and-pricing"></a>Onderdelen en prijzen
Hallo samenwerken volgende onderdelen toocreate een Azure-Cloud-service waarmee ad-hoc-uitvoering van administratieve taken. Hallo-componenten zijn geïnstalleerd en wordt automatisch geconfigureerd tijdens de installatie in uw abonnement. Kunt u Hallo services identificeren als ze allemaal hebt Hallo dezelfde automatisch gegenereerde naam. Hallo naam uniek is en bestaat uit Hallo voorvoegsel 'edj' gevolgd door 21 willekeurige tekens.

* **Azure-Cloudservice**: taken voor elastische database (preview) wordt geleverd als een klant gehost Azure Cloud service tooperform uitvoering van Hallo aangevraagd taken. Hallo-service is geïmplementeerd en gehost in uw Microsoft Azure-abonnement vanuit Hallo-portal. Hallo standaard geïmplementeerd-service wordt uitgevoerd met Hallo ten minste twee werkrollen voor hoge beschikbaarheid. de standaardgrootte Hallo van elke worker-rol (ElasticDatabaseJobWorker) wordt uitgevoerd op een exemplaar van A0. Zie voor prijzen [cloudservices-prijzen](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Azure SQL Database**: Hallo-service gebruikt een Azure SQL Database bekend als Hallo **beheer database** toostore alle Hallo taak metagegevens van. Hallo standaard servicelaag is een S0. Zie voor prijzen [prijzen SQL Database](https://azure.microsoft.com/pricing/details/sql-database/).
* **Azure Service Bus**: een Azure Service Bus is voor de coördinatie van Hallo werk binnen hello Azure Cloud Service. Zie [Service Bus prijzen](https://azure.microsoft.com/pricing/details/service-bus/).
* **Azure Storage**: een Azure Storage-account wordt gebruikt toostore diagnostische uitvoer logboekregistratie in Hallo gebeurtenis waarvoor een probleem verder foutopsporing (Zie [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](../cloud-services/cloud-services-dotnet-diagnostics.md)). Zie voor prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>De werking van taken voor elastische Database
1. Een Azure SQL Database is aangewezen een **beheer database** waarin alle gegevens in de metagegevens en de status wordt opgeslagen.
2. Hallo beheer database wordt geopend door Hallo **service taak** toolaunch en bijhouden taken tooexecute.
3. Twee verschillende rollen communiceren met de Hallo beheer database: 
   * Controller: Hiermee wordt bepaald welke taken vereisen taken tooperform Hallo aangevraagd taak en mislukte taken voor nieuwe pogingen door het maken van nieuwe taken.
   * Taak taakuitvoering: Wordt uitgevoerd Hallo taken.

### <a name="job-task-types"></a>Taak taaktypen
Er zijn meerdere typen taken die de uitvoering van taken uitvoeren:

* ShardMapRefresh: Query's Hallo shard-toewijzing toodetermine alle Hallo databases als shards gebruikt
* ScriptSplit: Splitsingen Hallo script via de GO'-instructies in batches
* ExpandJob: Maakt onderliggende taken voor elke database uit een taak die gericht is op een groep met databases
* ScriptExecution: Een script op basis van een bepaalde database met gedefinieerde referenties wordt uitgevoerd
* Dacpac: Geldt een DACPAC tooa bepaalde database met behulp van bepaalde referenties

## <a name="end-to-end-job-execution-work-flow"></a>End-to-end-taak kan worden uitgevoerd-werkstroom
1. Met Hallo Portal of PowerShell API hello, een taak wordt ingevoegd in Hallo **beheer database**. Hallo taak vraagt om de uitvoering van een Transact-SQL-script voor een groep van databases met behulp van specifieke referenties.
2. Hallo controller identificeert Hallo nieuwe taak. Taken worden gemaakt en toosplit Hallo script en toorefresh Hallo groep databases uitgevoerd. Ten slotte wordt een nieuwe taak is gemaakt en tooexpand Hallo taak uitgevoerd en nieuwe onderliggende taken waarbij elke onderliggende taak opgegeven tooexecute Hallo Transact-SQL-script op een individuele database in Hallo groep is maken.
3. Hallo controller identificeert Hallo onderliggende taken gemaakt. Voor elke taak Hallo domeincontroller maakt en een taak taak tooexecute Hallo script op basis van een database wordt geactiveerd. 
4. Nadat alle taken hebt voltooid, werkt Hallo controller Hallo taken tooa voltooid status. 
   Op elk moment tijdens de taakuitvoering mag Hallo PowerShell API gebruikte tooview Hallo van de huidige status van taak kan worden uitgevoerd. Alle tijden geretourneerd door Hallo PowerShell APIs worden weergegeven in UTC. Indien gewenst, kan een annuleringsverzoek geïnitieerd toostop een taak zijn. 

## <a name="next-steps"></a>Volgende stappen
[Hallo-onderdelen installeren](sql-database-elastic-jobs-service-installation.md), klikt u vervolgens [maken en toevoegen van een logboek in de database in de groep met databases Hallo tooeach](sql-database-manage-logins.md). toofurther begrijpen taak maken en beheren, Zie [maken en beheren van taken voor elastische database](sql-database-elastic-jobs-create-and-manage.md). Zie ook [aan de slag met elastische Database taken](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


