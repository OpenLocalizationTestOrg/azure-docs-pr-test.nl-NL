---
title: aaaAzure Cosmos DB resourcemodel en -concepten | Microsoft Docs
description: "Meer informatie over Azure Cosmos DB hiërarchische model van de databases, verzamelingen, door de gebruiker gedefinieerde functie (UDF), documenten, machtigingen toomanage bronnen en meer."
keywords: "Hiërarchische model cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Hiërarchisch bronmodel en basisconcepten voor Azure Cosmos DB
Hallo database entiteiten die Azure Cosmos DB beheert zijn waarnaar wordt verwezen tooas **resources**. Elke bron wordt uniek geïdentificeerd door een logische URI. U kunt met Hallo-resources met behulp van standaard HTTP-termen, aanvraag-/ antwoordheaders en statuscodes werken. 

Dit artikel leest, moet u kunnen tooanswer Hallo vragen te volgen:

* Wat is het resourcemodel Cosmos-database?
* Wat zijn resources gedefinieerd als bronnen in tegenstelling tot toouser gedefinieerd?
* Hoe ik een resource adresseren?
* Hoe werkt ik met verzamelingen?
* Hoe werkt ik met opgeslagen procedures, triggers en door de gebruiker gedefinieerde functies (UDF's)?

## <a name="hierarchical-resource-model"></a>Hiërarchische resourcemodel
Als hello volgende diagram ziet u, Hallo Cosmos DB hiërarchische **resourcemodel** bestaat uit sets van resources onder een databaseaccount elke adresseerbare via een logische en stabiele URI. Een set resources waarnaar wordt verwezen tooas worden een **feed** in dit artikel. 

> [!NOTE]
> Azure Cosmos DB biedt een zeer efficiënte TCP-protocol dat in het communicatiemodel via Hallo ook RESTful [DocumentDB .NET client-API](documentdb-sdk-dotnet.md).
> 
> 

![Azure hiërarchische resourcemodel Cosmos-DB][1]  
**Hiërarchische resourcemodel**   

toostart werken met resources, moet u [een databaseaccount maken](create-documentdb-dotnet.md) met behulp van uw Azure-abonnement. Een databaseaccount kan bestaan uit een reeks **databases**, elk met meerdere **verzamelingen**, elk van die op zijn beurt bevatten **opgeslagen procedures, triggers, UDF's, documenten**en verwante **bijlagen**. Een database ook gekoppelde **gebruikers**, elk met een reeks **machtigingen** tooaccess verzamelingen, opgeslagen procedures, triggers, UDF's, documenten of bijlagen. Hoewel databases, gebruikers, machtigingen en verzamelingen systeem gedefinieerde resources met bekende schema's, documenten en bijlagen bevatten echter willekeurige, gebruiker gedefinieerde JSON-inhoud.  

| Resource | Beschrijving |
| --- | --- |
| Databaseaccount |Een databaseaccount is gekoppeld aan een set databases en een vast bedrag van blob-opslag voor bijlagen. U kunt een of meer database accounts met behulp van uw Azure-abonnement maken. Ga voor meer informatie naar onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Database |Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen. Het is ook een gebruikerscontainer. |
| Gebruiker |Hallo logische naamruimte voor het vaststellen van machtigingen. |
| Machtiging |Een verificatietoken die zijn gekoppeld aan een gebruiker voor toegang tot tooa bepaalde resource. |
| Verzameling |Een verzameling is een container van JSON-documenten en Hallo bijbehorende JavaScript-toepassingslogica. Een verzameling is een factureerbare entiteit waar hello [kosten](performance-levels.md) wordt bepaald door het prestatieniveau Hallo Hallo verzameling gekoppeld. Verzamelingen kunnen een of meer partities/servers omvatten en kunnen worden geschaald toohandle vrijwel onbeperkte hoeveelheid opslag of doorvoer. |
| Opgeslagen procedure |De toepassingslogica is geschreven in JavaScript die is geregistreerd bij een verzameling en transactioneel uitgevoerd binnen Hallo database-engine. |
| Trigger |Toepassingslogica geschreven in JavaScript uitgevoerd vóór of na een invoeging vervangen of verwijderen. |
| UDF |Geschreven in JavaScript-toepassingslogica. UDF's inschakelen toomodel een aangepaste query-operator en waardoor Hallo core DocumentDB API-querytaal uit te breiden. |
| Document |De gebruiker gedefinieerde (willekeurige) JSON-inhoud. Er is geen schema moet toobe gedefinieerd standaard noch secundaire indexen hoeft toobe opgegeven voor alle Hallo documenten tooa verzameling toegevoegd. |
| Bijlage |Een bijlage is een speciale document met verwijzingen en gekoppelde metagegevens voor externe-blob/media. Hallo developer toohave Hallo blob beheerd door Cosmos DB of kies opslaan met een externe blob-provider zoals OneDrive, Dropbox, enz. |

## <a name="system-vs-user-defined-resources"></a>Systeem versus door de gebruiker gedefinieerde resources
Resources zoals database accounts, databases, verzamelingen, gebruikers, machtigingen, opgeslagen procedures, triggers en UDF - alle hebben een vaste schema en systeembronnen worden genoemd. Daarentegen resources, zoals documenten en bijlagen geldt geen beperking op Hallo schema en zijn voorbeelden van de gebruiker gedefinieerde resources. In Cosmos DB, systeem- en gebruiker gedefinieerde resources weergegeven en beheerd als standaard-compatibele JSON. Alle resources, het systeem of door de gebruiker gedefinieerde, hebben Hallo volgende algemene eigenschappen.

> [!NOTE]
> Opmerking dat alle eigenschappen in een resource gegenereerd worden voorafgegaan door een onderstrepingsteken (_) in de JSON-weergave.
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>Eigenschap</strong></p></td>
            <td valign="top"><p><strong>Gebruiker worden ingesteld of het systeem gegenereerde?</strong></p></td>
            <td valign="top"><p><strong>Doel</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>Systeem gegenereerde</p></td>
            <td valign="top"><p>Het systeem gegenereerde, unieke en hiërarchische-id van Hallo resource</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Systeem gegenereerde</p></td>
            <td valign="top"><p>ETag van Hallo-bron die vereist is voor Optimistisch gelijktijdigheidbeheer</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Systeem gegenereerde</p></td>
            <td valign="top"><p>Tijdstempel voor laatste bijgewerkte van Hallo resource</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Systeem gegenereerde</p></td>
            <td valign="top"><p>Unieke adresseerbare URI van Hallo resource</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>Systeem gegenereerde</p></td>
            <td valign="top"><p>De unieke naam van Hallo resource gedefinieerd door de gebruiker (dezelfde partitie Hello sleutelwaarde). Als het Hallo-gebruiker geeft niet een id, een id wordt het systeem worden gegenereerd</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Lijnweergave van resources
Cosmos DB schrijft niet voor een eigen uitbreidingen toohello JSON standard of speciale coderingen; Dit proces werkt met standaard compatibele JSON-documenten.  

### <a name="addressing-a-resource"></a>Een resource adressering
Alle resources zijn adresseerbare URI. waarde van Hallo Hallo **_self** eigenschap van een resource vertegenwoordigt de relatieve URI van de resource Hallo Hallo. Hallo Hallo URI bestaan uit Hallo /\<feed\>/ padsegmenten {_rid}:  

| Waarde van Hallo _self | Beschrijving |
| --- | --- |
| /DBS |Feed van databases onder een databaseaccount |
| /DBS/ {dbName} |Database met een id die overeenkomt met de Hallo waarde {dbName} |
| /colls/ /DBS/ {dbName} |Feed van verzamelingen onder een database |
| /DBS/ {dbName} /colls/ {collName} |De verzameling met een id die overeenkomt met de Hallo waarde {collName} |
| /DBS/ {dbName} /colls/ {collName} / docs |Feed van documenten in een verzameling |
| /DBS/ {dbName} /colls/ {collName} /docs/ {docId} |Document met een id die overeenkomt met de Hallo waarde {doc} |
| /gebruikers/ /DBS/ {dbName} |Feed gebruikers onder een database |
| /DBS/ {dbName} /gebruikers/ {userId} |Gebruiker met een id die overeenkomt met de Hallo waarde {user} |
| /DBS/ {dbName} /gebruikers/ {userId} / machtigingen |Feed machtigingen onder een gebruikersaccount |
| /DBS/ {dbName} /gebruikers/ {userId} /permissions/ {permissionId} |Machtiging met een id die overeenkomt met de Hallo waarde {machtiging} |

Elke resource heeft een unieke door de gebruiker gedefinieerde naam beschikbaar gesteld via de eigenschap id Hallo. Opmerking: voor documenten, als Hallo gebruiker niet een id geeft onze ondersteunde SDK's wordt automatisch gegenereerd een unieke id voor het Hallo-document. Hallo-id is een tekenreeks door de gebruiker gedefinieerde van maximaal too256 tekens die uniek is binnen het Hallo-context van een specifieke bovenliggende resource is. 

Elke resource heeft ook een systeem gegenereerde hiërarchische resource-id (ook waarnaar wordt verwezen tooas een RID), die beschikbaar zijn via Hallo _rid eigenschap is. Hallo RID codeert Hallo gehele hiërarchie van een bepaalde bron en het is dat een handige interne weergave tooenforce referentiële integriteit in een gedistribueerde manier gebruikt. Hallo RID uniek is binnen een databaseaccount en wordt intern gebruikt door Cosmos DB voor efficiënte routering zonder cross partitie zoekacties. Hallo-waarden van Hallo _self en Hallo _rid eigenschappen zijn alternatieve en canonieke vorm van een resource. 

Hallo REST-API's ondersteuning van resources adressering en routering van aanvragen door Hallo-id en Hallo _rid eigenschappen.

## <a name="database-accounts"></a>Database-accounts
U kunt een of meer Cosmos DB database accounts met behulp van uw Azure-abonnement inrichten.

U kunt maken en beheren van de Cosmos-DB database accounts via hello Azure-Portal op [http://portal.azure.com/](https://portal.azure.com/). Maken en beheren van een databaseaccount beheerderstoegang vereist en kan alleen worden uitgevoerd onder uw Azure-abonnement. 

### <a name="database-account-properties"></a>Eigenschappen van de database-account
Als onderdeel van het inrichten en beheren van een databaseaccount kunt u configureren en lezen Hallo volgende eigenschappen:  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>De naam van eigenschap</strong></p></td>
            <td valign="top"><p><strong>Beschrijving</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Consistentie beleid</p></td>
            <td valign="top"><p>Stel deze eigenschap tooconfigure-Hallo standaardniveau consistentie voor alle Hallo verzamelingen onder de databaseaccount van uw. U kunt Hallo consistentieniveau per aanvraag op basis van een aanvraagheader Hallo [x-ms-consistentie-niveau] met overschrijven. <p><p>Deze eigenschap geldt alleen toohello Opmerking <i>door de gebruiker gedefinieerde resources</i>. Alle door het systeem gedefinieerde resources zijn geconfigureerde toosupport leesbewerkingen/query's met sterke consistentie.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Autorisatie-sleutels</p></td>
            <td valign="top"><p>Dit zijn Hallo primaire en secundaire sleutels hoofd- en alleen-lezen die beheerdersrechten bieden toegang tot tooall van Hallo resources onder Hallo databaseaccount.</p></td>
        </tr>
    </tbody>
</table>

In aanvulling tooprovisioning, configureren en beheren van uw databaseaccount van hello Azure-Portal, u kunt ook programmatisch maken en Cosmos DB database accounts beheren met behulp van Hallo [Azure Cosmos DB REST API's](/rest/api/documentdb/) als alsmede [client-SDK's](documentdb-sdk-dotnet.md).  

## <a name="databases"></a>Databases
Een Cosmos-DB-database is een logische container voor een of meer verzamelingen en gebruikers, zoals wordt weergegeven in het volgende diagram Hallo. U kunt een willekeurig aantal databases onder een Cosmos-DB database account onderwerp toooffer grenzen maken.  

![Account en verzamelingen hiërarchische databasemodel][2]  
**Een Database is een logische container van gebruikers en verzamelingen**

Een database kan vrijwel onbeperkte documentopslag, gepartitioneerd in verzamelingen bevatten.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Elastisch schalen van een database van de Cosmos-DB
Een Cosmos-DB-database is elastisch standaard – variërend van een paar GB toopetabytes van SSD back documentopslag en ingerichte doorvoer. 

In tegenstelling tot een database in traditionele RDBMS is een database in Cosmos DB niet binnen het bereik tooa enkele machine. Met Cosmos DB, zoals de schaal van uw toepassing toogrow moet, kunt u meer verzamelingen, databases, of beide. Inderdaad hebt verschillende toepassingen in de eerste leveranciers binnen Microsoft gebruikt Cosmos-database op een schaal van de consument door te maken van zeer grote databases van de Cosmos-DB elke met duizenden verzamelingen met terabytes aan opslag van documenten. U kunt vergroten of verkleinen van een database door toe te voegen of te verwijderen van verzamelingen toomeet schaal van uw toepassing. 

U kunt een willekeurig aantal verzamelingen binnen een database onderwerp toohello aanbieding maken. Elke verzameling heeft back SSD-opslag en u afhankelijk van de geselecteerde prestatielaag Hallo ingerichte doorvoer.

Een Cosmos-DB-database is ook een container van gebruikers. Een gebruiker, beurt, is een logische naamruimte voor een reeks machtigingen die fijnmazig toocollections voor verificatie en toegangsbeheer, documenten en bijlagen voorziet.  

Zoals met andere bronnen in Hallo Cosmos DB resourcemodel, databases kunnen worden gemaakt, vervangen, verwijderd, lezen of opgesomd heel eenvoudig met beide Hallo [REST-API's](/rest/api/documentdb/) of een Hallo [client-SDK's](documentdb-sdk-dotnet.md). Cosmos DB garandeert een sterke consistentie voor lezen en het Hallo-metagegevens van een resource database opvragen. Een database wordt automatisch verwijderd, zorgt u ervoor dat u geen toegang Hallo verzamelingen of gebruikers die zich daarin tot.   

## <a name="collections"></a>Verzamelingen
Een Cosmos-DB-verzameling is een container voor uw JSON-documenten. 

### <a name="elastic-ssd-backed-document-storage"></a>Elastische SSD back-documentopslag
Er is een verzameling intrinsiek elastische - en deze automatisch groeit kleiner naarmate u documenten toevoegen of verwijderen. Verzamelingen zijn logische resources en kunnen een of meer fysieke partities of servers omvatten. Hallo aantal partities binnen een verzameling wordt bepaald op basis van Hallo opslaggrootte en ingerichte doorvoer van uw verzameling Hallo Cosmos-DB. Elke partitie in Cosmos-database heeft een vaste hoeveelheid back SSD opslag gekoppeld en is gerepliceerd voor hoge beschikbaarheid. Partitie management volledig wordt beheerd door Azure Cosmos DB, en u niet hebt toowrite complexe code of beheren van uw partities. Cosmos DB verzamelingen zijn **vrijwel onbeperkte** in termen van opslag en doorvoer. 

### <a name="automatic-indexing-of-collections"></a>Automatische indexering van verzamelingen
Cosmos DB is een databasesysteem waar zonder schema. Het niet wordt ervan uitgegaan dat of een schema voor Hallo JSON-documenten nodig. Als u documenten tooa verzameling toevoegt, Cosmos DB automatisch geïndexeerd en ze beschikbaar zijn voor u tooquery. Automatische indexering van documenten zonder schema of secundaire indexen is een belangrijke functie van Cosmos-database en wordt ingeschakeld door schrijven geoptimaliseerd, vergrendeling vrij en logboek gestructureerd index onderhoud technieken. Cosmos DB ondersteunt volgehouden volume zeer snel schrijfbewerkingen tijdens afhandeling van nog steeds consistente query's. Zowel document als index opslag zijn toocalculate Hallo opslagruimte is verbruikt door elke verzameling hebt gebruikt. U kunt beheren Hallo opslag en prestaties verschillen die zijn gekoppeld aan het indexeren door Hallo indexeringsbeleid voor een verzameling configureren. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>Hallo indexeringsbeleid van een verzameling configureren
Hallo indexeren beleid van elke verzameling kunt u toomake prestaties en opslag-en nadelen die zijn gekoppeld aan het indexeren. Hallo zijn volgende opties beschikbaar tooyou als onderdeel van de indexing-configuratie:  

* Kies of Hallo verzameling automatisch alle documenten Hallo of niet indexeert. Alle documenten worden standaard automatisch geïndexeerd. U kunt kiezen tooturn automatische indexering uitgeschakeld en alleen bepaalde documenten toohello index selectief toevoegen. Als u daarentegen, kunt u selectief kiezen tooexclude alleen bepaalde documenten. Dit doet u door het instellen van Hallo automatische eigenschap toobe waar of onwaar op Hallo indexingPolicy van een verzameling en de aanvraagheader Hallo [x-ms-indexingdirective] tijdens het invoegen, vervangen of een document verwijderen.  
* Kies of tooinclude of uitsluiten van specifieke paden of patronen in uw documenten van Hallo index. U kunt dit doen door de instelling includedPaths en excludedPaths op Hallo indexingPolicy van een verzameling respectievelijk. Ook kunt u configureren Hallo opslag en prestaties-en nadelen voor bereik en hash-query's voor een specifiek pad patronen. 
* Kiezen tussen synchrone (consistent) en indexupdates van asynchrone (lazy). Hallo-index wordt standaard synchroon bijgewerkt op elke invoegen, vervangen of verwijderen van een document toohello-verzameling. Hierdoor kunnen query's Hallo toohonor Hallo dezelfde consistentieniveau als die van Hallo document leest. Hoewel Cosmos DB geoptimaliseerd voor schrijven is en volgehouden volumes van document schrijfbewerkingen samen met synchrone index onderhoud ten behoeve van consistente query's ondersteunt, kunt u bepaalde tooupdate verzamelingen de index traag. Vertraagde indexeren verhoogt de schrijfprestaties verdere Hallo en is ideaal voor bulksgewijs opname scenario's voor voornamelijk lezen zware verzamelingen.

Hallo indexeren beleid kan worden gewijzigd door het uitvoeren van een PUT op Hallo-verzameling. Dit kan worden bereikt via Hallo [client SDK](documentdb-sdk-dotnet.md), Hallo [Azure Portal](https://portal.azure.com) of Hallo [REST-API's](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Opvragen van een verzameling
Hallo documenten binnen een verzameling kunnen willekeurige schema's en u kunt documenten binnen een verzameling query zonder op te geven van een schema of secundaire indexen tevoren betaalt. U kunt een query Hallo verzameling op basis van Hallo [Azure Cosmos DB DocumentDB-API: naslaginformatie voor SQL-syntaxis](https://msdn.microsoft.com/library/azure/dn782250.aspx), waarmee u uitgebreide hiërarchische, ruimtelijke en relationele operators en uitbreidingsmogelijkheden via UDF's op basis van JavaScript. JSON-grammatica biedt de mogelijkheid voor het modelleren van JSON-documenten als structuren met labels als structuurknooppunten Hallo. Dit is zowel door automatische indexering technieken DocumentDB-API, evenals een van de API van de DocumentDB SQL-dialect misbruikt. Hallo querytaal DocumetDB API bestaat uit drie belangrijkste aspecten:   

1. Een kleine set van querybewerkingen die zijn toegewezen natuurlijk toohello-boomstructuur met inbegrip van hiërarchische query's en projecties. 
2. Een subset van relationele bewerkingen inclusief samenstelling, filter, projecties, statistische functies en self joins. 
3. Pure JavaScript gebaseerd UDF's die met werken (1) en (2).  

Hallo Cosmos DB querymodel probeert toostrike een evenwicht tussen functionaliteit, efficiëntie en eenvoud. Hallo Cosmos DB database-engine systeemeigen compileert en Hallo SQL-query-instructies worden uitgevoerd. U kunt een verzameling met Hallo query [REST-API's](/rest/api/documentdb/) of een Hallo [client-SDK's](documentdb-sdk-dotnet.md). Hallo .NET SDK wordt geleverd met een LINQ-provider.

> [!TIP]
> U kunt Hallo DocumentDB API uitproberen en SQL-query's uitvoeren op onze gegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Transacties met meerdere documenten
Databasetransacties bieden een veilige en voorspelbare programmeermodel voor het omgaan met gelijktijdige wijzigingen toohello gegevens. In RDBMS, is het Hallo traditionele manier toowrite bedrijfslogica toowrite **opgeslagen procedures** en/of **triggers** en verzendt het toohello-databaseserver voor de transactionele uitvoering. Hallo toepassing programmeurs is in RDBMS, vereist toodeal met twee verschillende programmeertalen: 

* programmeertaal van de toepassing hello (niet-transactionele) (zoals JavaScript, Python, C#, Java, enz.)
* T-SQL, Hallo transactionele programmeertaal die standaard wordt uitgevoerd door Hallo-database

Doordat de grondige streven tooJavaScript en JSON rechtstreeks in de database-engine Hallo Cosmos DB biedt een intuïtieve programmeermodel voor uitvoerende JavaScript-toepassingslogica rechtstreeks gebaseerd op Hallo verzamelingen in termen van opgeslagen procedures en Triggers. Hiermee kunt u beide Hallo volgende:

* Efficiënte implementatie van gelijktijdigheid van taken worden beheerd, herstel, automatische indexering van Hallo JSON objectgrafieken rechtstreeks in de database-engine Hallo
* Natuurlijk uitdrukken Controlestroom, variabele scoping, toewijzing en integratie van primitieven met databasetransacties rechtstreeks in termen van Hallo JavaScript programmeertaal uitzonderingsverwerking

Hallo JavaScript-logica geregistreerd op het niveau van een verzameling kan databasebewerkingen uitvoeren op Hallo documenten Hallo gegeven verzameling vervolgens uitgeven. Cosmos DB impliciet terugloopt Hallo die JavaScript op basis van opgeslagen procedures en triggers binnen een ambient ACID-transactions met snapshot-isolatie tussen documenten binnen een verzameling. In de loop Hallo van de uitvoering ervan, als JavaScript genereert een uitzondering Hallo Hallo vervolgens hele transactie is afgebroken. Hallo resulterende programmeermodel is een zeer eenvoudige maar krachtige. JavaScript-ontwikkelaars ophalen een 'duurzame' programmeermodel terwijl u ook hun bekend taalconstructs en bibliotheek primitieven   

Hallo mogelijkheid tooexecute JavaScript rechtstreeks in het Hallo-database-engine in het Hallo dezelfde adresruimte zoals Hallo buffergroep zodat en transactionele uitvoering van de activiteiten van de database op Hallo documenten van een verzameling maakt. Bovendien Cosmos DB database-engine maakt een grondige streven toohello JSON en JavaScript elimineert impedantie niet overeenkomen tussen Hallo type systemen van toepassing en het Hallo-database.   

Na het maken van een verzameling, kunt u opgeslagen procedures, triggers en UDF's registreren met een verzameling met Hallo [REST-API's](/rest/api/documentdb/) of een Hallo [client-SDK's](documentdb-sdk-dotnet.md). U kunt verwijzen naar en ze worden uitgevoerd na de registratie. Houd rekening met Hallo volgende opgeslagen procedure is geschreven in JavaScript, volledig Hallo-code hieronder worden twee argumenten (naam en de naam van auteur) en maakt een nieuw document, query's voor een document en werkt vervolgens het – alle binnen een impliciete ACID-transactie. Op elk moment tijdens de uitvoering van Hallo als een JavaScript-uitzondering is opgetreden, annuleert de hele transactie Hallo.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

Hallo-client kan 'verzenden' hello hierboven JavaScript-logica toohello database voor de transactionele uitvoering via HTTP POST. Zie voor meer informatie over het gebruik van HTTP-methoden [RESTful interacties met Azure Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx). 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


U ziet dat omdat Hallo database systeemeigen JSON en JavaScript begrijpt, er is geen niet-overeenkomend gegevenstype system, geen 'OR toewijzing' of code generatie magic vereist.   

Opgeslagen procedures en triggers communiceren met een verzameling en het Hallo-documenten in een verzameling via een goed gedefinieerde objectmodel, waarmee de huidige verzameling context Hallo.  

Verzamelingen in Hallo DocumentDB API kan worden gemaakt, verwijderd, lees- of opgesomd heel eenvoudig met beide Hallo [REST-API's](/rest/api/documentdb/) of een Hallo [client-SDK's](documentdb-sdk-dotnet.md). Hallo DocumentDB API biedt altijd sterke consistentie voor lezen of het uitvoeren van query's Hallo metagegevens van een verzameling. Als u een verzameling verwijdert, wordt automatisch zorgt ervoor dat u geen toegang documenten hello, bijlagen, opgeslagen procedures, triggers tot en UDF's daarin.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Opgeslagen procedures, triggers en de gebruiker gedefinieerde functies (UDF)
Zoals beschreven in de vorige sectie hello, kunt u de toepassing logica toorun rechtstreeks binnen een transactie in database-engine Hallo schrijven. Hallo-toepassingslogica volledig in JavaScript kan worden geschreven en kan worden gemodelleerd als een opgeslagen procedure, trigger of een UDF. Hallo JavaScript-code binnen een opgeslagen procedure of een trigger kunt invoegen, vervangen, lees- of documenten binnen een verzameling verwijderen. Op Hallo daarentegen, Hallo JavaScript binnen een UDF kan niet invoegen, vervangen of verwijderen van documenten. UDF's Hallo documenten van de resultatenset van een query inventariseren en produceren van een andere resultatenset. Cosmos DB afgedwongen voor multitenancy, een strikte reservering op basis van resource governance. Elk opgeslagen procedure, trigger of een UDF haalt een vaste quantum van besturingssysteem resources toodo het werk. Bovendien opgeslagen procedures, triggers of UDF's kunnen geen koppeling tegen externe JavaScript-bibliotheken en zijn gebeurd als ze Hallo resource budgetten toegewezen toothem overschrijdt. U kunt registreren, hef de registratie van opgeslagen procedures, triggers of UDF's met een verzameling met behulp van Hallo REST-API's.  Bij de registratie een opgeslagen procedure, trigger of een UDF vooraf gecompileerd en opgeslagen als de code van de bytes die later wordt uitgevoerd. Hallo volgende sectie laten zien hoe u kunt gebruiken Hallo Cosmos DB JavaScript SDK tooregister, uitvoeren, en hef de registratie van een opgeslagen procedure, trigger en een UDF. Hallo JavaScript SDK is een eenvoudige wrapper via Hallo [REST-API's](/rest/api/documentdb/). 

### <a name="registering-a-stored-procedure"></a>Registreren van een opgeslagen procedure
De registratie van een opgeslagen procedure maakt een nieuwe resource van de opgeslagen procedure op een verzameling via HTTP POST.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>Uitvoeren van een opgeslagen procedure
Uitvoering van een opgeslagen procedure wordt gedaan door uitgifte van een HTTP POST op basis van een bestaande resource in de opgeslagen procedure door de parameters in de aanvraagtekst Hallo toohello procedure doorgeven.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>De registratie van een opgeslagen procedure
De registratie van een opgeslagen procedure wordt gewoon door uitgifte van een HTTP DELETE op basis van een bestaande resource in de opgeslagen procedure uitgevoerd.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>Registratie van een vooraf trigger
De registratie van een trigger wordt uitgevoerd door een nieuwe trigger-resource maken in een verzameling via HTTP POST. U kunt opgeven dat het Hallo trigger een vooraf is of een post-trigger en Hallo type bewerking kan het worden gekoppeld aan (bijvoorbeeld maken, Replace, Delete of alle).   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>Uitvoeren van een vooraf trigger
Uitvoering van een trigger wordt gedaan door te geven Hallo-naam van een bestaande trigger gelijktijdig Hallo met verzenden Hallo POST, PUT, verwijderen van een documentbron via de aanvraagheader Hallo.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>De registratie van een vooraf trigger
De registratie van een trigger wordt gewoon uitgevoerd via het uitgeven van een HTTP DELETE op basis van een bestaande trigger-resource.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>Registreren van een UDF
De registratie van een UDF wordt uitgevoerd door een nieuwe UDF-resource maken in een verzameling via HTTP POST.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>Een UDF als onderdeel van Hallo query uitvoeren
Een UDF kan worden opgegeven als onderdeel van de SQL-query Hallo en wordt gebruikt als een manier tooextend Hallo core [SQL-querytaal voor Hallo DocumentDB API](https://msdn.microsoft.com/library/azure/dn782250.aspx).

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>De registratie van een UDF
De registratie van een UDF gebeurt gewoon door uitgifte van een HTTP DELETE op basis van een bestaande UDF-resource.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

Hoewel Hallo codefragmenten bovenstaande Hallo-registratie (POST), registratie (PUT), lezen/lijst (GET) en uit te voeren (POST) via Hallo [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), u kunt ook Hallo [REST-API's](/rest/api/documentdb/) of andere [client-SDK's](documentdb-sdk-dotnet.md). 

## <a name="documents"></a>Documenten
U kunt invoegen, vervangen, verwijderen, lezen, opsommen en willekeurige JSON-documenten in een verzameling opvragen. Cosmos DB schrijft geen schema niet en vereist geen secundaire indexen in volgorde toosupport opvragen over documenten in een verzameling. Hallo maximale grootte voor een document is 2 MB.   

Wordt een echt geopende database-service, Cosmos-database komt niet voor voorraad eventuele speciale gegevenstypen (bijvoorbeeld een datum-tijd) of specifieke coderingen voor JSON-documenten. Houd er rekening mee dat er geen speciale JSON conventies toocodify Hallo relaties tussen verschillende documenten; is vereist voor Cosmos-DB Hallo SQL-syntaxis van de Cosmos-DB biedt krachtige query van hiërarchische en relationele operators tooquery en project documenten zonder speciale aantekeningen of nodig toocodify relaties tussen documenten met behulp van de eigenschappen van DN.  

Als u documenten kunnen worden gemaakt met alle andere resources, vervangen, verwijderd, lezen, geïnventariseerd en opgevraagd eenvoudig met REST-API's of een van de Hallo [client-SDK's](documentdb-sdk-dotnet.md). Verwijderen van een document onmiddellijk vrijgemaakt Hallo quotum bijbehorende tooall Hallo genest bijlagen. Hallo lezen consistentieniveau van documenten volgt Hallo consistentie beleid op Hallo databaseaccount. Dit beleid kan worden genegeerd op basis van per aanvraag, afhankelijk van de gegevens consistent vereisten van uw toepassing. Tijdens het opvragen van de documenten lezen Hallo consistentie volgt Hallo modus die is ingesteld op Hallo verzameling te indexeren. Dit volgt Hallo-account consistentie beleid voor 'consistent'. 

## <a name="attachments-and-media"></a>Bijlagen en media
Cosmos DB kunt u toostore binaire blobs/media met Cosmos-DB (maximaal 2 GB per account) of tooyour eigen externe mediastore. U kunt er ook toorepresent Hallo metagegevens van een medium in termen van een speciale document met de naam van de bijlage. Een bijlage van de Cosmos-database is een speciale (JSON)-document dat verwijzingen Hallo media/blob elders opgeslagen. Een bijlage is gewoon een speciale document waarmee Hallo metagegevens (zoals locatie, auteur enz.) van een media opgeslagen in een externe Mediaopslag wordt vastgelegd. 

U kunt een toepassing van sociale lezen die gebruikmaakt van aantekeningen Cosmos-DB-toostore en metagegevens, opmerkingen, waaronder markeert, bladwijzers, classificaties, enz. gekoppelde voor een e-book van een bepaalde gebruiker alsof/ervaringen.   

* Hallo inhoud van het Hallo-adresboek zelf wordt opgeslagen in Hallo Mediaopslag ofwel beschikbaar als onderdeel van de Cosmos-DB-databaseaccount of een externe mediastore. 
* Een toepassing kan elke gebruiker metagegevens opslaan als een afzonderlijke document--bijvoorbeeld Jan van metagegevens voor Map1 worden opgeslagen in een document waarnaar wordt verwezen door /colls/joe/docs/book1. 
* Bijlagen wijzen toohello inhoudspagina's van een bepaalde boek van een gebruiker worden opgeslagen onder Hallo bijbehorende document bijvoorbeeld /colls/joe/docs/book1/chapter1 /colls/joe/docs/book1/chapter2 enzovoort. 

Let op: Hallo voorbeelden hierboven vermelde beschrijvende-ID's tooconvey Hallo resource hiërarchie gebruiken. Bronnen worden geopend via Hallo REST-API's via unieke resource-id. 

Hallo-media die wordt beheerd door Cosmos DB, wordt Hallo _media eigenschap van Hallo bijlage verwijst naar Hallo media door de URI. Cosmos DB ervoor toogarbage verzamelen Hallo media wanneer alle Hallo uitstaande verwijzingen worden verwijderd. Cosmos DB Hallo bijlage wordt gegenereerd tijdens het uploaden van de nieuwe media Hallo automatisch en wordt gevuld Hallo _media toopoint toohello toegevoegde media. Als u kiest toostore Hallo media in een externe blob-opslag beheerd door uzelf (zoals OneDrive, Azure Storage DropBox enz.), kunt u nog steeds bijlagen tooreference Hallo media. In dit geval u Hallo bijlage zelf maken en vullen van de eigenschap _media.   

Net als bij alle andere resources, bijlagen kunnen worden gemaakt, vervangen, verwijderd, lees- of opgesomd eenvoudig met behulp van REST-API's of een van de Hallo client-SDK's. Met documenten, Hallo consistentieniveau van bijlagen gelezen volgt Hallo consistentie beleid op Hallo databaseaccount. Dit beleid kan worden genegeerd op basis van per aanvraag, afhankelijk van de gegevens consistent vereisten van uw toepassing. Bij het opvragen van bijlagen, lezen Hallo consistentie volgt Hallo modus die is ingesteld op Hallo verzameling te indexeren. Dit volgt Hallo-account consistentie beleid voor 'consistent'. 
 

## <a name="users"></a>Gebruikers
Een gebruiker Cosmos DB vertegenwoordigt een logische naamruimte voor het groeperen van machtigingen. Een Cosmos-DB-gebruiker kan tooa gebruiker in een identiteitsbeheersysteem of een vooraf gedefinieerde toepassingsrol overeenkomen. Voor Cosmos-DB vertegenwoordigt een gebruiker gewoon een abstractie toogroup een reeks machtigingen onder een database.   

Voor het implementeren van multi-tenancymodus in uw toepassing, kunt u gebruikers in Cosmos-database die overeenkomt met de werkelijke gebruikers tooyour of Hallo tenants van uw toepassing. Vervolgens kunt u machtigingen voor een bepaalde gebruiker die overeenkomen met toohello toegangsbeheer via verschillende verzamelingen, documenten, bijlagen, enzovoort.   

Als uw toepassingen nodig tooscale met de groei van uw gebruiker, kunt u verschillende manieren tooshard uw gegevens vast. U kunt een model van elk van uw gebruikers als volgt:   

* Elke gebruiker maps tooa database.
* Elke gebruiker maps tooa verzameling. 
* Bijbehorende toomultiple gebruikers documenten gaat tooa toegewezen verzameling. 
* Bijbehorende toomultiple gebruikers documenten gaat tooa set van verzamelingen.   

Ongeacht Hallo specifieke sharding-strategie die u kiest, kunt u uw werkelijke gebruikers als gebruikers in de database van de Cosmos-DB model en fijn gedetailleerde machtigingen tooeach gebruiker koppelen.  

![Verzamelingen van gebruikers][3]  
**Sharding-strategieën en modellering gebruikers**

Net als alle andere resources, gebruikers in Cosmos-database kunnen worden gemaakt, vervangen, verwijderd, lezen of opgesomd eenvoudig met behulp van REST-API's of een van de Hallo client-SDK's. Cosmos DB geeft altijd sterke consistentie voor lezen of het uitvoeren van query's Hallo metagegevens van een gebruiker een resource. Wordt het bewerken van wijzen op of verwijdering van een gebruiker automatisch zorgt ervoor dat u geen toegang Hallo machtigingen erin opgenomen tot. Hoewel Hallo Cosmos DB indexrijen Hallo quotum van Hallo machtigingen als onderdeel van de gebruiker op de achtergrond Hallo Hallo verwijderd, Hallo verwijderd machtigingen is onmiddellijk beschikbaar opnieuw voor u toouse.  

## <a name="permissions"></a>Machtigingen
Vanuit een access control-perspectief wordt resources, zoals accounts, database, databases, gebruikers en machtigingen worden beschouwd als *beheerdersrechten* bronnen omdat deze is vereist voor beheerdersmachtigingen nodig. Op Hallo daarentegen resources inclusief Hallo verzamelingen, documenten, bijlagen, opgeslagen procedures, triggers, UDF's zijn en onder een bepaalde database scoped en beschouwd als *toepassingsresources*. Hallo autorisatie model overeenkomt toohello twee typen resources en het Hallo-functies die toegang deze (namelijk Hallo beheerder en gebruiker tot), definieert twee soorten *toegangssleutels*: *hoofdsleutel* en *bronsleutel*. Hallo-hoofdsleutel is een onderdeel van het databaseaccount Hallo en wordt aangeboden toohello ontwikkelaars (of beheerder) die Hallo databaseaccount is ingericht. Deze hoofdsleutel heeft administrator-semantiek in dat het gebruikte tooauthorize toegang tooboth administratieve en toepassingsbronnen kan zijn. Een resource-sleutel is daarentegen een gedetailleerde toegangssleutel waarmee toegang tooa *specifieke* toepassingsbron. Hallo-relatie tussen Hallo gebruiker van een database worden vastgelegd en dus Hallo machtigingen Hallo gebruiker heeft voor een specifieke bron (bijvoorbeeld verzameling, document, bijlage, opgeslagen procedure, trigger of UDF).   

Hallo alleen manier tooobtain die een resource-sleutel is door het maken van een machtiging bron op onder een bepaalde gebruiker. Houd er rekening mee dat In de volgorde toocreate of een machtiging voor het ophalen, een hoofdsleutel in Hallo autorisatie-header moet worden gepresenteerd. Een machtiging resource ties Hallo resource, de toegang en Hallo gebruiker. Na het maken van een resource machtiging moet Hallo gebruiker alleen toopresent Hallo gekoppeld bronsleutel in volgorde toogain toegang toohello relevante resource. Daarom kan de sleutel van een resource worden weergegeven als een logische en compact representatie van Hallo machtiging resource.  

Net als bij alle andere resources, machtigingen in Cosmos-database kunnen worden gemaakt, vervangen, verwijderd, lees- of opgesomd eenvoudig met behulp van REST-API's of een van de Hallo client-SDK's. Cosmos DB geeft altijd sterke consistentie voor lezen of Hallo metagegevens van een machtiging voor het uitvoeren van query's. 

## <a name="next-steps"></a>Volgende stappen
Meer informatie over het werken met resources met behulp van HTTP-opdrachten in [RESTful interacties met bronnen Cosmos DB](https://msdn.microsoft.com/library/azure/mt622086.aspx).

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

