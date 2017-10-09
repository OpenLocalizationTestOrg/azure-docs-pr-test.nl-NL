---
title: aaaScaling uit met Azure SQL Database | Microsoft Docs
description: Software als een Service (SaaS)-ontwikkelaars kan eenvoudig elastische maken, schaalbare databases in Hallo cloud met behulp van deze hulpprogramma 's
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Uitbreiden met Azure SQL Database
U kunt eenvoudig hello met Azure SQL-databases worden uitgebreid **elastische Database** hulpprogramma's. Deze hulpprogramma's en onderdelen kunnen u vrijwel onbeperkte Hallo resources van de database **Azure SQL Database** toocreate oplossingen voor transactionele werkbelastingen en met name de Software als een Service (SaaS)-toepassingen. Elastische databasefuncties van de volgende Hallo bestaan:

* [Clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md): Hallo-clientbibliotheek is een functie die u kunt u toocreate en onderhouden van shard-databases.  Zie [aan de slag met hulpprogramma's voor elastische Database](sql-database-elastic-scale-get-started.md).
* [Elastische Database gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md): verplaatst gegevens tussen de shard-databases. Dit is handig voor het verplaatsen van gegevens uit een multitenant database tooa één tenant-database (of andersom). Zie [elastische database gesplitste Merge tool zelfstudie](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Elastische Database taken](sql-database-elastic-jobs-overview.md) (preview): gebruik taken toomanage grote aantallen Azure SQL-databases. Gemakkelijk administratieve bewerkingen, zoals wijzigingen in het schema, Referentiebeheer, verwijzing Gegevensupdates, prestatiegegevens verzamelen of verzamelen van telemetriegegevens in de tenant (klant) met behulp van taken uitvoeren.
* [Elastische databasequery](sql-database-elastic-query-overview.md) (preview): Hiermee kunt u toorun een Transact-SQL-query die meerdere databases omvat. Hierdoor verbinding tooreporting hulpprogramma's zoals Excel, Power BI, Tableau, enzovoort.
* [Elastische transacties](sql-database-elastic-transactions-overview.md): deze functie kunt u toorun transacties die verschillende databases in Azure SQL Database omvatten. Elastische databasetransacties zijn beschikbaar voor .NET-toepassingen die gebruikmaken van ADO .NET en integreren met Hallo bekend programmeerervaring met Hallo [System.Transaction klassen](https://msdn.microsoft.com/library/system.transactions.aspx).

Hallo onderstaande afbeelding toont een architectuur met Hallo **elastische Database functies** in relatie tooa verzameling van databases.

In deze afbeelding vertegenwoordigen de kleuren van Hallo database schema's. Databases met Hallo Hallo dezelfde kleur delen hetzelfde schema.

1. Een set **Azure SQL-databases** worden gehost op Azure met behulp van sharding-architectuur.
2. Hallo **clientbibliotheek voor elastische Database** gebruikte toomanage een shard is ingesteld.
3. Een subset van Hallo databases worden die pakketten in een **elastische pool**. (Zie [wat is er een groep?](sql-database-elastic-pool.md)).
4. Een **elastische Database-taak** gepland of ad-hoc T-SQL-scripts uitvoeren op alle databases.
5. Hallo **gesplitste merge tool** gebruikte toomove gegevens uit één shard tooanother is.
6. Hallo **elastische Database query** kunt u een query die alle databases in de shard-set Hallo omvat toowrite.
7. **Elastische transacties** kunt u toorun transacties die verschillende databases omvatten. 

![Hulpprogramma's voor elastische databases][1]

## <a name="why-use-hello-tools"></a>Waarom Hallo-hulpprogramma's gebruiken?
Achieving elasticiteit en schaal voor cloud-toepassingen eenvoudig VM's en de blob-opslag simpelweg toevoegen of afgetrokken eenheden of vergroot power. Maar het moeilijk voor stateful gegevensverwerking in relationele databases is gebleven. Uitdagingen ontstaan in deze scenario's:

* Groeien en capaciteit voor Hallo relationele database deel uitmaakt van uw workload te verkleinen.
* Het beheren van hotspots die kunnen ontstaan die invloed hebben op een specifieke subset van gegevens -, zoals een bijzonder bezet end-klant (tenant).

Traditioneel zijn scenario's zoals deze door te investeren in grotere schaal servers toosupport Hallo databasetoepassing gericht. Deze optie wordt echter beperkt in Hallo cloud waarbij alle bijbehorende verwerkingen op vooraf gedefinieerde basishardware gebeurt. In plaats daarvan distribueren van gegevens en verwerking tussen meerdere databases identiek gestructureerd biedt (een patroon voor scale-out 'sharding' genoemd) een alternatieve tootraditional omhoog schalen benaderingen zowel op het gebied kosten en elasticiteit.

## <a name="horizontal-and-vertical-scaling"></a>Horizontale en verticale schalen
Hallo afbeelding hieronder toont Hallo horizontale en verticale dimensies van de schaal, die zijn basismethoden Hallo Hallo elastische databases kunnen worden geschaald.

![Horizontale en verticale Scaleout][2]

Horizontaal schalen verwijst tooadding of verwijderen databases in volgorde tooadjust capaciteit of de algehele prestaties. Dit is een afkorting 'schalen' uit. Sharding, waarin de gegevens in een verzameling van identieke gestructureerde databases zijn gepartitioneerd is een algemene manier tooimplement horizontale schaal.  

Verticale schaling verwijst tooincreasing of aflopende volgorde Hallo prestatieniveau van een individuele database — dit staat ook bekend als "omhoog schalen."

De meeste databasetoepassingen voor cloud-scale wordt een combinatie van deze twee strategieën gebruiken. Een servicetoepassing Software als een kan bijvoorbeeld horizontaal schalen tooprovision nieuwe end-klanten en verticaal schalen tooallow elke eindgebruiker database toogrow of verkleind resources naar behoefte door Hallo werkbelasting gebruiken.

* Horizontaal schalen wordt beheerd met behulp van Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md).
* Verticale schaling bereikt met behulp van Azure PowerShell-cmdlets toochange Hallo servicelaag, of door het plaatsen van databases in een elastische pool.

## <a name="sharding"></a>Sharding
*Sharding* is een techniek toodistribute grote hoeveelheden identiek gestructureerde gegevens over een aantal onafhankelijke databases. Het is vooral populaire met cloud-ontwikkelaars maken van Software als een Service (SAAS)-aanbiedingen voor end-klanten of bedrijven. Deze end-klanten zijn vaak waarnaar wordt verwezen tooas 'tenants'. Sharding mogelijk zijn vereist voor een aantal redenen zijn:  

* totale hoeveelheid gegevens Hallo is te groot toofit binnen Hallo beperkingen van een individuele database
* Hallo transactiedoorvoer Hallo algehele werkbelasting is groter dan Hallo-mogelijkheden van een individuele database
* Tenants mogelijk fysieke isolatie van elkaar, zodat de afzonderlijke databases nodig zijn voor elke tenant
* Verschillende secties van een database wellicht tooreside verschillende geografieën voor naleving, prestaties of geopolitieke redenen.

In andere scenario's, zoals de opname van gegevens van gedistribueerde apparaten worden sharding gebruikte toofill een set databases die tijdelijk zijn geordend. Bijvoorbeeld, kan een aparte database worden toegewezen tooeach dag of week. In dat geval kan Hallo sharding-sleutel een geheel getal dat Hallo datum (aanwezig is in alle rijen van de shard tabellen Hallo) en query's bij het ophalen van informatie voor een bepaald datumbereik moeten worden gerouteerd door Hallo toepassing toohello subset van de databases die betrekking hebben op Hallo bereik in vraag.

Sharding werkt het beste als elke transactie in een toepassing beperkt tooa worden kan enkele waarde van een sharding-sleutel. Dit zorgt ervoor dat alle transacties lokale tooa specifieke database worden.

## <a name="multi-tenant-and-single-tenant"></a>Multitenant- en één tenant
Sommige toepassingen gebruik Hallo eenvoudigste methode voor het maken van een aparte database voor elke tenant. Dit is Hallo **patroon voor één tenant sharding** die zorgt voor isolatie, de mogelijkheid back-up/herstel en resource schalen Hallo samenvattingen van Hallo tenant. Met één tenant sharding, elke database is gekoppeld aan een specifieke tenant-id-waarde (of waarde van de klant), maar die sleutel moet altijd bevinden zich in geen Hallo gegevens zelf. Het is van toepassing verantwoordelijkheid tooroute Hallo elke aanvraag toohello juiste database - en Hallo-clientbibliotheek kunt dit vereenvoudigen.

![Één tenant ten opzichte van meerdere tenants][4]

Andere scenario's voor meerdere tenants samen pack in de databases in plaats van ze te isoleren in afzonderlijke databases. Dit is een typische **multitenant sharding patroon** - en deze mag worden aangedreven door Hallo feit dat een toepassing grote aantallen zeer kleine tenants beheert. Hallo rijen in de databasetabellen Hallo zijn in de multitenant-sharding dat alle toocarry ontworpen een sleutel die identificeert Hallo-ID of sharding-tenantsleutel. Opnieuw Hallo toepassingslaag is verantwoordelijk voor het doorsturen van een tenant aanvraag toohello juiste database en dit kan worden ondersteund door het Hallo-clientbibliotheek voor elastische database. Bovendien mag beveiliging gebruikte toofilter welke rijen toegang elke tenant - voor meer informatie tot hebben Zie [multitenant-toepassingen met elastische database-hulpprogramma's en beveiliging](sql-database-elastic-tools-multi-tenant-row-level-security.md). Opnieuw distribueren van gegevens tussen databases zijn mogelijk vereist met Hallo multitenant sharding patroon en dit proces wordt vergemakkelijkt door Hallo elastische database gesplitste merge tool. Zie toolearn meer informatie over ontwerppatronen voor SaaS-toepassingen met elastische pools [ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Gegevens uit meerdere toosingle tenancymodus databases verplaatsen
Wanneer een SaaS-toepassing maakt, is het typische toooffer potentiële klanten een evaluatieversie van hello software. In dit geval is het rendabele toouse een multitenant-database voor Hallo-gegevens. Wanneer een kandidaat een klant wordt, is een één-tenant-database echter beter omdat deze betere prestaties biedt. Als klant Hallo had gemaakt van gegevens tijdens de proefperiode hello, gebruikt u Hallo [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md) toomove Hallo gegevens uit Hallo multitenant toohello nieuwe single-tenant-database.

## <a name="next-steps"></a>Volgende stappen
Zie voor een voorbeeld-app die u laat zien van de clientbibliotheek Hallo [aan de slag met hulpprogramma's van elastische Datababase](sql-database-elastic-scale-get-started.md).

tooconvert bestaande databases toouse Hallo-hulpprogramma's, Zie [tooscale-out migreren bestaande databases](sql-database-elastic-convert-to-use-elastic-tools.md).

toosee hello details van de elastische groep hello, Zie [prijs- en Prestatieoverwegingen voor een elastische pool](sql-database-elastic-pool.md), of maak een nieuwe pool met [elastische pools](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

