---
title: Tips voor betere prestaties - Azure Cosmos DB NoSQL | Microsoft Docs
description: Meer informatie over client-configuratieopties voor het verbeteren van de prestaties van Azure DB die Cosmos-database
keywords: voor de verbetering van prestaties van de database
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: a94cda90eca9dca2b93adb8f5091d829e7375aa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Tips voor betere prestaties voor Azure Cosmos-DB
Azure Cosmos-database is een snelle en flexibele gedistribueerde database waarin naadloos met gegarandeerde latentie en doorvoer schaalt. U beschikt niet over belangrijke architectuur wijzigen of complexe code schrijven om te schalen van uw database met Cosmos-DB. Omhoog en omlaag schalen is net zo eenvoudig als het maken van één API-aanroep of [SDK-aanroep van methode](set-throughput.md#set-throughput-sdk). Omdat Cosmos DB wordt benaderd via het netwerk aanroepen zijn er echter clientzijde optimalisaties die voor optimale prestaties kunt u.

Dus als u vraagt "hoe kan ik mijn de databaseprestaties verbeteren?" Houd rekening met de volgende opties:

## <a name="networking"></a>Netwerken
<a id="direct-connection"></a>

1. **Verbindingsbeleid: de modus rechtstreekse verbinding gebruiken**

    Hoe een client verbinding maakt met Cosmos-DB heeft belangrijke gevolgen voor de prestaties, met name in termen van waargenomen-clientzijde latentie. Er zijn twee belangrijke configuratie-instellingen beschikbaar zijn voor het configureren van client verbindingsbeleid – de verbinding *modus* en de [verbinding *protocol*](#connection-protocol).  De twee modi beschikbaar zijn:

   1. Gateway-modus (standaard)
   2. Directe modus

      Gateway-modus wordt ondersteund op alle platforms van de SDK en de geconfigureerde standaardwaarde is.  Als uw toepassing wordt uitgevoerd binnen een bedrijfsnetwerk met strikte firewallbeperkingen, is Gateway-modus de beste keuze, omdat maakt gebruik van de standaard HTTPS-poort en één eindpunt. De verhouding prestaties is echter dat Gateway modus betrekking heeft op een extra netwerk-hop telkens wanneer gegevens worden gelezen of geschreven naar Cosmos-DB. Daarom biedt directe modus betere prestaties vanwege minder netwerkhops.
<a id="use-tcp"></a>
2. **Verbindingsbeleid: gebruiken het TCP-protocol**

    Wanneer u directe modus gebruikt, zijn er twee protocolopties beschikbaar:

   * TCP
   * HTTPS

     Cosmos DB biedt een eenvoudige en RESTful-programmeermodel openen via HTTPS. Daarnaast biedt het een efficiënte TCP-protocol, dat is ook RESTful in het communicatiemodel en is beschikbaar via de SDK voor .NET-clients. Directe TCP- en HTTPS worden SSL gebruiken voor eerste authenticatie en versleuteling verkeer. Gebruik indien mogelijk de TCP-protocol voor de beste prestaties.

     Bij gebruik van TCP in de modus van de Gateway, TCP-poort 443 is de Cosmos-DB-poort en 10255 is de MongoDB-API-poort. Als u TCP in directe modus, behalve de poorten voor de Gateway, moet u ervoor zorgen de poort bereik tussen 10000 en 20000 is geopend, omdat de Cosmos-database maakt gebruik van dynamische TCP-poorten. Als deze poorten niet geopend zijn en u probeert om TCP te gebruiken, ontvangt u een 503 Service niet beschikbaar-fout.

     De Connectiviteitsmodus wordt geconfigureerd tijdens het samenstellen van de DocumentClient-exemplaar met de parameter ConnectionPolicy. Als de modus Direct wordt gebruikt, kan het Protocol ook worden ingesteld binnen de ConnectionPolicy-parameter.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from the Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Omdat TCP wordt alleen ondersteund in de directe modus als Gateway-modus wordt gebruikt, het HTTPS-protocol wordt altijd gebruikt om te communiceren met de Gateway en de waarde van het Protocol in de ConnectionPolicy wordt genegeerd.

    ![Afbeelding van het beleid van Azure DB die Cosmos-verbinding](./media/performance-tips/connection-policy.png)

3. **Aanroepen van OpenAsync om te voorkomen dat de latentie starten op de eerste aanvraag**

    De eerste aanvraag heeft een hogere latentie standaard, omdat er voor het ophalen van de adres-routeringstabel. Om te voorkomen dat deze latentie starten op de eerste aanvraag, moet u OpenAsync() als volgt één keer tijdens de initialisatie aanroepen.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Clients in hetzelfde Azure-regio voor prestaties plaatsen**

    Indien mogelijk, plaatst u toepassingen Cosmos DB aanroepen in dezelfde regio bevinden als de database van de Cosmos-database. Voor een geschatte vergelijking aanroepen naar Cosmos DB binnen dezelfde regio binnen 1-2 ms voltooid, maar de latentie tussen de West en oostkust van de VS is > 50 ms. Deze latentie kan waarschijnlijk uit om aan te vragen variëren, afhankelijk van de route die door de aanvraag wordt uitgevoerd het doorgeven van de client aan de grens van de Azure-datacenter. De laagst mogelijke latentie wordt bereikt door ervoor te zorgen dat de aanroepende toepassing bevindt zich in dezelfde Azure-regio als de ingerichte Cosmos-DB-eindpunt. Zie voor een lijst met beschikbare regio's, [Azure-gebieden](https://azure.microsoft.com/regions/#services).

    ![Afbeelding van het beleid van Azure DB die Cosmos-verbinding](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **Verhoog het aantal threads/taken**

    Omdat aanroepen naar Azure Cosmos DB worden aangebracht via het netwerk, moet u wellicht de mate van parallelle uitvoering van uw verzoeken om te variëren, zodat de clienttoepassing nodig heeft voor het zeer weinig tijd wachten tussen aanvragen. Bijvoorbeeld als u. De NET [taak parallelle bibliotheek](https://msdn.microsoft.com//library/dd460717.aspx), maken in de volgorde van 100s van taken lezen of schrijven naar een Cosmos-DB.

## <a name="sdk-usage"></a>Gebruik van de SDK
1. **De meest recente SDK installeren**

    De Cosmos-DB SDK's zijn voortdurend wordt verbeterd, zodat de beste prestaties bieden. Zie de [Cosmos DB SDK](documentdb-sdk-dotnet.md) pagina's om te bepalen van de meest recente SDK en verbeteringen controleren.
2. **Een singleton Cosmos-DB-client gedurende de levensduur van uw toepassing gebruiken**

    Houd er rekening mee dat elk exemplaar DocumentClient thread-veilige en efficiënte Verbindingsbeheer en adrescaching in directe modus wordt uitgevoerd. Zodat efficiënt Verbindingsbeheer en betere prestaties door DocumentClient verdient het gebruik van één exemplaar van de DocumentClient per AppDomain gedurende de levensduur van de toepassing.

   <a id="max-connection"></a>
3. **System.Net MaxConnections per host verhogen als u de Gateway-modus**

    DB cosmos-aanvragen worden gedaan via HTTPS/REST bij gebruik van Gateway-modus en zijn onderworpen aan de standaardlimiet verbinding per hostnaam of IP-adres. Mogelijk moet u de MaxConnections ingesteld op een hogere waarde (100-1000), zodat meerdere gelijktijdige verbindingen met Cosmos DB van de clientbibliotheek gebruikmaken kan. In de .NET SDK 1.8.0 en hoger wordt met de standaardwaarde voor [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) 50 en de waarde wilt wijzigen, kunt u instellen de [Documents.Client.ConnectionPolicy.MaxConnectionLimit](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx)op een hogere waarde.   
4. **Parallelle query's voor gepartitioneerde verzamelingen afstemmen**

     DocumentDB .NET SDK versie 1.9.0 en hoger ondersteuning parallelle query's waarmee u kunt een query uitvoeren op een gepartitioneerde verzameling worden parallel (Zie [werken met de SDK's](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) en de verwante [codevoorbeelden](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) voor meer informatie Info). Parallelle query's zijn ontworpen voor betere Querylatentie en doorvoer via hun seriële equivalent. Parallelle query's bieden twee parameters die gebruikers afstemmen kunnen om de vereisten (a) MaxDegreeOfParallelism aangepaste aanpassen: om te bepalen dat het maximum aantal partities vervolgens kan worden opgevraagd in parallel en (b) MaxBufferedItemCount: om te bepalen het aantal vooraf opgehaalde resultaten.

    (a) ***afstemmen MaxDegreeOfParallelism\: *** parallelle query werkt door meerdere partities parallel uitvoeren van query's. Echter, gegevens van een afzonderlijke gepartitioneerde verzamelen ten opzichte van de query wordt opeenvolgend opgehaald. Dus heeft als u de MaxDegreeOfParallelism op het aantal partities de maximale kans op de meeste query zodat opgegeven alle andere voorwaarden system hetzelfde blijven. Als u het aantal partities niet weet, kunt u de MaxDegreeOfParallelism instellen op een groot aantal en het systeem de minimale (aantal partities, invoer van de gebruiker opgegeven) als de MaxDegreeOfParallelism kiest.

    Het is belangrijk te weten dat parallelle query's de beste prestaties opleveren als de gegevens evenredig verdeeld over alle partities ten opzichte van de query. Als de gepartitioneerde verzameling zodanig dat alle of een meerderheid van de gegevens die door een query zijn geretourneerd voornamelijk in een paar partities (één partitie in ergste geval) en de prestaties van de query als knelpunt zou worden verwerkt door deze partities is gepartitioneerd.

    (b) ***afstemmen MaxBufferedItemCount\: *** parallelle query is ontworpen om de resultaten vooraf ophaalt tijdens de huidige batch met resultaten wordt verwerkt door de client. Het vooraf ophalen helpt in algemene verbetering van de latentie van een query. MaxBufferedItemCount is de parameter om het aantal vooraf opgehaalde resultaten te beperken. Instelling MaxBufferedItemCount met het verwachte aantal resultaten geretourneerd (of een hogere waarde), kunt de query voor het ontvangen van maximaal profiteren van het vooraf ophalen.

    Houd er rekening mee dat vooraf ophalen werkt op dezelfde manier ongeacht de MaxDegreeOfParallelism, en er één buffer voor de gegevens van alle partities.  
5. **Schakel op de GC-serverzijde**

    In sommige gevallen kan minder vaak uit garbagecollection helpen. Stel in .NET, [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) op true.
6. **Backoff RetryAfter intervallen implementeren**

    Tijdens het testen van prestaties, moet u load verhogen tot een klein aantal aanvragen ophalen beperkt. Als beperkt, moet de clienttoepassing backoff op vertraging voor de server opgegeven interval. De backoff te respecteren, zorgt u ervoor dat u besteden aan de minimale hoeveelheid tijd wachten tussen nieuwe pogingen. Ondersteuning voor nieuwe pogingen Groepsbeleid is opgenomen in versie 1.8.0 en hoger van de DocumentDB [.NET](documentdb-sdk-dotnet.md) en [Java](documentdb-sdk-java.md), versie 1.9.0 en hoger van de [Node.js](documentdb-sdk-node.md) en [Python ](documentdb-sdk-python.md), en alle ondersteunde versies van de [.NET Core](documentdb-sdk-dotnet-core.md) SDK's. Zie voor meer informatie [Exceeding gereserveerd doorvoerlimieten](request-units.md#RequestRateTooLarge) en [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Uitbreiden van de werkbelasting van uw client**

    Als u op niveaus met hoge doorvoer testen wilt (> 50.000 RU/s), de clienttoepassing mogelijk het knelpunt als gevolg van de machine beperking af op CPU- of -gebruik. Als u deze punt bereikt, kunt u blijven voor de push-het account Cosmos DB verder door het uitbreiden van uw clienttoepassingen op meerdere servers.
8. **Cache document URI's voor lagere latentie mogelijk lezen**

    Cache document URI's waar mogelijk voor de beste prestaties voor lezen.
   <a id="tune-page-size"></a>
9. **De paginagrootte van de voor query's leestijd feeds voor betere prestaties afstemmen**

    Bij het uitvoeren van een bulksgewijs documenten met behulp van de feed functionaliteit (bijvoorbeeld ReadDocumentFeedAsync) lezen of lezen bij de uitgifte van een DocumentDB SQL-query, worden de resultaten in een gesegmenteerde manier geretourneerd als de resultatenset is te groot is. Standaard resultaten worden geretourneerd in segmenten van 100 items of 1 MB, eerst de limiet is bereikt.

    Verminder het aantal netwerk retouren vereist voor het ophalen van alle toepasselijke resultaten, kunt u de paginagrootte met behulp van de aanvraagheader x-ms-max--aantal items en maximaal 1000 vergroten. In gevallen waarin u wilt alleen enkele resultaten weer te geven bijvoorbeeld, als uw gebruikers-interface of toepassing API retourneert alleen 10 een tijd resulteert, u kunt ook de paginagrootte van de op 10 tot en met de doorvoer verbruikt voor leesbewerkingen en query's verminderen verlagen.

    U kunt ook de paginagrootte met behulp van de beschikbare Cosmos-DB SDK's instellen.  Bijvoorbeeld:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Verhoog het aantal threads/taken**

    Zie [Verhoog het aantal threads/taken](#increase-threads) in de sectie over netwerken.

11. **Gebruik 64-bits host verwerken**

    De DocumentDB SDK werkt in een 32-bits hostproces wanneer u de DocumentDB .NET SDK versie 1.11.4 gebruikt en hoger. Als u over verschillende partitie query's gebruikt, wordt 64-bits host verwerken echter aanbevolen voor verbeterde prestaties. De volgende soorten toepassingen hebben het hostproces van 32-bits als de standaardconfiguratie, om te wijzigen die in 64-bits, volg deze stappen uit op basis van het type van uw toepassing:

    - Voor uitvoerbare toepassingen kunt dit doen door het uitschakelen van de **liever 32-bits** optie in de **Projecteigenschappen** venster op de **bouwen** tabblad.

    - Voor VSTest op basis van de Testprojecten, kunt u dit doen door te selecteren **testen**->**instellingen testen**->**processorarchitectuur standaard als X64**, van de **Visual Studio Test** menuoptie.

    - Voor lokaal geïmplementeerde ASP.NET-webtoepassingen, kunt dit doen door het controleren van de **de 64-bits versie van IIS Express gebruiken voor websites en projecten**onder **extra**->**opties**  -> **Projecten en oplossingen**->**Web-projecten**.

    - Voor ASP.NET-webtoepassingen wordt geïmplementeerd in Azure, kan dit worden gedaan door het kiezen van de **Platform als 64-bits** in de **toepassingsinstellingen** in de Azure portal.

## <a name="indexing-policy"></a>Indexeringsbeleid
1. **Gebruik vertraagde indexering voor snellere piek tijd opname tarieven**

    Cosmos DB kunt u opgeven – op het niveau verzameling – indexeringsbeleid, waarmee u als u wilt dat de documenten in een verzameling automatisch worden geïndexeerd of niet.  U kunt bovendien ook tussen synchrone (consistente) en updates van de index asynchrone (Lazy). De index wordt standaard synchroon bijgewerkt op elke invoegen, vervangen of verwijderen van een document aan de verzameling. Synchroon modus maakt het mogelijk de query's te voldoen aan dezelfde [consistentieniveau](consistency-levels.md) als die van het document wordt gelezen zonder enige vertraging voor de index te 'lopen'.

    Vertraagde indexeren kan worden overwogen om scenario's waarin gegevens worden geschreven in bursts en gewenste om het werk dat nodig is tot inhoud van de index gedurende een langere periode af te schrijven. Vertraagde indexeren kunt u uw ingerichte doorvoer effectief gebruiken en dienen schrijfaanvragen piekuren met een minimale latentie. Het is belangrijk te weten echter dat als vertraagde indexeren is ingeschakeld, queryresultaten uiteindelijk consistent, ongeacht de consistentieniveau geconfigureerd voor het account van de Cosmos-DB zijn.

    Daarom Consistent indexing-modus (IndexingPolicy.IndexingMode is ingesteld in Consistent) leidt ertoe dat de hoogste aanvraag eenheid kosten per schrijfbewerking tijdens het indexeren modus (IndexingPolicy.IndexingMode is ingesteld op Lazy) en geen indexering Lazy (IndexingPolicy.Automatic is ingesteld op False) hebben nul indexering kosten op het moment van schrijven.
2. **Ongebruikte paden uitsluiten van indexering voor snellere schrijfbewerkingen**

    Indexeringsbeleid cosmos van de database kunt u opgeven welke paden document wilt opnemen of uitsluiten door gebruik te indexeren paden (IndexingPolicy.IncludedPaths en IndexingPolicy.ExcludedPaths) te indexeren. Het gebruik van de indexering van paden kunt bieden verbeterde schrijfprestaties en lagere opslagkosten voor index voor scenario's waarin de querypatronen tevoren bekend als indexering kosten rechtstreeks worden gecorreleerd met het aantal unieke paden die zijn geïndexeerd.  De volgende code ziet u bijvoorbeeld een hele sectie van de documenten (ook uitsluiten een substructuur) vanuit indexering met de ' * ' jokerteken.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Zie voor meer informatie [Azure Cosmos DB indexeren beleid](indexing-policies.md).

## <a name="throughput"></a>Doorvoer
<a id="measure-rus"></a>

1. **Meten en stemmen voor lagere aanvraag eenheden/seconde gebruik**

    Cosmos DB biedt een uitgebreide reeks databasebewerkingen, met inbegrip van relationele en hiërarchische query's met UDF's, opgeslagen procedures en triggers – alle operationele op de documenten binnen een verzameling van de database. De kosten die zijn gekoppeld aan elk van deze bewerkingen varieert op basis van de CPU, IO en geheugen dat nodig is om de bewerking te voltooien. In plaats van het denken over en beheer van hardwareresources, kunt u een aanvraag-eenheid (RU) beschouwen als een enkele meting voor de resources die zijn vereist voor het uitvoeren van verschillende databasebewerkingen en de aanvraag voor een toepassing.

    [Aanvraageenheden](request-units.md) zijn ingericht voor het account van elke database op basis van het aantal eenheden voor capaciteit die u aanschaft. Aanvraag eenheidsverbruik wordt geëvalueerd als een percentage per seconde. Toepassingen die groter is dan het percentage van de eenheid ingerichte aanvragen voor het account beperkt is tot de snelheid onder het gereserveerde niveau voor het account zakt. Als uw toepassing een hogere mate van doorvoer vereist, kunt u extra capaciteitseenheden aanschaffen.

    De complexiteit van een query heeft gevolgen voor het aantal eenheden van de aanvraag voor een bewerking worden verbruikt. Het aantal predicaten, aard van de predicaten, aantal UDF's en de grootte van de bron-gegevensset alle invloed hebben op de kosten van querybewerkingen.

    Voor het meten van de overhead van bewerkingen (maken, bijwerken of verwijderen) inspecteren van de header x-ms-aanvraag-kosten (of de equivalente RequestCharge-eigenschap in ResourceResponse<T> of FeedResponse<T> in de .NET SDK) voor het meten van het aantal aanvraageenheden verbruikt door deze bewerkingen.

    ```C#
    // Measure the performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure the performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    De aanvraag kosten geretourneerd in deze header is een fractie van de ingerichte doorvoer (dat wil zeggen, 2000 RUs / seconde). Als de voorgaande query 1000 1KB-documenten retourneert, is de kosten van de bewerking 1000. Als zodanig binnen één seconde respecteert de-server slechts twee dergelijke aanvragen voordat de beperking van de volgende aanvragen. Zie voor meer informatie [Aanvraageenheden](request-units.md) en de [aanvraag eenheid Rekenmachine](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Verwerken frequentie beperken/aanvraagsnelheid te groot**

    Wanneer een client probeert overschrijdt de gereserveerde doorvoer voor een account, is er geen verslechtering van prestaties optreedt op de server en geen gebruik van doorvoercapaciteit afgezien van het niveau van de gereserveerde. De server wordt optie preventief beëindigen van de aanvraag met RequestRateTooLarge (HTTP-statuscode 429) en de x-ms-opnieuw-na-ms-header die de hoeveelheid tijd in milliseconden, dat de gebruiker wachten moet voordat de aanvraag opnieuw proberen aangeeft retourneren.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    De SDK's alle impliciet dit antwoord catch, wordt de server opgegeven probeer het opnieuw nadat de header en de aanvraag opnieuw proberen. Tenzij uw account wordt door meerdere clients tegelijkertijd geopend, wordt de volgende poging slaagt.

    Als er meer dan één client cumulatief werken consistent boven het percentage aanvragen, het aantal nieuwe pogingen van standaard ingesteld op 9 intern door de client niet toereikend zijn; in dit geval, genereert de client een DocumentClientException met statuscode 429 tot de toepassing. Het aantal standaard pogingen kan worden gewijzigd door de RetryOptions op het exemplaar ConnectionPolicy. Standaard wordt de DocumentClientException met statuscode 429 na een cumulatieve wachttijd van 30 seconden geretourneerd, als de aanvraag blijft werken boven het percentage aanvragen. Dit gebeurt zelfs als het huidige aantal pogingen is kleiner dan het maximale aantal, worden deze de standaardwaarde van 9 of een door de gebruiker gedefinieerde waarde.

    Terwijl het gedrag voor het automatisch opnieuw kan worden verbeterd tolerantie en bruikbaarheid voor de meeste toepassingen, kan deze op odds zijn bij het uitvoeren van prestatiebenchmarks, vooral wanneer latentie meten.  De latentie waargenomen-client wordt pieken als het experiment treffers in de beperking van de server en zorgt ervoor dat de client SDK achtergrond opnieuw proberen. Meten van de kosten die zijn geretourneerd door elke bewerking om te voorkomen latentiepieken tijdens prestaties experimenten, en zorg ervoor dat aanvragen worden gebruikt onder het gereserveerde percentage. Zie voor meer informatie [Aanvraageenheden](request-units.md).
3. **Ontwerp voor kleinere documenten voor een hogere doorvoer**

    De kosten van de aanvraag (dat wil zeggen aanvraagverwerking kosten) van een bepaalde bewerking wordt rechtstreeks gecorreleerd met de grootte van het document. Bewerkingen op grote documenten duurder dan bewerkingen voor kleine documenten.

## <a name="next-steps"></a>Volgende stappen
Zie voor een voorbeeldtoepassing gebruikt om te evalueren Cosmos DB voor scenario's met hoge prestaties op enkele clientcomputers, [prestaties en schaal testen met Cosmos DB](performance-testing.md).

Zie ook voor meer informatie over het ontwerpen van uw aanvraag voor schaal en hoge prestaties, [partitionering en schalen in Azure Cosmos DB](partition-data.md).
